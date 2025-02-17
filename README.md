# Reinforcement Learning for CartPole: Q-learning and Actor-Critic Approaches
### Overview
This project implements reinforcement learning for the CartPole environment using both Q-learning and Actor-Critic methods. The goal is to balance a pole on a moving cart by taking discrete actions (left or right) based on the environment's state.

- The CartPole environment consists of
  - A cart that can move left or right.
  - A pole attached to the cart, which must be balanced.
  - A reward system that encourages keeping the pole upright.
  - Termination conditions when the pole falls too far or the cart moves out of bounds.

### 1. Actor-Critic Approach
#### Objective
The Actor-Critic method optimizes the agent’s policy by learning both a value function (Critic) and a policy function (Actor). The objective is to minimize the total loss
- $L=L_{Critic}+α⋅L_{Actor}$

where:
- Critic Loss evaluates how well the value function predicts future rewards.
- Actor Loss updates the policy to maximize expected rewards while maintaining sufficient entropy for exploration.

### 2. Q-learning Approach
#### Objective
Q-learning is used to approximate the optimal action-value function. The goal is to minimize the loss:
- $L(θ)=E[(y−Q(s,a;θ))^2]$
where:
- $Q(s,a)=r+γa ′max​Q(s′,a′)$
- The agent updates $Q(s,a)$  to learn the best action-value function over time.

### Implementation Details
This project implements reinforcement learning using Deep Q-Networks (DQN) for Q-learning and Advantage Actor-Critic (A2C) for the Actor-Critic method.

### Constraints
- State Space
  - $𝑆=[x,x',θ,θ']$
    - $x$ : Cart position $(−2.4≤x≤2.4)4
    - $x'$ : Cart velocity (real-valued, no restriction)
    - $𝜃$ : Pole angle $(−12≤θ≤12,−0.21≤θ≤0.21 radians)$
    - $𝜃'$ : Pole angular velocity (real-valued, no restriction)
- Action Space
  - $a∈{0,1}$ (move left or right)
- Termination Conditions
  - $∣x∣>2.4$ ⇒ Terminate Episode
  - $∣θ∣>12$ ⇒ Terminate Episode
  - t≥max_steps⇒Terminate Episode
 
### result
- AC
https://github.com/user-attachments/assets/e940a031-8374-4c28-b5de-45ca6abd5c13
- DQN
https://github.com/user-attachments/assets/4853b476-3cfd-4a62-aee7-a9d4d8837f11




### Comparison of DQN and Actor-Critic (A.C)
To ensure a fair evaluation, both DQN and A.C were initially set up with identical reward functions, network architectures, and other conditions. However, while DQN learned effectively, A.C failed to learn at all. This phenomenon was also observed in a previously submitted assignment.

1. Why DQN Learned Easily
DQN is value-based and learns by approximating the action-value function $Q(s,a)$, making it effective in discrete action spaces.
It works well with simple reward functions and network architectures, making learning more straightforward.
However, DQN struggles in complex environments due to difficulties in accurately estimating Q-values and potential overfitting.
2. Why A.C Initially Failed to Learn
A.C relies on both an Actor (policy network) and a Critic (value function). If the Critic fails to learn an accurate value function, the Actor cannot optimize effectively.
Simple network architectures and reward functions may not provide enough learning signal for the Critic, leading to unstable training.
Unlike DQN, which selects the best action based on Q-values, A.C requires effective exploration and policy updates, which may not work well under simplistic setups.
3. Why A.C Learned After a More Complex Setup
A deeper network structure likely improved the Critic’s value estimation, stabilizing policy learning.
Additional techniques such as entropy regularization or advantage normalization may have enhanced training.
More refined reward signals and exploration strategies helped optimize policy learning.
4. Conclusion
DQN can learn effectively even with simple rewards and architectures but struggles in complex environments.
A.C requires a well-designed setup, as policy-based methods depend heavily on the Critic’s accuracy and exploration mechanisms.
The observed phenomenon aligns with the fact that DQN is more robust in simple settings, while A.C benefits from a more refined structure.
