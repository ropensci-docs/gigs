# Extended INTERGROWTH-21^(st) Newborn Size Standards GAMLSS coefficients

A set of nested lists containing mu, sigma, nu and tau values across
gestational ages for either sex, for the extended INTERGROWTH-21^(st)
weight/length/head circumference-for-gestational age standards in
newborns. The lists are ordered by acronym, then sex.

## Source

Mu/sigma/nu/tau values were provided by Dr Eric Ohuma.

## Note

The mu and sigma coefficients have been extrapolated by Simon Parker
(with guidance from Eric Ohuma) to include a wider range of gestational
ages, and should be applied carefully by researchers. More detail on the
extrapolation process is available in an article on the package website.

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
names(gigs::ig_nbs_ext_coeffs)
#> [1] "wfga"  "lfga"  "hcfga"
head(gigs::ig_nbs_ext_coeffs$wfga$male)
#>   gest_days       mu     sigma       nu      tau
#> 1       231 1.905973 0.4027349 1.095261 17.05299
#> 2       232 1.945933 0.4024603 1.095261 17.05299
#> 3       233 1.985389 0.4021894 1.095261 17.05299
#> 4       234 2.024345 0.4019221 1.095261 17.05299
#> 5       235 2.062806 0.4016584 1.095261 17.05299
#> 6       236 2.100775 0.4013983 1.095261 17.05299
```
