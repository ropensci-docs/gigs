# WHO Child Growth Standards LMS coefficients

A set of nested lists containing tables with LMS values for each sex in
different combinations of age/length-height/BMI. The list is ordered by
acronym first, then by sex.

## Source

[WHO Child Growth
Standards](https://www.who.int/tools/child-growth-standards/standards)

## References

World Health Organisation. **WHO child growth standards:
length/height-for-age, weight-for-age, weight-for-length,
weight-for-height and body mass index-for-age: methods and
development.** *Technical report, WHO, Geneva*, 2006.

World Health Organisation. **WHO child growth standards: head
circumference-for-age, arm circumference-for-age, triceps
skinfold-for-age and subscapular skinfold-for-age: methods and
development.** *Technical report, WHO, Geneva*, 2007.

## Examples

``` r
names(gigs::who_gs_coeffs)
#> [1] "wfa"  "bfa"  "lhfa" "wfl"  "wfh"  "hcfa" "acfa" "ssfa" "tsfa"
head(gigs::who_gs_coeffs$lhfa$male)
#>   age_days L       M       S
#> 1        0 1 49.8842 0.03795
#> 2        1 1 50.0601 0.03785
#> 3        2 1 50.2359 0.03775
#> 4        3 1 50.4118 0.03764
#> 5        4 1 50.5876 0.03754
#> 6        5 1 50.7635 0.03744
```
