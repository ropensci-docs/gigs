# Categorise weight-for-age z-scores into weight-for-age strata

Categorise weight-for-age z-scores into weight-for-age strata

## Usage

``` r
categorise_wfa(waz, outliers = FALSE)
```

## Arguments

- waz:

  A numeric vector of length one or more containing weight-for-age
  z-scores (WAZs).

- outliers:

  A single `TRUE` or `FALSE` value specifying whether implausible
  z-score thresholds should be applied. Default = `FALSE`.

## Value

An object of class factor with the same length as `waz`, containing
weight-for-age classifications. Its levels are
`c("underweight_severe", "underweight", "normal", "overweight")` if
`outliers = FALSE` (the default), else
`c("underweight_severe", "underweight", "normal", "overweight", "outlier")`.
By default, gigs will inform you this object contains unused factor
levels. You can change this behaviour using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for weight-for-age categories are:

|                      |                        |                           |
|----------------------|------------------------|---------------------------|
| **Category**         | **Factor level**       | **Z-score bounds**        |
| Severely underweight | `"underweight_severe"` | `waz` =\< -3              |
| Underweight          | `"underweight"`        | -3 \< `waz` =\< -2        |
| Normal weight        | `"normal_weight"`      | `abs(waz)` \< 2           |
| Overweight           | `"overweight"`         | `waz` \>= 2               |
| Outlier              | `"outlier"`            | `waz` \< -6 or `waz` \> 5 |

## References

**'Implausible z-score values'** *in* World Health Organization (ed.)
*Recommendations for data collection, analysis and reporting on
anthropometric indicators in children under 5 years old*. Geneva: World
Health Organization and the United Nations Children's Fund UNICEF,
(2019). pp. 64-65.

**'Percentage of children stunted, wasted, and underweight, and mean
z-scores for stunting, wasting and underweight'** *in* *Guide to DHS
Statistics DHS-7* Rockville, Maryland, USA: ICF (2020). pp. 431-435.
<https://dhsprogram.com/data/Guide-to-DHS-Statistics/Nutritional_Status.htm>

## Examples

``` r
waz <- c(-6.5, -3.5, -2.5, 0, 2.5, 3.5)
categorise_wfa(waz, outliers = FALSE)
#> [1] underweight_severe underweight_severe underweight        normal_weight     
#> [5] overweight         overweight        
#> Levels: underweight_severe underweight normal_weight overweight
categorise_wfa(waz, outliers = TRUE)
#> [1] outlier            underweight_severe underweight        normal_weight     
#> [5] overweight         overweight        
#> Levels: underweight_severe underweight normal_weight overweight outlier
```
