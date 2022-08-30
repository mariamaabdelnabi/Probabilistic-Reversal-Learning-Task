# Probabilistic-Reversal-Learning-Task
This is a MATLAB code of the probabilistic reversal learning task. Ideally, it includes 2420 simulations, with 20 rounds in each session for 10 sessions. A reversal phase occurs after every 10 rounds. Reward contingencies are 1 and 0.


Reward-seeking tasks that involve learning in a risky environment offer an ideal testbed for investigating the influence of loss aversion on reward maximization, and the PRLT is an exact fit. In a general sense, agents have to decide between binary choice actions – left and right – and are expected to choose the action that is most likely to be associated with a reward. On each trial, the correct action will have a probability p of a positive reward and probability 1-p of no reward, whereas the other action will have a probability 1-p of a reward and p of no reward; such that p>1-p. Traditionally, agents are free to choose between the two actions for several trials and are predicted to establish a preference for the high-rewarding action until they cross a learning criterion, a trial at which the correct action has been chosen t times in a row. Once this criterion is crossed, a reversal occurs. The action that initially had p as the probability of a reward now has 1-p, and vice versa. In other words, the probabilistic reward contingencies are reversed between the right and left actions. Agents experience several reversals before the task ends to measure how quickly they adapt to the switching environment.

Specifically, the task designed in this study presents agents with the same binary choices (i.e., left and right) in each round. The initial design, referred to as the default scenario, consists of 10 sessions of 20 rounds. In each round, an agent decides between left and right, and after the first 10 rounds, a reverse occurs, where reward contingencies are switched. The default scenario follows the traditional 80-20 reward contingencies. Initially, the left action is reinforced 80% of the time, and after 10 rounds, the right action is for another 10 rounds. Once one reversal takes place, a session ends, and another begins. Finally, the reward system in the default scenario includes an r=1 for a reward and an r=0 for no reward. An example of the number of choices and reversals for each number of rounds and sessions is presented in Table 1. As presented in the table, a round controls the number of choices made, and a session controls the reversals in a game.

Table 1: Decisions and reversals made at a different number of rounds and sessions.
Rounds	Choices	Sessions	Reversals
10	20	10	20
50	1000	10	20
100	2000	10	20
500	10000	10	20
10	200	50	100
10	200	100	200
10	200	500	1000

The value-learning process is modelled through the Q-learning algorithm, where there are no states, but only actions. The expected value of an upcoming action Q¬〖¬(a)〗_(t+1) is updated by the prediction error, [r_t-Q_t (a)], that is scaled by a general learning rate α. A lower α implies a gradual, slow update of the action’s Q-value, whereas a higher one implies a heavy dependence on the prediction error. In order to capture and quantify loss aversion, not only does an agent update an action’s Q-value when it receives a reward, but it updates it when it receives a negative or no reward as well. For this, the α is divided between an α_rew for a reward and an α_norew for no reward to have an appropriate measurement for feedback-dependent learning. Accordingly, this model’s Q-values are presented in Equations 2 and 3.

Q_(t+1) (a)=Q_t (a)+α_rew [r_t-Q_t (a)]   at r_t=1	Eq. 2
Q_(t+1) (a)=Q_t (a)+α_norew [r_t-Q_t (a)]   at r_t=0	Eq. 3


Finally, to compute probabilities of action selection at each trial, the model relies on the softmax function and the inverse temperature parameter β. A high β represents an agent tending more towards exploring its choice set, and a low one is an agent that is exploiting known information. The softmax function is presented in Equation 4.

Pr(a)=e^β[Q_t (a)] /e^(β[Q_t (a)+Q_t (a_un )]) 	Eq. 4
Where Q(a_un ) is the Q-value of the unchosen action


The measurement of a reward in this study is a calculated Average Reversal Reward (ARR) for each agent which is calculated at every reversal phase in the session.  Precisely, an agent playing in a session of 20 rounds can have an ARR between 0 and 10, an ARR between 0 and 40 in a 20-round session, and so forth.

Each free parameter has a specific range in the design. Both the α_rew and the α_norew lie within the traditional range of 0 and 1. As for the inverse temperature parameter β, it lies between 0 and 1000 to examine a wide range of possible behavioural patterns in the exploration/exploitation trade-off. Therefore, the set of simulations included all possible combinations of  α_rew,α_norew and β, making it an 11x11x20 combination of 2420 agents.
