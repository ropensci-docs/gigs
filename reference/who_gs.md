# WHO Child Growth Standards growth curve data

A set of nested lists containing tables with reference values at
different z-scores/centiles for valid x values (usually age in days,
also length or height in cm for weight-for-length (`wfl`) and
weight-for-height (`wfh`) standards, respectively). The list is ordered
by acronym first, then by sex and finally by z-score/centile.

## Source

[WHO Child Growth
Standards](https://www.who.int/tools/child-growth-standards/standards)

## References

de Onis M, Garza C, Victora CG, Onyango AW, Frongillo EA, Martines J.
**The WHO Multicentre Growth Reference Study: planning, study design,
and methodology** *Food Nutr Bull.* 2004, **25(1 Suppl):S15-26.**
[doi:10.1177/15648265040251s104](https://doi.org/10.1177/15648265040251s104)

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
names(gigs::who_gs)
#> [1] "wfa"  "bfa"  "lhfa" "wfl"  "wfh"  "hcfa" "acfa" "ssfa" "tsfa"
head(gigs::who_gs$wfa$male$zscores)
#>   age_days SD4neg SD3neg SD2neg SD1neg   SD0   SD1   SD2   SD3   SD4
#> 1        0  1.701  2.080  2.459  2.881 3.346 3.859 4.419 5.031 5.642
#> 2        1  1.692  2.065  2.437  2.854 3.317 3.830 4.394 5.013 5.633
#> 3        2  1.707  2.080  2.454  2.872 3.337 3.852 4.421 5.045 5.669
#> 4        3  1.725  2.100  2.475  2.895 3.363 3.881 4.453 5.083 5.712
#> 5        4  1.745  2.122  2.499  2.921 3.392 3.913 4.490 5.124 5.758
#> 6        5  1.767  2.146  2.525  2.949 3.422 3.947 4.528 5.167 5.806
```
