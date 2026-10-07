# Categorise head circumference-for-age z-scores into head circumference-for-age strata

Categorise head circumference-for-age z-scores into head
circumference-for-age strata

## Usage

``` r
categorise_headsize(hcaz)
```

## Arguments

- hcaz:

  A numeric vector of length one or more containing head
  circumference-for-age z-scores (HCAZs).

## Value

An object of class factor with the same length as `hcaz`, containing
head circumference-for-age classifications. Its levels are
`c("microcephaly_severe", "microcephaly", "normal_headcirc", "macrocephaly", "macrocephaly_severe")`.
By default, gigs will inform you this object contains unused factor
levels. You can change this behaviour using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for head size categories are:

|                           |                         |                     |
|---------------------------|-------------------------|---------------------|
| **Category**              | **Factor level**        | **Z-score bounds**  |
| Severe microcephaly       | `"microcephaly_severe"` | `hcaz` =\< -3       |
| Microcephaly              | `"microcephaly"`        | -3 \< `hcaz` =\< -2 |
| Normal head circumference | `"normal_headcirc"`     | `abs(hcaz)` \< 2    |
| Macrocephaly              | `"macrocephaly"`        | `hcaz` \>= 2        |
| Severe macrocephaly       | `"macrocephaly_severe"` | `hcaz` \>= 3        |

## References

Victora CG, Schuler-Faccini L, Matijasevich A, Ribeiro E, Pessoa A,
Barros FC. **Microcephaly in Brazil: how to interpret reported
numbers?** *The Lancet* 2016, *387(10019):621-624*
[doi:10.1016/S0140-6736(16)00273-7](https://doi.org/10.1016/S0140-6736%2816%2900273-7)

Accogli A, Geraldo AF, Piccolo G, Riva A, Scala M, Balagura G, et al.
**Diagnostic Approach to Macrocephaly in Children**. *Frontiers in
Paediatrics* 2022, *9:794069*
[doi:10.3389/fped.2021.794069](https://doi.org/10.3389/fped.2021.794069)

## Examples

``` r
hcaz <- c(-6.5, -3.5, -2.5, 0, 2.5, 3.5)
categorise_headsize(hcaz)
#> [1] microcephaly_severe microcephaly_severe microcephaly       
#> [4] normal_headcirc     macrocephaly        macrocephaly_severe
#> 5 Levels: microcephaly_severe microcephaly normal_headcirc ... macrocephaly_severe
```
