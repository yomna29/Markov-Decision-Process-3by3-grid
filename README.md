

# Gridworld MDP Solver using Value Iteration
This repository contains the Python script `MDP.py`, which implements the **Value Iteration algorithm** to find the optimal state values $V^*(s)$ and the optimal policy $\pi^*(s)$ for a simple 3 x 3 Gridworld Markov Decision Process (MDP).

The script is a self-contained solver demonstrating the core concepts of reinforcement learning in a small, probabilistic environment.

##  How It Works
The simulation takes place on a 3 x 3 grid. The solution method is **Value Iteration**, an iterative dynamic programming algorithm based on the **Bellman Optimality Equation**:

The algorithm converges to the optimal values $V^*(s)$ when the change in values (\Delta) between iterations is smaller than the threshold $10^{-4}$. The optimal policy $\pi^*(s)$ is then extracted directly by choosing the action a that maximizes the utility at each state s.

### Probabilistic Transitions
The environment is probabilistic, meaning actions do not always result in the intended movement:

* **Intended Direction**: 80\% probability.
* **Perpendicular Directions**: 10\% probability for each of the two adjacent, perpendicular directions.
* **Wall Collision**: If an action (or a probabilistic slip) would cause a collision with the grid boundary, the agent remains in its current state.


| Constant |	Value |	Description |
| :--- |	:--- |	:--- |
| `gamma` |	0.99 |	The discount factor, valuing immediate rewards slightly more than future rewards. |
| `actions` |	`["Up", "Down", "Left", "Right"]` |	The set of four possible actions. |
| `grid_size` |	3 |	Defines the grid dimensions (3 * 3). |

## Reward Structure
The script tests the algorithm across four different reward structures by varying the reward at the critical top-left state (0, 0).

| State |	Coordinate |	Reward |
| :--- |	:--- |	:--- |
| Top-Right (Terminal) |	(0, 2) |	+10 |
| Other States (Non-Terminal) |	Varies |	-1 (default penalty) |
| Top-Left (Tested) |	(0, 0) |	Tested with: 100, 3, 0, -3 |

The results demonstrate how the optimal policy $\pi^*(s)$ shifts based on the attractiveness of the reward at state (0, 0).

### Running the Script. 
1. Ensure you have Python 3 and NumPy installed.
2. Save the code as `MDP.py`.
3. Execute from the command line:
```bash
python MDP.py

```



The output will display the converged **State Values** and the final **Policy** for each of the four reward configurations.

## Code Structure
### `get_transition_probabilities(state, action)`
Calculates the list of possible resulting states and their probabilities for a given state-action pair, incorporating the 80/10/10 split and wall collision logic.

### `value_iteration(reward, threshold)`
The main solver function that:

1. Initializes state values $V(s)$ and policy $\pi(s)$.
2. Enters a loop to compute $V_{k+1}(s)$ using the Bellman Optimality Equation.
3. Updates the policy $\pi(s)$ by choosing the greedy action.
4. Breaks when the max change $\Delta$ is less than the threshold.

### `display_policy(policy)` 
A utility function to print the optimal policy in a clear, formatted grid.
