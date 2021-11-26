# Typed representation of datasets for Differential Privacy systems

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

| Name | Alergic |
| ---- | ------- |
| Alejandro | 1 |
| Marco     | 0 |
| Elisabet  | 1 |

If the query consists on *counting the number of alergic people*, which in this
case returns a count of `2`, has sensitivity **1**. Why 1? Observe that the
range of the column `Alergic` (computed by the distance between its extremes
values) is ```math | 1 - 0 | = 1 ```. So, if we take out any row of the dataset
and re-run the query, then we should expect a different in the result of almost
`1`! For instance, running the same query in the following table given a count
of `1` (instead of `2` as it was before).

| Name | Alergic |
| ---- | ------- |
| Alejandro | 1 |
| Marco     | 0 |


## General representation of tables as n-ary product


## Capturing columns ranges
