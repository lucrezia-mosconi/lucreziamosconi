---
title: Knowledge Compilation
tags:
categories:
date: 2024-10-06
lastMod: 2025-02-04
---
# Darwiche

![1106.1819v1.pdf](/assets/1106.1819v1_1728213205808_0.pdf)

  + ### Main idea

    + Given a propositional theory T, we want to compile it in a target language such that answering queries can be done online in polytime.

    + > Three components:
1. Succinctness of the target language in which the proposition is compiled
2. Class of queries that can be answered in polytime
3. Class of transformations that can be answered in polytime

    + {{< logseq/orgIMPORTANT >}}**Target compilation language** T $\Leftrightarrow$ T supports clausal entailment in polytime
{{< / logseq/orgIMPORTANT >}}

  + 

  + ### **Key properties:**

    + |Property |Description|
|Smoothness|Disjuncts mention the same set of variables|
|Decomposability|Conjuncts do not share variables|
|Determinism|Disjuncts are logically disjoint (i.e. contradictory)|

  + 

  + > **Succintness**: $L_1$ at least as succint as $L_2$ if there exists a polynomial p such that for every sentence $\alpha$ in $L_2$ there is an equivalent sentence $\beta$ in $L_1$ and $|\beta| < p|\alpha|$

  + ### **Key Queries**

    + |Query|Description|
|CO| Polytime consistency check|
|VA| Polytime validity check|
|CE| Polytime clausal entailment check|
|IM| Polytime implicant check|
|EQ| Polytime equivalence check|
|SE| Polytime sentential entailment check|
|CT| Polytime model counting|
|ME| Polytime model enumeration|

  + 

  + {{< logseq/orgIMPORTANT >}}$OBBD_<$ and MODS are the only languages supporting **all** queries in polytime
{{< / logseq/orgIMPORTANT >}}

  + ## Transforming Compiled Theories





# Algebraic Model Counting

![1211.4475v1.pdf](/assets/1211.4475v1_1728213361667_0.pdf)

  + {{< logseq/orgPINNED >}}Weighted model counting is an extension of \# SAT in which we want to compute the weighed sum of a theory's models. Here it is extended beyond the probabilistic setting and generalised for any semiring structure
{{< / logseq/orgPINNED >}}

  + > **Problem Setup** 
Given: 
{{< logseq/orgCENTER >}}1. a propositional logic theory T over a set of variables V 
2. a commutative semiring $(A, \oplus, \otimes, e^\otimes, e^\oplus)$
3. A labelling function $\alpha: \mathcal{L} \rightarrow A$ which maps literals $\mathcal{L}$ of the variables in V to elements of the semiring set A
#+END_CENTER
Compute: 
#+BEGIN_CENTER
A(T) = $\bigoplus \bigotimes \alpha (l)$
{{< / logseq/orgCENTER >}}
A(T) is the algebraic model count over the set of models M(T) of the propositional theory T

  + 

  + Many problems can be transformed into AMC by defining the appropriate semiring and labelling function.

  + 

  + ### sd-DNNF evaluation

  + > This is the easiest case, as we can use the properties (Smoothness, Decomposability & Determinism)

  + ### Other decomposable circuits

  + We need restrictions to make this easily computable, and we apply restrictions to the $(\oplus, \alpha)$ components.

  + |Idempotent $\odot$| $\odot$ is an idempotent operator if for all elements a $\in \mathcal{A},a \odot a = a$ | 
|Neutral $(\oplus, \alpha)$ | $(\oplus, \alpha)$  neutral if for all $ v \in \mathcal{V}, \alpha (v) \oplus \alpha (\neg v) = e^\oplus |

  + ### Non-Decomposable circuits

    + We need further restrictions on the $(\oplus, \alpha)$ pair in order for this to work

  + 

  + 

  + 

# Algebraic Circuits for Decision Theoretic Inference and Learning

![FAIA-325-FAIA200392.pdf](/assets/faia-325-faia200392_1728219992472_0.pdf)

### Main idea

Algebraic circuits can solve decision theoretic inference and a utility learning task under partial observability.

### Knowledge Compilation



{{< logseq/orgCENTER >}}**Sentential decision diagrams (SDD):**
{{< / logseq/orgCENTER >}}

> **Definition** 
 > Represents a logic theory T and it is eitheer a constant ($\top$, $\bot$ ),  a literal or a decomposition node {($p_1, s_1), \ldots, (p_n, s_n$)}.
     > The latter represents $\vee^n_{i = 1} p_i \land s_i$, where $p_i, s_i$ are both SDDs. A decomposition node is an or-node which partitions the theory into disjoint children ($p_i, s_i$), which are called the elements of the decomposition node. 
     > The pair $p_i, s_i$ represents a conjunction of both, and $s_i$ represents the parent theory conditioned on $p_i$

{{< logseq/orgCENTER >}}**Vtree**
{{< / logseq/orgCENTER >}}

> **Definition**
Full binary tree in which each SDD variable appears in a leaf node, and it determines the construction of an SDD by determining the variables present in the primes and subs of each SDD node.
{{< logseq/orgCENTER >}}We say that a SDD $\alpha$ **respects** a vtree *v* iff: 
{{< / logseq/orgCENTER >}}
$\alpha = \bot \ or \top$
$\alpha = X$ or $\alpha = \neg X$ and *v* contains variable X 
$\alpha = {(p_1, s_1), \ldots, (p_n, s_n)} $ and each $(p_i, \ldots p_n)$ are SDD that respect the subtrees of $v^l$, and $s_1, \ldots, s_n$ are SDD's that respect $v^r$ and $\langle p_1 \rangle \ldots \langle p_n \rangle$ is a partition



{{< logseq/orgIMPORTANT >}}To obtain an *arithmetic circuit* from the SDD, we replace or-nodes with + and and-nodes with $\times$. we can then evaluate it bottom-up to obtain the WMC at the root node.  +, \times  can be generalised if leaves are semiring elements and we obtain an *algebraic circuit*
{{< / logseq/orgIMPORTANT >}}

{{< logseq/orgCENTER >}}**Further Definitions** 
{{< / logseq/orgCENTER >}}

> A vtree node *v* is X-constraied if v appears on the rightmost path of the vtree and X is the set of variables outside *v*.
A vtree is X-constrained if it has an X-constrained nodes.



## Using AMC for Maximising Expected Utility (Decision Theoretic Inference)

### Main idea

Instead of having a simple expected utility semiring, we introduce decision variables and want the assignment of truth values to those decisions which maximise expected utility.



> **Definition**
 We have a propositional logic theory T over a set of decision variables D and a set of *stochastic* variables S, where each is associated with a probability and a utility.

#### Problem Setup

> Given:
{{< logseq/orgCENTER >}}    1. Decision variables have probability 0 or 1.
	2. $D_v$ := an assignment of truth values for each decision variable d ∈ D
	3. T[D: $D_v$] is the theory T when the truth values of variables in D are set to $D_v$
#+END_CENTER
Find the best truth assignment $D_v$ such that the expected utility is maximised, i.e.


#+BEGIN_CENTER
$argmax_{D_v}$ $\sum_{m \in \mathcal{M}T[D: D_v]  }$ $(\prod_{l \in m }$ $p_l$ ) $\sum_{l \in m} u_l$
{{< / logseq/orgCENTER >}}

{{< logseq/orgCAUTION >}}This task consists of three operations (max, sum and product) while the semiring operators are only two, which means applying AMC in this scenario is **not trivial**
{{< / logseq/orgCAUTION >}}



### Case 1: Constrained Circuits

**Problem setup**

In the case in which our circuit is X-constrained, we can use a semiring structure to solve the problem as follows:

> We use the following structure, which stores the decision information in the semiring elements in the form of a decision set L, ad perform maximisation when the decision sets are different. 
{{< logseq/orgCENTER >}}($\mathcal{A}, \oplus, \otimes, e^\oplus, e^\otimes$) where: 
{$\alpha (v) = (p_v, p_v \times u_v, L_v | v \in D \cup S)$} $\subset A$, with $L_v = {v}$ if v $\in D$, and $L_v =  \varnothing$ if $v \in S$
{{< / logseq/orgCENTER >}}

The operations are defined as follows:



$a \oplus b$ = 
logseq.order-list-type:: number
1.1 max(a, b) if $L_a \neq L_b$ 
1.2 ($p_a + p_b, eu_a + eu_b, L_a$) otherwise

$a \otimes b$ = ($p_a p_b, p_a eu_b + p_b eu_a, L_a \cup L_b$)
logseq.order-list-type:: number

$e^\oplus = (0, 0, D \cup \neg D)$
logseq.order-list-type:: number

$e^\otimes = (1, 0, \varnothing)$
logseq.order-list-type:: number

logseq.order-list-type:: number

### Case 2. Unconstrained circuits

**Problem setup**

Since the vtree that yields the smallest circuit is not necessarily X-Constrained, and constraining it may lead to larger circuits. Instead of doing this, we use another procedure, which does the maximisation **outside** the circuit. It treats the circuit as a function where decision values have to be chosen such that the output of a function (Expected Utility) is maximised.

{{< logseq/orgIMPORTANT >}}The problem is solved via gradient ascent and we compute the gradient using the circuit and AMC. Since we use GD, we are *not* guaranteed an optimal decision. 
{{< / logseq/orgIMPORTANT >}}

The function to optimise is the one given by the algebraic circuit, i.e.



{{< logseq/orgCENTER >}}MEU = $\sum_{m \in \mathcal{M}(T)} U(m) \times P(m)$
{{< / logseq/orgCENTER >}}



## Learning Utility Parameters





# Semiring Programming

![1-s2.0-S0888613X20302073-main.pdf](/assets/1-s2.0-s0888613x20302073-main_1728213428057_0.pdf)



# Compilation and Communication Complexity

{{< logseq/orgPINNED >}}Uses the notion of a **combinatorial rectangle** to obtain a lower bound on the representation size of DNNFs, i.e. displays a general technique. This allows to translate lower bounds from communication complexity into lower bounds for DNNF representations. 
{{< / logseq/orgPINNED >}}

> **Definition** : Combinatorial Rectangle
     > Let X be a finite set of variables. Then a combinatorial rectangle over X is a function $r : \{ 0,1\}^X \rightarrow \{ 0,1\}$ such that there is a partition $(X_1, X_2)$ of X and functions $r^i : \{ 0,1\}^{X_i} \rightarrow \{ 0,1\}$ for $i \in \{ 1, 2\}$ such that sat(r) = $sat(r^1) \times sat(r^2)$ . 
    > We call R $\subseteq \{0,1\}^X$ a rectangle over X with underlying partition $(X_1, X_2)$  if there is a rectangle $ r : \{ 0,1\}^X \rightarrow \{ 0,1\}$ with partition $(X_1, X_2)$  such that R = sat(r)



> **Definition**: Rectangle Cover
Let $f : \{ 0,1\}^X \rightarrow \{ 0,1\}$ be a function. A finite set $\{r_i\}$ of rectangles over X is called a rectangle cover iff sat(f) = $\bigcup_i sat(r_i)$



# Second Order Weighted Model Counting

Previously: One semiring structure to generalise sum product problems.

![efficient-knowledge-compilation-beyond-weighted-model-counting.pdf](/assets/efficient-knowledge-compilation-beyond-weighted-model-counting_1731322897639_0.pdf)



MAP inference and Optimization



> Monoids and Semirings

> Definition: X-Firstness
Given NNF n partitioned into X, Y. a node $n_i$  is **pure** if  all variables of $n_i$  are a subset of either X or Y (*mixed* otherwise). X-firstness means that  for each **and** node  n: either its children are all pure nodes, or one is mixed and the rest are pure with all of them being a subset of X.



> **Problem Setup**
{{< logseq/orgCENTER >}}T is a propositional Theory 
$X_I, X_O$ a Partition of T 
$S_j$ a commutative semiring as above 
$a_j$ is a labelling function 
$t_i$ is a weight transformation
{{< / logseq/orgCENTER >}}

{{< logseq/orgIMPORTANT >}}***VALUE OF A*** 
$2AMC(A) = \oplus_{x_o \in int(X_O)}^O \otimes _{x \in x_o}^o$
{{< / logseq/orgIMPORTANT >}}

{{< logseq/orgNOTE >}}2AMC can be solved in polynomial time in the size of $\mathcal{T}$ when $\mathcal{T}$ is an $X_O$ first sd-DNNF, assuming constant time for semiring operations
{{< / logseq/orgNOTE >}}

> **MAP TASK**
Given a probabilistic logic program $\mathcal{L}$, a conjunction of observed literals **e** for a set of evidence atoms **E** and a set of ground query atoms **Q**
Find the most probable assignment **q** to Q given the evidence **e**, with **R** = **H** \ (**Q** $\cup$ **E**):

this requires the following:

summing probabilities over the truth values of the atoms in **R**,while keeping fixed the truth values for the atoms in **E** $\cup$ **Q**
logseq.order-list-type:: number

Determining the truth values of the atoms in **Q** that maximise the inner sum, thus our variable partition is $X_O$ = **Q** and **Q** $\cup$ **R**
logseq.order-list-type:: number

logseq.order-list-type:: number
















