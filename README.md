# cyclic_executive_scheduling
An explanation of the scheduling of periodic tasks using time triggered cyclic executive along with a mixed integer linear programming formulation which solves this problem

## Definition and particulars of cyclic executive scheduling

### Notation

$\tau_i$ : Periodic task $i$

$C_i, T_i, D_i$: Computation time, Period, and Deadline of task $i$ in unit time.

$P$ hyperperiod which equations to $\text{LCM}(\{T_i\}_{i=0}^{n-1} )$ where $n$ is the total number of tasks in periodic taskset $\Pi$

$f$ is defined as the frame size

$\phi_i$ is defined as the phase of periodic task $i$

### Scheduling constraints

In cyclic executive scheduling, the variables that the designer can influence are $f$ (frame size), $\phi_i \forall \tau_i\in \Pi$ (the phases of all tasks), and the frames in which tasks are scheduled. 

Following constraints need to be adhered:

\begin{equation}
f\leq T_i \; \qquad\tau_i \in \Pi
\end{equation}

\begin{equation}
f\geq C_i \; \qquad\tau_i \in \Pi
\end{equation}

\begin{equation}
P/f \in \mathbb{N}
\end{equation}

**specification of frame based scheduling constraints is pending**


## MILP formulation for scheduling

**Documentation is pending**



