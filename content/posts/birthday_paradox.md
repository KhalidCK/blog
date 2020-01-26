---
title: "Birthday Paradox ?"
date: 2018-05-08T10:14:00+02:00
draft: true
---

Lately I have stumbled on the birthday paradox. At first glace it does not seems more than some probability fantasy, however this problem is relevant as a proxy to a number of real world case : for example in security the [birthday attack](https://en.wikipedia.org/wiki/Birthday_attack)

<!--more-->

## A story ...

There are tons of solvers on internet that will provide the answer to this problem, however, here I'm interested to solve and understand the general idea of it. I'll **resonate** through it using python.

A concrete example is usually a good way to go, let's say that we're in a room of 23 peoples and I'm betting with my friends to know how many people here are sharing the same birthday.

To make it simpler I'll say that a year always have 365 days (I don't consider leap years).

I'll build the example with python and [Faker](https://github.com/stympy/faker) library.

```python
from faker import Faker
fake = Faker('fr_FR')
```

I'll also load some useful library to simulate random choice and manipulate probabilistic concept

```python
import random
from itertools import combinations
```

Here our _people_ :

```python
peoples = [fake.name() for nb in range(0,23)]
```

```python
len(peoples)
```

    23

```python
peoples[:5]
```

    ['Marcel Maurice',
     'Lucas Dupuy',
     'Bertrand Le Roux-Guillot',
     'Agnès-Joséphine Antoine',
     'Gilles Delmas']

I'm in the room, I look around and try to compare my birthday to the 22 other people.

Knowing that there is 1/365 that I share my birthday date with, so there is something like 23 different possible combinations ... **hold on**

We want to figure out how many people **in the room** are sharing their birthday not only **me**, outch I was a little self-centered here.

We have to consider all the combination of people in the room.
Let's model it with Python :

```python
combination = list(combinations(peoples,2))
```

A quick look at samples :

```python
for peopleA,peopleB in random.sample(combination,5):
    print(f'{peopleA} **compare with** with {peopleB}')
    print('----')
```

    Gilles Delmas **compare with** with Auguste Caron
    ----
    Audrey Henry **compare with** with Marcel Lemaitre
    ----
    Charlotte Lejeune du Guillon **compare with** with Matthieu de la Poulain
    ----
    Bertrand Le Roux-Guillot **compare with** with Bertrand Potier
    ----
    Matthieu de la Poulain **compare with** with Roger-Raymond Lemoine
    ----

and this list contains :

```python
len(combination)
```

    253

Fair enough _a little_ more than 23.

The question is :

> In this room of 23 people, what the chance is that there are at least two persons that have the same birthday.

This question is quite complex and hard to think about. However the opposite question is easier to understand

> What is the chance that everyone is different ?

If we answer this question, we can answer the initial one (_1 - opposite question_)

### Work out the probabilities.

Loosely a probability can be defined as :

```
The number of possibilities that meet  a condition

divided by

The number of equally likely possibilities
```

In our case the probability of two birthdays to _collide_ is 1/365.

So we also know the probably to **not** collide.

```python
proba_not_collide = 1 - 1/365
round(proba_not_collide,3)
```

    0.997

As expected it is an unlikely event .

Just to be sure let's continue our investigation ...

### Instincts

We have independent probability, so we can use the same old strategy that we were taught at school in this case.

Meaning that we divide ... or mutliply or ... Ok I have to face it, I don't remember.

I'll figure it out with some examples

![tree coin proba](/img/birthday/proba_tree_coin.png)

So it seems that rather than multiply or divide we're going for an exponent change !

So our probability that there is no collision in birthday is :

    (364/365)^23

```python
proba_not_collide**253
```

    0.4995228459634194

And therefore the response to our initial question

```python
1 - 0.4995
```

    0.5005

The result is kind of counter-intuitive, you have 1/2 chance to have two person with the same birthday in a room of 23 people.

There is probably two main reason for our initial misleading intuition :

- You have to think about all of combination that are **not** you.
- Thinking in exponent is usually not natural for human being, we are more used to linear like addition, multiplying ...

To go further :

- [Better explained](https://betterexplained.com/articles/understanding-the-birthday-paradox/)
- [Wikipedia](https://en.wikipedia.org/wiki/Birthday_problem)
