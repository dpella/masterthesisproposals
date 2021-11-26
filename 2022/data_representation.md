# Typed representation of datasets for Differential Privacy systems

## Differential Privacy

[Differential privacy](https://link.springer.com/chapter/10.1007/11681878_14)
(DP) is emerging as a viable solution to release statistical information about
the population without compromising data subjects' privacy.
[//]:
A standard way to achieve DP is by adding some statistical noise to
the result of a data analysis.
[//]:
If the noise is carefully calibrated, it provides *privacy* protection for the
individuals contributing their data.

## Calibrated noise

A standard way to achieve DP is adding some carefully calibrated noise to the
result of a query.
[//]:
To protect all the different ways in which an individual's data can affect the
result of a query, the noise needs to be calibrated to the maximal change that
the result of the query can have when changing an individual's data. This is
formalized through the notion of **sensitivity**.
[//]:
The sensitivity gives a measure of the amount of noise needed to protect one
individual's data.

## Range of possible values for columns

One way to approximate the sensitivity of a query is by understanding the range
of possible value that a data in a table column might have.
[//]:
For instance, consider the table

| Name | Alergic |
| ---- | ------- |
| Alejandro | 1 |
| Marco     | 0 |
| Elisabet  | 1 |




## General representation of tables as n-ary product


## Capturing columns ranges
