# Categorise weight-for-length/height z-scores into wasting strata

Categorise weight-for-length/height z-scores into wasting strata

## Usage

``` r
categorise_wasting(wlz, outliers = FALSE)
```

## Arguments

- wlz:

  A numeric vector of length one or more containing
  weight-for-length/height z-scores (WLZs).

- outliers:

  A single `TRUE` or `FALSE` value specifying whether implausible
  z-score thresholds should be applied. Default = `FALSE`.

## Value

An object of class factor with the same length as `wlz`, containing
wasting classifications. Its levels are
`c("wasting_severe", "wasting", "not_wasting", "overweight")` if
`outliers = FALSE` (the default), else
`c("wasting_severe", "wasting", "not_wasting", "overweight", "outlier")`.
By default, gigs will inform you this object contains unused factor
levels. You can change this behaviour using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for wasting categories are:

|                |                    |                    |
|----------------|--------------------|--------------------|
| **Category**   | **Factor level**   | **Z-score bounds** |
| Severe wasting | `"wasting_severe"` | `wlz` =\< -3       |
| Wasting        | `"wasting"`        | -3 \< `wlz` =\< -2 |
| No wasting     | `"not_wasting"`    | `abs(wlz)` \< 2    |
| Overweight     | `"overweight"`     | `wlz` \>= 2        |
| Outlier        | `"outlier"`        | `abs(wlz)` \> 5    |

## Note

This function assumes that your measurements were taken according to WHO
guidelines, which stipulate that recumbent length should not be measured
after 730 days. Instead, standing height should be used. Implausible
z-score bounds are sourced from the referenced WHO report, and
classification cut-offs from the DHS manual.

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
wlz <- c(-5.5, -3, 0, 3, 5.5)
categorise_wasting(wlz, outliers = FALSE)
#> ! Unused factor levels kept after wasting categorisation: "wasting".
#> [1] wasting_severe wasting_severe not_wasting    overweight     overweight    
#> Levels: wasting_severe wasting not_wasting overweight
categorise_wasting(wlz, outliers = TRUE)
#> ! Unused factor levels kept after wasting categorisation: "wasting".
#> [1] outlier        wasting_severe not_wasting    overweight     outlier       
#> Levels: wasting_severe wasting not_wasting overweight outlier
```
