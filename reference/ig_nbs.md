# INTERGROWTH-21^(st) Newborn Size Standards (including very preterm) growth curve data

A set of nested lists containing tables with reference values at
different z-scores/centiles for valid gestational ages in days. The list
is ordered by acronym first, then by sex and finally by z-score/centile.

## Source

[INTERGROWTH-21^(st) Newborn Size in Very Preterm
Infants](https://intergrowth21.tghn.org/very-preterm-size-birth/#vp1)  
[INTERGROWTH-21^(st) Newborn Size
Standards](https://intergrowth21.tghn.org/newborn-size-birth/#ns1)  
[INTERGROWTH-21^(st) Newborn Size Standards - Body
Composition](https://www.nature.com/articles/pr201752)

## Note

The tables in this package are combined versions of the tables published
by Villar *et al.* (2014) and Villar *et al.* (2016), so they cover
`168` to `300` days' gestational age. The body composition tables
(`ffmfga`, `bfpfga`, and `fmfga`) cover a smaller gestational age span,
ranging from only `266` to `294` days' (38 to 42 weeks') gestational
age.

## References

Villar J, Cheikh Ismail L, Victora CG, Ohuma EO, Bertino E, Altman DG,
et al. **International standards for newborn weight, length, and head
circumference by gestational age and sex: the Newborn Cross-Sectional
Study of the INTERGROWTH-21st Project.** *Lancet* 2014,
**384(9946):857-68.**
[doi:10.1016/S0140-6736(14)60932-6](https://doi.org/10.1016/S0140-6736%2814%2960932-6)

Villar J, Giuliani F, Fenton TR, Ohuma EO, Ismail LC, Kennedy SH et al.
**INTERGROWTH-21st very preterm size at birth reference charts.**
*Lancet* 2016, **387(10021):844-45.**
[doi:10.1016/S0140-6736(16)00384-6](https://doi.org/10.1016/S0140-6736%2816%2900384-6)

Villar J, Puglia FA, Fenton TR, Ismal LC, Staines-Urias E, Giuliani F,
et al. **Body composition at birth and its relationship with neonatal
anthropometric ratios: the newborn body composition study of the
INTERGROWTH-21st project.** *Pediatric Research* 2017, **82:305-316.**
[doi:10.1038/pr.2017.52](https://doi.org/10.1038/pr.2017.52)

## Examples

``` r
names(gigs::ig_nbs)
#> [1] "wfga"   "lfga"   "hcfga"  "wlrfga" "ffmfga" "bfpfga" "fmfga" 
head(gigs::ig_nbs$wfga$male$zscores)
#>   gest_days SD3neg SD2neg SD1neg  SD0  SD1  SD2  SD3
#> 1       168   0.36   0.43   0.53 0.64 0.77 0.94 1.14
#> 2       169   0.36   0.44   0.54 0.65 0.79 0.96 1.16
#> 3       170   0.37   0.45   0.55 0.66 0.80 0.98 1.18
#> 4       171   0.38   0.46   0.56 0.68 0.82 0.99 1.21
#> 5       172   0.39   0.47   0.57 0.69 0.84 1.01 1.23
#> 6       173   0.39   0.48   0.58 0.70 0.85 1.03 1.25
```
