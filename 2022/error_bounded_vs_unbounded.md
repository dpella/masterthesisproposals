# Testing data-dependent accuracy for unbounded notions of Differential Privacy

This thesis will be carried out at [DPella AB](www.dpella.io), Kungsgatan 11 -
6th floor, 41119 Gothenburg.

- DPella AB supervisor: Marco Gaboardi
- Chalmers supervisor: Prof. Alejandro Russo
- Possible examiner: Prof. David Sands

Skills required to complete the thesis:
- Haskell programming
- Good skills on mathematics and basic knowledge of probability theory
- Good knowledge of QuickCheck testing framework

## Differential Privacy

[Differential privacy](https://link.springer.com/chapter/10.1007/11681878_14)
(DP) is emerging as a viable solution to release statistical information about
the population without compromising data subjects' privacy. A standard way to
achieve DP is by adding some statistical noise to the result of a data analysis.
If the noise is carefully calibrated, it provides *privacy* protection for the
individuals contributing their data.

## Bounded vs. Unbounded notions of Differential Privacy

There are two kind of definitions about how to formulate differential privacy
guarantees: unbound and bounded -- see the paper [No Free Lunch in Data
Privacy](http://www.cse.psu.edu/~duk17/papers/nflprivacy.pdf). Intuitively, and
for the purpose of this work, we can simplify these two notions as follows.

- *Unbounded DP notion*: the amount of rows of a dataset is considered sensitive
  information.
- *Bounded DP notion*: the amount of rows of a dataset is considered public.

### Unbounded DP

The unbounded notion entails that, if someone wants to know the amount of rows
of a given dataset, then a *differentially private query* needs to be performed
to obtain such information. For instance, imagine that we want to know the
amount of people at our company that has some decease:

```haskell
sickEmployees dataset = do
    dataset' <- filter (\employee -> sick employee == True) dataset
    noise_n <- lenght_with_DP dataset'
    return noise_n
```

The program above takes a `dataset`, and generates another dataset `dataset'`
with only the employees with a decease. After that, we count the length of that
dataset using differential privacy by calling `length_with_DP dataset'` -- so
the privacy of the individual is protected. The noise here is needed for cases
where the amount of rows is "small" and what is considered small might vary
according to the situation. Nevertheless, to illustrate this point, we can
consider the extreme case where `dataset` consists of employees with a given
name Alejandro and lastname Russo. In this case, knowing the exact number might
give you a hint if someone is Alejandro Russo is sick.

## Bounded DP

 XX
