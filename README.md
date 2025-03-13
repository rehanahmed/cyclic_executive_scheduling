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

$$f\leq T_i \; \qquad\tau_i \in \Pi$$

$$f\geq C_i \; \qquad\tau_i \in \Pi$$

$$P/f \in \mathbb{N}$$

$$2\cdot f - \text{gcd}(T_i, f)\leq D_i  $$

The first equation ensures that frame size is no greater than than every period. The second equation ensures that the frame size is no less than every computation time. The third constraint ensures that the hyperperiod has integer number of frames. The fourth constraint ensures that between each arrival and deadline of a task, there is at least one full frame. The specified constraints only specify the constraints on framesizes. Following constraints need to be satisfied for scheduling

- A task instance can be executed in frame $F_i$ iff the arrival of the task instance is not after the staring time of $F_i$.
- A task instance can be executed in frame $F_i$ iff the deadline of the task instance is not before the ending time of $F_i$.
- Tasks instances are executed non-preemptively.
- Execution of a given task instance needs to complete in a single frame. In other words, the execution cannot be split across two or more frames.
- Most importantly, each task instance needs to be executed.

For scheduling, we can define the following constraints.

Let $f_{ij}$ denote the frame index where the $j^\text{th}$ instance of periodic task $i$ is executed.

$$\displaystyle\sum_{i|f_{i,j}=k} C_i\leq f\qquad \forall\; 0\leq k\leq \frac{P}{f} -1$$

$$\phi_i \leq f_{ij}\cdot f -j\cdot T_i \qquad \forall \tau_i \in \Pi,\; 0\leq j\leq \frac{P}{T_i}-1$$

$$j\cdot T_i + \phi_i + D_i\geq (f_{ij}+1)\cdot f\qquad \forall \tau_i \in \Pi,\; 0\leq j\leq \frac{P}{T_i}-1$$

First constraint ensures that we do not over-fill any frame. Second constraint ensures that the frame assigned for the scheduling of task any instance is starting no earlier than the arrival time of the task instance. Third constraint ensures that the frame assigned for the scheduling of task any instance is ending no later than the deadline of the task instance. Note that the first constraint is not linear, since the decision variable $f_{i,j}$ is part of the summation condition. 





**specification of frame based scheduling constraints is pending**


## MILP formulation for scheduling
In this formulation, we will chose to use binary variables for task to frame assignment. This makes the frame capacity constraint easy to model. The frame assignment constraints will need to be adapted in accordance with the binary variable. The frame size is not treated as a variable. The MILP can be executed iteratively for the frame sizes which satisfy the four frame size constraints.

Following parameters are fixed:

n: Total number of tasks in periodic taskset $Pi$. i.e. $n=|\Pi|$

F: Total number of frames. i.e. $F=P/f$

### Variables

$F_{it}$: Binary variables which is *True* iff task with index $t$ is executed in frame with index $i$

$\phi_i$: Integer variable which defines the phase of task with index $i$



### Constraints

$$ \sum_{0 \leq t < n} F_{ij}\leq f \qquad \forall 0 \leq I < F $$

$$ \sum_{0\leq j\leq i} F_{jt}\leq \frac{i\cdot f -\phi_t}{T_t} +1 \qquad \forall  0 \leq i < F,  0\leq t < n $$

$$ \sum_{0\leq j\leq i} F_{jt}\geq \frac{(i+2)\cdot f -\phi_t -D_t}{T_t} \qquad \forall  0 \leq i < F,  0 \leq t< n $$

The first constraint guarantees that we do not over-fill any frame. The second and third constraints guarantee that each task instance is scheduled in a frame that start no earlier than the arrival time, and a frame that ends no later than the deadline.



