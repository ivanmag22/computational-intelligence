# Laboratory n.10 - Reinforcement Learning in Tic Tac Toe 

Made by
- Ivan Magistro Contenta,
- s314356, 
- [s314356@studenti.polito.it](s314356@studenti.polito.it)

## Introduction
This **laboratory** required to implement a Reinforcement Learning agent for Tic Tac Toe game.

## Rewards
I have only three rewards for the episode:
- +1 for the victory of the agent
- -1 for the loss of the agent
- 0 otherwise (not the end or draw)

I've considered also the number of moves done, but I thought that it could bring to maximize or minimize the number of moves and not to win the game.

## Strategies
After studying some material regarding Reinforcement Learning, I decided to introduce two different strategies based on model-free Reinforcement Learning:
- **Monte Carlo Approach**: it learns directly from episodes of experience, in particular from complete episodes.
- **Q-Learning**: it is an *off-policy* algorithm, which means that, while learning a so-called target policy, it uses a so-called behaviour policy to select actions. In this case Quality function table stores useful value to understand what action pick (if we do not act randomly).
I used two policy:
    - *ϵ-greedy policy*: policy that chooses the best action (i.e. the action associated with the highest value) with probability 1−ϵ ∈ [0,1] and a random action with probability ϵ.
    - *softmax policy*: it is a way to select actions based on the Q-values (the expected future rewards) of each action in a given state.

## Results
In test phase I collect the results of each approach like the percentages of victories, losses and draws between the final player that has the informations by Reinforcement Learning method and a random player.

I ran 20k episodes for training and different number of episodes for testing for each method.

- Using the **Monte Carlo Approach** I obtained
    - Avg Wins: 58.45576208901873 %
    - Avg Draws: 12.69550780020847 %
    - Avg Losses: 28.848730110772816 %
- Using the **Q-Learning with** ***ϵ-greedy policy*** I obtained
    - Avg Wins: 86.59067572599369 %
    - Avg Draws: 3.8217688205956586 %
    - Avg Losses: 9.58755545341066 %
- Using the **Q-Learning with** ***softmax policy*** I obtained
    - Avg Wins: 78.84648872334519 %
    - Avg Draws: 6.406189919541619 %
    - Avg Losses: 14.747321357113183 %

Moreover I observed that the percentages of victory, loss and draw do not change if we use different number of games (as you can see in the code).

The final result depends only on the number of games done during training. Indeed with 20k episodes for training I obtain good results, while for a reduced number the percentages decrease (for example from 88% of wins with 20k episodes of training to 60% with 5k episodes of training).

## Conclusions
So **my conclusion** is that the agent learns better using *Q-Learning method* than using *Monte Carlo method*. I think that it depends a lot on the policy that the agent follows, while acting randomly is not always good.