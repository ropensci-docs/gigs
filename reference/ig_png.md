# INTERGROWTH-21^(st) Postnatal Growth Standards growth curve data

A set of nested lists containing tables with reference values at
different z-scores/centiles for valid post-menstrual ages. The list is
ordered by acronym first, then by sex, and finally by z-score/centile.

## Source

[INTERGROWTH-21^(st) Postnatal Growth of Preterm
Infants](https://intergrowth21.tghn.org/postnatal-growth-preterm-infants/)

## References

Villar J, Giuliani F, Bhutta ZA, Bertino E, Ohuma EO, Ismail LC et al.
**Postnatal growth standards for preterm infants: the Preterm Postnatal
Follow-up Study of the INTERGROWTH-21st Project.** *Lancet Glob Health*
2015, *3(11):e681-e691.*
[doi:10.1016/S2214-109X(15)00163-1](https://doi.org/10.1016/S2214-109X%2815%2900163-1)

## Examples

``` r
names(gigs::ig_png)
#> [1] "wfa"  "lfa"  "hcfa" "wfl" 
head(gigs::ig_png$wfa$male$zscores)
#>   pma_weeks SD3neg SD2neg SD1neg  SD0  SD1  SD2  SD3
#> 1        27   0.36   0.44   0.55 0.67 0.83 1.02 1.25
#> 2        28   0.46   0.56   0.68 0.83 1.01 1.23 1.50
#> 3        29   0.57   0.69   0.83 1.00 1.21 1.46 1.76
#> 4        30   0.69   0.83   0.99 1.19 1.42 1.70 2.04
#> 5        31   0.83   0.98   1.17 1.39 1.65 1.96 2.33
#> 6        32   0.97   1.14   1.35 1.60 1.89 2.23 2.63
```
