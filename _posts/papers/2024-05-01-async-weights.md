---
layout: post
title: "How Hard is Asynchronous Weight Reassignment?"
date: 2024-05-01 07:00:00 -0700
mathjax: true
categories: papers
tags: software-engineering distributed-systems academic weights wqms quorum
---

_Summary of [How Hard is Asynchronous Weight Reassignment?](https://arxiv.org/pdf/2306.03185)_

Majority quorum systems are useful in providing a simple mechanism for consensus. To accept a value, you need a majority of servers to agree to accepting it. Weighted majority quorum services (WQMS) take this approach and recognise that some servers are going to have better performance than others, so they should get more voting power. 

<!--more-->

The main contribution of this paper is defining three ways of reassigning weights in a WQMS. The first two are shown to be as difficult as consensus, while the third can be performed consensus-free. 

I'm not fully sure how practically useful this is, but that's also because I don't know much about the real world uses of WQMS! As far as the paper goes, it's very clearly written, with some nicely presented proofs. 

### Weight Reassignment
The paper presents the problem of weight reassignment. Solving this problem means providing an algorithm to update the weights of a static set of servers running a WQMS. 

Weight reassignment has some restrictions. With the system, we want to be able to tolerate up to $f$ servers (out of a total $n$) crashing at once. This means that we need to place a limit on the total weight of the $f$ most weighted servers, we'll call this set $F$, so they have less than half of the total weight. This way, if *any* $f$ servers fail, the remaining $n - f$ can continue to make progress. We call this restriction *integrity*. 

This means that we can't reassign weights in a way that would violate integrity. Say we had a quorum of 5 servers ($n = 5$), each with a voting weight of $1$, and we wanted to tolerate up to two server failures, so $f = 2$. If we were to add $2$ to the weight of any of the servers, now the $f$ top weighted servers would have a weight of $4$, and the total weight would be $7$. Since the weight of $F$ is greater than half of the total weight, this would violate integrity. 

There are three other restrictions on the weight reassignment algorithm that are simpler:
- Validity-I - when a weight change is proposed, if it violates integrity then a no-op change (a change with zero weight difference) is created. If it *doesn't* violate integrity then the proposed change is created.
- Validity-II - there's an API clients can use to check the weights of a server $s$, `read_changes(s)`. When it's called, a client gets a list of all of the weight changes made to $s$, from which they can reconstruct the current weight of $s$ by summing the changes. 
- Livesness - if a server calls `reassign`, the operation will eventually complete, and the server will get back a message indicating the set of changes made.

#### Equivalence to consensus

Laid out in this way, the authors go on to show that this problem is equivalent to consensus, meaning it's at least as difficult to solve. Given we're using a quorum system to solve consensus, that sounds like it would defeat the point! 

I really liked the proof they use to demonstrate this. The authors construct a scenario in which every server proposes a weight change. These changes are constructed such that one, and only one, of the weight changes can succeed with a non-zero weight change. If two or more of the changes succeeded, then integrity would be violated. 

For the proof, the servers are divided into two disjoint sets, $F$ and $S \backslash F$, where $F$ is the set of servers $F = \{ s_1, s_2, ..., s_f\}$. $S$ is the set of all servers, so $S \backslash F$ is the set of all servers not in $F$. Note that the sets have the following lengths $\|S\| = n, \|F\| = f, \|S \backslash F\| = n - f$. The initial weight of each server $s \in F$ is $\frac{n - 1}{2f}$ while the weight of every server $s \in S \backslash F$ is $\frac{n+1}{2(n - f)}$. We can call the total weight of a set $S$ at time $t$: $\texttt{W}_{S,t}$. Based on the initial weights of each server in the sets, $\texttt{W}_{F,0} = \frac{n - 1}{2f} \times f$ and $\texttt{W}_{S \backslash F,0} = \frac{n+1}{2(n - f)} \times (n - f)$. Since  $\frac{n - 1}{2} < \frac{n+1}{2}$, we can see that the total weight of $F$ is less than the total weight of $S \backslash F$ and integrity is satisfied by the initial weights. 

Each of the servers $s_i$ proposes a weight change. For the servers in $F$, they propose adding $0.5$ to their weight: $\texttt{reassign}(s_i, 0.5)$, while all servers in $S \backslash F$ propose subtracting $0.5$ from their weight: $\texttt{reassign}(s_i, -0.5)$. From this, we can see that accepting one of these changes would not violate integrity. E.g., if we accept one change from $F$, then the new total weight of $F$ becomes $\frac{n - 1}{2} + 0.5$, which is still less than $\frac{n+1}{2}$. Similarly, if we accept one change from $S \backslash F$, then $\texttt{W}_{S \backslash F,1} = \frac{n+1}{2} - 0.5$. 

However, it's clear that if we accept more than one change in any combination then integrity will be violated. E.g., if we accept one change from both sets, we can see that $\frac{n - 1}{2} + 0.5 = \frac{n+1}{2} - 0.5$, which would violate integrity. Since if a change doesn't violate integrity we have to accept it, then we must accept one and only one change, which is the same as deciding consensus on a value between the group. The paper also provides an algorithm for solving consensus by proposing weight changes and deciding on one, which is fun but probably not as interesting or useful as the equivalence proof. 

#### Pairwise weight reassignment

The authors then tried restricting the problem to make it easier to solve. If it's hard to arbitrarily re-assign weights up and down among the servers, what about only allowing pairs of servers to exchange weights? E.g., for server $s_2$ to gain a weight, some other server $s_4$ needs to lose the same amount of weight. This means that the total weight of all servers can remain constant throughout. 

Apart from this change, weight reassignment remains the same. The integrity requirement is still in place. Instead of a server proposing $\texttt{reassign}$, they can propose to $\texttt{transfer}(s_i, s_j, \Delta)$, where the $\Delta$ change in weight is taken from $s_i$ and given to $s_j$ if integrity is not violated. If integrity would be violated by the change, then two zero weight changes are created (one for $s_i$ and one for $s_j$).

The authors then show in much the same way that this is also equivalent to consensus. Just like before, they craft a scenario based on the sets of servers $F$ and $S \backslash F$ where one and only one weight $\texttt{transfer}$ can complete with a non-zero weight, showing that the problem is equivalent to consensus. The proof is pretty similar to the previous one so I won't go in to the exact scenario. Again, they provide an algorithm for consensus based on this impossibility proof. 

#### Restricted pairwise weight reassignment
Finally the authors introduce restricted pairwise weight reassignment, which can be performed *without* consensus. There are two restrictions they place on transfer:
1. Only $s_i$ can call $\texttt{transfer}(s_i, *, \Delta)$. So only $s_i$ can transfer away some of its weight 
2. The weight of $s_i$ has to always be greater than $\frac{\texttt{W}_{S,0}}{2(n - f)}$. That means there's a floor on the weight of each server, such that if each server in $S \backslash F$ had this weight, they would have the majority vote.

The authors assert that if the first condition holds, then the second is locally verifiable, meaning it can be done without consensus. I found this argument pretty straight forward! Any server can give away its weight, but only while remaining greater than the floor weight, leaving all of the servers not in $F$ with enough weight to continue as a quorum. This is proved with the inequality:

$$|S\backslash F| \times \frac{\texttt{W}_{S, 0}}{2(n - f)} = \frac{\texttt{W}_{S, 0}}{2}$$

So $\texttt{W}\_{S \backslash F, t} > \frac{\texttt{W}_{S, 0}}{2}$ and integrity is preserved at all times. 

The reason no other server can take away another's weight without consensus is that if we have any two servers trying to take away weight from some server $s_i$, then while either of them could make a transfer recognizing the second condition, there's no way for both transfers to succeed without some form of consensus to decide which succeeds. 

### Thoughts

The authors proved this result for a static set of servers. It would be great to see if the results could be extended for a dynamic set of servers, but given all of the proofs relied on a static set I'd imagine that would be hard. At the minimum you could imagine using consensus to decide weights as you add/remove servers, before switching back to the consensus free weight reassignment.

How useful is it? You can easily imagine a scenario where a server doesn't know that it's holding up progress for a quorum, and since only servers can give away their own weight, that might prove tricky to use in practice. It would be great to see an experimental evaluation to see how helpful this could be.