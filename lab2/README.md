# Laboratory n.2 Nim game

Made by
- Ivan Magistro Contenta,
- s314356, 
- [s314356@studenti.polito.it](s314356@studenti.polito.it)

## Introduction

I was inspired by the code _rastrigin.ipynb_ made by prof. Squillero to understand the ES-Strategies and I readapt to this problem. 

I have implemented the Evolutionary Strategy in the following way: in order to optimize with the epochs the performances of the simple function _weighted()_, we have to train the individuals (obtained mutating the parent(s)) making some matches with the other opponents (_optimal()_, *pure_random()*, _gabriele()_, recurring to ***play_games()***) or with the _optimal_ opponent (recurring to ***play_games_with_optimal()***). So from each of their matches we obtain the accuracy of victory of the individuals, that represents their fitness, and we check if the best individual among them is better than the best one found until that moment. Then we repeat these steps until we reach the number of epochs.

At the end we try our model against the _optimal_ opponent to see how it is efficient in a certain number of matches.

## How does it work?

The **evolutionary strategy** is *self-adaptive*, indeed it modifies the mutation step σ following the "one-out-of-five" rule.

The *evolutionary approach* is described by **evolutionary functions**: as I said, we pick each individual and let it play with opponent(s) and then improve their weights. We run all these instructions for a slightly small number of epochs (1_000 // λ).
There are **different implementations**:
- *evolutionary_plus()* for (1 + λ)-ES
- *evolutionary_comma()* for (1, λ)-ES
- *evolutionary_plus_mu()* for (µ + λ)-ES
- *evolutionary_comma_mu()* for (µ, λ)-ES

To follow an *evolutionary strategy* approach, we have to modify (or better improve) the individuals during the epochs. For this purpose I have followed prof. Squillero's intuition of ***rules*** (condition + action) with weights: I interpreted these weights as probabilities, indeed I imposed that the sum of the weights must be 1.
I implemented a particular class, called **NimGame**, that contains the list of weights, the dictionary of rules (the key is an integer, the value is a function *r**x**()*) and the accuracy of the individual that must be set after the matches.
The implemented rules are the following:
- ***r0()***: it takes objects only from even rows
- ***r1()***: it takes objects of a whole row (if k is set the number of objects must be less or equal to k)
- ***r2()***: it takes objects only one object from a row
- ***r3()***: it takes a random number objects from the last available row (respecting k if it is set and the number of objects of that row)

The _weighted()_ function must take the "heaviest" rule (that is activated to be taken).
It is wrapped into a function (*es_wrapper()*) that gives it the weights and then, when _weighted()_ is called, it considers the current configuration and it does the most promising move. 

## Some statistics

With *(1_000 // λ) epochs* (with λ=20 -> 50 epochs) I obtained:
- **(1 + λ)-ES**
    + playing with all three players (optimal, pure_random, gabriele)
        * ES-accuracy = 68.89 %
        * accuracy obtained by 30 matches with pure_random = 96.97 %
    + playing with optimal
        * ES-accuracy = 40 %
        * accuracy obtained by 30 matches with pure_random = 98.89 %
- **(1, λ)-ES**
    + playing with all three players (optimal, pure_random, gabriele)
        * ES-accuracy = 69.63%
        * accuracy obtained by 30 matches with pure_random = 100%
    + playing with optimal
        * ES-accuracy = 48.89 %
        * accuracy obtained by 30 matches with pure_random = 98.89 %