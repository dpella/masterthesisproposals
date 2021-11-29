# Typed representation of datasets for Differential Privacy systems

This thesis will be carried out at [DPella AB](www.dpella.io), Kungsgatan 11 - 6th floor, 41119
Gothenburg.

- DPella AB supervisor: Marco Gaboardi
- Chalmers supervisor: Prof. Alejandro Russo
- Possible examiner: Prof. David Sands

Skills required to complete the thesis:
- Knowledge about Haskell programming language
- Type-level programming concepts like type-families, type classes, data kinds, and type
  constraints.
- Experience with designing domain specific languages

## Differential Privacy

[Differential privacy](https://link.springer.com/chapter/10.1007/11681878_14)
(DP) is emerging as a viable solution to release statistical information about
the population without compromising data subjects' privacy. A standard way to
achieve DP is by adding some statistical noise to the result of a data analysis.
If the noise is carefully calibrated, it provides *privacy* protection for the
individuals contributing their data.

## Calibrated noise

A standard way to achieve DP is adding some carefully calibrated noise to the
result of a query. To protect all the different ways in which an individual's
data can affect the result of a query, the noise needs to be calibrated to the
maximal change that the result of the query can have when changing an
individual's data. This is formalized through the notion of **sensitivity**. The
sensitivity gives a measure of the amount of noise needed to protect one
individual's data.

## Range of possible values for columns

One way to approximate the sensitivity of a query is by understanding the range
of possible value that a data in a table column might have. For instance,
consider the table

| name | allergic |
| ---- | ------- |
| Alejandro | 1 |
| Marco     | 0 |
| Elisabet  | 1 |

If the query consists on *counting the number of alergic people*, which in this
case returns a count of `2`, has sensitivity **1**. Why 1? Observe that the
range of the column `allergic` (computed by the distance between its extremes
values) is ```math | 1 - 0 | = 1 ```. So, if we take out any row of the dataset
and re-run the query, then we should expect a different in the result of almost
`1`! For instance, running the same query in the following table given a count
of `1` (instead of `2` as it was before).

| name | allergic |
| ---- | ------- |
| Alejandro | 1 |
| Marco     | 0 |

The take home message is that if the range of columns are known, it is possible
to quickly compute the sensitivity of certain queries when using DP techniques.

# Goal of the thesis

The overall goal of this thesis is to explore typed representation for tables,
where *the type information for each column not only says the kind of stored
data (e.g., bool, int), but also the range of its values*. We will use the
programming language Haskell in this work. To give an example, one could be
represent the table shown above as a data type definition, where a table is
simply a list of rows.

```haskell

data Row = MkRow {
      name    :: String
    , alergic :: Int
    }

type Table = [Row]
```

What we would like is to represent also the possible options for each value at
the type level. For instance,

```haskell
data Row = MkRow {
      name    :: String
    , alergic :: EnumVals [0,1] Int
    }

type Table = [Row]
```

Where the type `EnumVals` uses a type-level list to describe the possible values
of type `Int` for the field `alergic`.

While this example looks simple, there are two main challenges aspects about
this work.

## Type-level decimal numbers

While enumerating the possible value of booleans, and integers is somehow
feasible, representing decimal numbers is challenging. For instance, an interval
of blood sugar measurements ranges typically [from 4 to 7 mmol/L with one
decimal
precision](https://www.diabetes.co.uk/diabetes_care/blood-sugar-level-ranges.html),
which gives a total 40 possible values. If we want to consider measurements of
blood sugar with two decimal precision, then we will have 400 possible values!
Doing an enumeration at the type-level is possible but it will significantly
load the type-system process.

Instead, this work consists on exploring compact type-level representation for
decimal intervals with a fixed precision at the type-level. Having conceived a
type-level representation for decimals, the thesis will provide mechanisms to
generate, at term level, all the possible values of a given range.

## Integration into DPella's data model

Once type-level interval are conceived, the thesis will incorporate the
type-level ranges on DPella's backend by using advanced generic programming
techniques like [n-ary products](https://dl.acm.org/doi/10.1145/2633628.2633634).
