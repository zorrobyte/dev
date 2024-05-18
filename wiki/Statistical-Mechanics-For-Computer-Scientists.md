Statistical Mechanics for Computer Scientists
===

These are notes on statistical mechanics concepts with a focus
on interpreting them from the perspective of a computer scientist.
These should be considered personal opinions and, therefore, might
be completely misleading or outright wrong.

---

### Entropy

Entropy can be considered "the number of bits that it takes to describe a system".

That is if a system has $N$ possible states, each occurring with probability $p_i$, then
the number of bits to describe the system is:

$$
S _ { * } = - \sum_{i=0}^{N-1} p_i \cdot \lg( p_i )
$$

With $\lg(\cdot) = \frac{ \ln(\cdot) }{ \ln(2) }$.

---

### Boltzmann Distribution

The state $i$ is often called a "microstate".
If we have a set of microstates and start out with assigning each
of them energies, rather than probabilities, under suitable conditions,
we can derive a probability for each microstate.

If we assume each microstate has an energy, $E_i$, attached to it, we can
write down some equations:

$$
\begin{array}{ll}
1 = & \sum_{i} p_i \\\\
E = & \sum_{i} p_i E_i \\\\
S = & - \sum_{i} p_i \ln(p_i)
\end{array}
$$

Where we use $S_{*}$ to differentiate between the entropy defined with $\lg(\cdot)$ instead of $\ln(\cdot)$
For the derivations below, it's easier to work in natural logarithm ( $\ln (\cdot )$ ) rather than the logarithm
base 2 ( $\lg(\cdot)$ ) in addition to what is used in the physics literature.
The choice of base for the logarithm should only contribute a constant factor and shouldn't take away
from the broader ideas.

In the above, we make a few assumptions:

* Each of the microstate energies, $E_i$, is fixed and unchanging
* We impose the constraint that the average energy, $E$, is fixed
* The $p_i$ form a probability distribution

In other words find the maximum entropy, $S$, subject to the constraints
of $E_i$ chosen/fixed and an average fixed energy, $E$.

So, we want to maximize $S$ by varying each of the individual $p_i$'s.
We can use the method of Lagrange multipliers by using the two equations above as the constraints:

$$
\begin{align}
\vec{p} & = ( p_0, p_i, \cdots, p_{N-1} ) \\\\
L( \vec{p}, \alpha, \beta ) & = S - \alpha [ (\sum_{i} p_i) - 1 ] - \beta [ (\sum_{i} p_i E_i) - E ] \\\\
 & = - \sum_{i} p_i \ln(p_i) - \alpha [ (\sum_{i} p_i) - 1 ] - \beta [ (\sum_{i} p_i E_i) - E ] \\\\
\frac{\partial}{\partial p_i} L = & -ln(p_i) - 1 - \alpha - \beta E_i = 0 \\\\
\to \ \ & p_i = e^{-(1+\alpha)} e^{-\beta E_i}
\end{align}
$$

We can now define temperature:

$$
T = \frac{1}{\beta}
$$

And using one of the constraints, we can rewrite equations to get rid of the $\alpha$ term:

$$
\begin{align}
\sum_{i} p_i & = 1  \\\\
\to \ \ & \sum_{i} e^{ -\beta E_i } = e^{1 + \alpha} \\\\
\to \ \ & \sum_{i} e^{ \frac{E_i}{T} } = Z(T) \\\\
\to \ \ & Z(T) = e^{1 + \alpha}
\end{align}
$$

Which gives us:

$$
p_i = \frac{1}{Z(T)} e^{ -\frac{E_i}{T} }
$$

Adding a term,  $\kappa$, to $T$ and rewriting the probability as:

$$
p_i \propto e^{ -\frac{E_i}{\kappa T} }
$$

Is called a Boltzmann distribution.
Another name is Gibbs distribution.

$Z(T)$ is often called the partition function and acts as a renormalization constant.

Because of the partition function's ( $Z(T)$ ) relation to temperature and energy, among
other derived quantities, interrogating the partition function through the use of derivatives
of different variables can produce information about the underlying system.

---

### Kullback-Leibler Divergence

We want to talk about free energy but we will need the idea of
the Kullback-Leibler divergence first before providing intuition about the free energy
definition.

Consider an optimal encoding of sending $n$ symbols over a channel with the $i$'th symbol
occurring with probability $p_i$.
We can write the entropy of the distribution $p(\cdot)$ as:

$$
S_p = - \sum_{i}^{n-1} p_i \ln(p_i)
$$

Let's say we introduce another distribution $q(\cdot)$ that we will use to find an encoding/decoding
method on the symbols.
If the symbols are transmitted at the rate of $p_i$ but we're using $q_i$ to encode/decode them,
we end up with (proportionally) $\lg(q_i)$ bits per symbols instead of (proportionally) $\lg(p_i)$
bits per symbol.

We can write down the entropy of receiving these symbols with probability distribution $p_i$ but
using $q_i$ to encode them as:

$$
S_q = - \sum_{i}^{n-1} p_i \ln(q_i)
$$

The difference, $S_q - S_p$ is
how "bad" the $q_i$ encoding is in terms of how many extra bits we waste using the $q_i$ encoding.
If we introduce more notation:

$$
\begin{align}
S_q - S_p & = - [ \sum _ i p _ i \ln(q _ i) - \sum _ i p _ i \ln(p _ i) ] \\\\
\to D_{KL}(p || q) & \stackrel{\text{def}}{=}  \sum _ i p _ i \ln( \frac{p _ i}{q _ i} )
\end{align}
$$

Which is called the Kullback-Leibler Divergence.

Another way to write this is:

$$
D_{KL}(p || q) = H(p,q) - H(p)
$$

Where $H(p,q)$ is called the "cross entropy":

$$
\begin{align}
H(p) & = - \sum_{i} p_i \ln(p_i) \\\\
H(p,q) & = - \sum_{i} p_i \ln(q_i)
\end{align}
$$

---

### Helmholtz Free Energy

Helmholtz free energy is defined as the average energy minus the entropy:

$$
\begin{align}
F_H & = U - TS \\\\
 & = \sum_{i} p_i E_i + T \sum_{i} p_i \ln(p_i)
\end{align}
$$

Under equilibrium (?) recall

$$
\begin{align}
\ \ & p_i  = \frac{e^{ -\frac{E_i}{T} } }{Z} \\\\
\to \ \ & E_i  = -T \ln(p_i) - T \ln(Z) \\\\
\end{align}
$$

Shuffling around, we find:

$$
\begin{align}
F_H & = U - TS \\\\
 & = \sum_{i} p_i E_i + T \sum_{i} p_i \ln(p_i) \\\\
 & = - T \sum_{i} p_i \ln(p_i) - T \ln(Z) \sum_{i} p_i + T \sum_{i} p_i \ln(p_i) \\\\
 & = - T \ln(Z)
\end{align}
$$

Relating the log of the partition function (number of bits to describe the number of states),
modified by temperature, to the average energy minus the entropy.

For the sake of clarity:

$$
\begin{align}
F_H & = U - TS \\\\
F_H & = -T \ln(Z) \\\\
\end{align}
$$

---

### Gibbs Free Energy

If, instead we have a "trial" probability distribution $q_i$ but keep the energies of the microstates, $E_i$,
untouched, we get the Gibbs free energy:

$$
\begin{align}
F_G & = \sum_{i} q_i E_i - T S_q \\\\
 & = \sum_{i} q_i E_i + T \sum_{i} q_i \ln(q_i)
\end{align}
$$

Rearranging:

$$
\begin{align}
 F_G & = \sum_{i} q_i E_i + T \sum_{i} q_i \ln(q_i) \\\\
 & = -T \sum_{i} q_i \ln(p_i) - T \ln(Z) + T \sum_{i} q_i \ln(q_i) \\\\
 & = T \sum_{i} q_i \ln( \frac{q_i}{p_i} ) - T \ln(Z) \\\\
\end{align}
$$

$$
 F_G = T D_{KL}( q || p ) + F_H
$$

Relating Gibbs free energy to Helmholtz free energy by a factor of
the "divergence" of the probability distributions.

---

Appendix
---

### Lagrange Multipliers

Statement without proof.


$$
\begin{align}
& f,g \in C^1 & \\\\
& f:  \mathbb{R}^n   \mapsto \mathbb{R} & \\\\
& g: \mathbb{R}^n  \mapsto \mathbb{R}^m & \ \ \ (m < n) \\\\
& D h(x) = [ \frac{\partial h_j}{\partial x_k} ] &
\end{align}
$$

$$
\begin{align}
\text{ maximize: } & f(x) \\\\
\text{ subject to: } & g(x)=0 \\\\
\to \ \  &  x ^ * \text{ optimal } \\\\
& \exists \lambda ^ * \in \mathbb{ R } ^ m \\\\
\text{ s.t. } \  & D f(x ^ { \* }) = { \lambda ^ { \* } } ^ { \intercal } D g(x ^ { \* })
\end{align}
$$

In other words, subject to the constrained surface $g$, the maximum point on $f$ is achieved when when
the gradient of $f$ is equal and opposite to the constraint surface, $g$.

### Derivation of Entropy

See [Shannon Entropy](./Shannon-Entropy.html) but briefly recreated here for completeness.

Consider $n$ distinct symbols, each occurring with probability $p_k$ for $k \in (0,1,, \dots , n-1)$.
If a system is comprised of a collection of $B$ symbols, taken from the $n$ available,
with each assumed to be independent of each other,
and $B$ large, then $B \cdot p_k \cdot n$ is approximately integral and the
the number of ways of arranging $B$ symbols is:

$$
{ B \cdot n \choose (B \cdot p_0 \cdot n), (B \cdot p_1 \cdot n), \dots, (B \cdot p_{n-1} \cdot n) }
$$

$$
= \frac{(B \cdot n)!}{ {\prod} _ { k=0 } ^ { n-1 } (B \cdot p _ k \cdot n)!}
$$

The number of bits to describe the number of configurations is (with $\lg(\cdot) = \log_2(\cdot)$ ):

$$
\lg( \frac{(B \cdot n)!}{ {\prod} _ { k=0 } ^ { n-1 } (B \cdot p _ k \cdot n)!} )
$$

Which, after some algebra, reduces to:

$$
= - B \sum _ { k=0 } ^ { n-1 } p _ k \lg(p _ k)
$$

Define the entropy, $S$, to be the average number of bits needed to represent our system at a particular
point in time (that is, the average number of bits per symbol), we find:

$$
S = - \sum _ { k=0 } ^ { n-1 } p _ k \lg(p _ k)
$$


### Metropolis Hastings Algorithm

In this context, we sometimes want to sample from the Boltzmann distribution distribution.

Call a state of the system $s_t$ with the energy of the state $E_{s_t}$.
We call the transition probability:

$$
P( s_t \to s_{t+1} ) = \begin{cases}
  e^{- \beta ( E_{s_t} - E_{s_{t+1}} ) } & , & E_{s_{t+1}} > E_{s_t} \\\\
  1 & , & E_{s_{t+1}} \le E_{s_t} \\\\
\end{cases}
$$

Recall $\beta = \frac{1}{T}$.

Call the number of possible transition states from one state to the other $N(\cdot)$:

$$
\begin{array}{ll}
N( s_t \to s_{t+1} ) & \propto N_{s_t} e^{ -\beta ( E_{s_{t+1}} - E_{s_t} ) } \\\\
N( s_{t+1} \to s_t ) & \propto N_{s_{t+1}}
\end{array}
$$

If we assume:

$$
N_{s_t} > 0, N_{s_{t+1}} > 0 \\\\
N( s_t \to s_{t+1} ) = N( s_{t+1} \to s_t )
$$

Then:

$$
\begin{array}{ll}
 & N( s_t \to s_{t+1} ) - N( s_{t+1} \to s_t ) = N_{s_t} e^{ -\beta ( E_{s_{t+1}} - E_{s_t} ) } - N_{s_{t+1}} \\\\
\to & 0 = N_{s_t} e^{ -\beta ( E_{s_{t+1}} - E_{s_t} ) } - N_{s_{t+1}} \\\\
\to & 0 = N_{s_t} ( \frac{ e^{ -\beta E_{s_{t+1}} }}{ e^{ - \beta E_{s_t} } }  - \frac{ N_{s_{t+1}} }{ N_{s_t} } ) \\\\
\to & 0 = \frac{ e^{ -\beta E_{s_{t+1}} }}{ e^{ - \beta E_{s_t} } }  - \frac{ N_{s_{t+1}} }{ N_{s_t} } \\\\
\to & \frac{ N_{s_{t+1}} }{ N_{s_t} } = \frac{ e^{ -\beta E_{s_{t+1}} }}{ e^{ - \beta E_{s_t} } } \\\\
\to &  N_{s_{t+1}} e^{ - \beta E_{s_t} } = N_{s_t} e^{ -\beta E_{s_{t+1}} }   \\\\
\end{array}
$$

Which is a detailed balance condition ensuring it be an ergodic process.


References
---


* [susskind](https://www.youtube.com/watch?v=rhFkYjaM5kE&list=PL_IkS0viawhr3HcKH607rXbVqy28W_gB7&index=4)
* [Gibbs free energy](https://en.wikipedia.org/wiki/Gibbs_free_energy)
* [Kullback-Leibler Divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)
* [Lagrange Multipliers](https://en.wikipedia.org/wiki/Lagrange_multiplier)
* [Stationary Distribution](https://en.wikipedia.org/wiki/Stationary_distribution)
* [Stationary Ergodic Process](https://en.wikipedia.org/wiki/Stationary_ergodic_process)
* [Ergodic Process](https://en.wikipedia.org/wiki/Stationary_ergodic_process)
* [Detailed Balance](https://en.wikipedia.org/wiki/Detailed_balance)
* [Complexity and Criticality by K. Christensen and N. Moloney](https://github.com/abetusk/papers/blob/release/books/Complexity-and-Criticality-Advanced-Physics-Texts-.pdf)

###### 2023-11-12
