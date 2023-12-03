## Considerations and thoughts about Lab n.9
This **laboratory** required to solve a problem using the minimum number of fitness calls.
I want to say that I could not reach the results that I hoped for, and in the following lines, I will explain all - from the *reasoning* to *my expected results*.

For this laboratory, I turned to **Genetic Algorithm** because they handle *bit strings*. Additionally I was inspired by *one-max.ipynb* code made by prof. Squillero (you can find it in folder *squillero/computational-intelligence/2022-23/*, in its repository) because it deals with a similar problem.

Initially, I pondered the right trade-off between a low number of fitness calls and high fitness value:
- to have a low number of fitness calls
    - we need to have low individuals to evaluate, thus increasing the number of generations
- to have the best fitness value:
    - we need to obtain different individuals and to tweak them. Moreover we need to know when to do exploration and when to do exploitation -> it depends by the generation. We can do this making a comparison between the previous generation and the current one in terms of average fitness, best fitness values, differences between maximum and minimum fitness values etc.

As first thing I used professor's code to test its performances with the problem on several instances (I adapted opportunately the code it to this specific task): it obtained very good performances for instance 1 (it found the individual with fitness 1.00), then for the other instances it worked less well.

In order to solve this problem I recurred to **parallel methods** in order to deal with inviduals divided in different groups: in this manner they could grow and then interact in base of the adopted method.

In first instance I adopted the **segregation model** that consists to divide the population in different sub-groups and then to unify them after some generations. I implemented this model and I tried to optimize it, but I did not obtain the desired results:
- for *instance 1* it obtained an individual with fitness around 0.57 after some hundreds of generations (from 317 to 685), calling 200k times the fitness function
- for *instance 2* it obtained an individual with fitness around 0.55 after a few hundreds of generations (around 300), calling 100k times the fitness function
- for *instance 5* it obtained an individual with fitness around 0.41 after some hundreds of generations (around 600), calling more than 200k times the fitness function
- for *instance 10* it obtained an individual with fitness around 0.34 after some hundreds of generations (around 500), calling around 200k times the fitness function.

This model performs better than the one that works with the whole population with instance 2 and instance 5, then it has similar behaviour with instance 10 and it is worse for instance 1 as I said.

I tried to *optimize* this model recurring to:
- new mechanism to pick the parent for the generation of a new individual, like a roulette wheel,
- techniques to select the individuals for the next generation, like *elitism*, *genetical GA* or both combined together,
- self-adaptation for the mutation probability (I make a comparison between the best of the previous generation of that niche to the best of the current generation in order to know if it is more suitable to do exploration or exploitation) (*prv_fitness[index] * 11/10 >= tmp_fitness[index] -> True (exploration), False (exploration)*),
- generation of niches by collecting individuals by similar fitness (I rejected the idea of collecting them by genotype because it could let me to niches that converge immediately and that do not find the best individual),
- new recombination method like *uniform crossover*.
But they let me to slightly good improvements, nothing really special.

So I thought to try another model: **island model**. Unfortunately the performances did not grow really well.

Then, after seeing the performances of professor's code on *instance 1 problem* I tried to use a number of niches (but also of migrants) proportional to the instance (for example for instance 1 problem it seems that the model with one niche works better than the one with fixed number of niches/islands), but this try did not go well.

So **my conclusion** is that I am committed and I spent effort to do this task (as you can read). My expected results were influenced by colleagues performances. For this porpose I ASK TO YOU to give me a sincere feedback in order that I can improve my skill and in order to see this laboratory from another point of view.

P.S. sorry for my bad english