# Categorise birthweight centiles and gestational ages into small vulnerable newborn strata

Categorise birthweight centiles and gestational ages into small
vulnerable newborn strata

## Usage

``` r
categorise_svn(p, gest_days)
```

## Arguments

- p:

  A numeric vector with birth weight centiles from the
  INTERGROWTH-21^(st) Newborn Size standard. If elements of `p` are not
  between `0` and `1`, gigs will warn you. You can customise this
  behaviour with the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- gest_days:

  A numeric vector of length one or more with gestational age(s) in
  days. Used to determine whether infants are term or preterm (a
  gestational age \> 259 days means an infant is term).

## Value

An object of class factor with the same length as the longest input
vector, containing small vulnerable newborn classifications. Its levels
are
`c("Preterm SGA", "Preterm AGA", "Preterm LGA", "Term SGA", "Term AGA", "Term LGA")`.
By default, gigs will inform you this object contains unused factor
levels. You can change this behaviour using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for small, vulnerable newborn categorisations are:

|  |  |  |  |
|----|----|----|----|
| **SVN category** | **Factor level** | **Centile bounds** | **Gestational age range** |
| Preterm-SGA | `"Preterm SGA"` | `p` \< 0.1 | `gest_days` \< 259 |
| Preterm-AGA | `"Preterm AGA"` | 0.1 =\< `p` =\< 0.9 | `gest_days` \< 259 |
| Preterm-LGA | `"Preterm LGA"` | `p` \> 0.9 | `gest_days` \< 259 |
| Term-SGA | `"Term SGA"` | `p` \< 0.1 | `gest_days` \>= 259 |
| Term-AGA | `"Term AGA"` | 0.1 =\< `p` =\< 0.9 | `gest_days` \>= 259 |
| Term-LGA | `"Term LGA"` | `p` \> 0.9 | `gest_days` \>= 259 |

*Abbreviations:* SGA, small-for-gestational age; AGA,
appropriate-for-gestational age; LGA, large-for-gestational age.

## Note

Input vectors are recycled by
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html),
and must adhere to the [vctrs recycling
rules](https://vctrs.r-lib.org/reference/theory-faq-recycling.html).

## References

Lawn JE, Ohuma EO, Bradley E, Idueta LS, Hazel E, Okwaraji YB et al.
**Small babies, big risks: global estimates of prevalence and mortality
for vulnerable newborns to accelerate change and improve counting.**
*The Lancet* 2023, *401(10389):1707-1719.*
[doi:10.1016/S0140-6736(23)00522-6](https://doi.org/10.1016/S0140-6736%2823%2900522-6)

## See also

[`classify_svn()`](https://docs.ropensci.org/gigs/reference/classify_svn.md),
which wraps this function for easy use in analytic pipelines. Also check
out
[`categorise_sfga()`](https://docs.ropensci.org/gigs/reference/categorise_sfga.md),
which this function uses to stratify `p` into size-for-gestational age
categories.

## Examples

``` r
p <- c(0.01, 0.07, 0.25, 0.75, 0.93, 0.99)
gest_days <- c(250, 250, 250, 280, 280, 280) # 3 preterm, 3 term
categorise_svn(p = p, gest_days = gest_days)
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm LGA" and "Term SGA".
#> [1] Preterm SGA Preterm SGA Preterm AGA Term AGA    Term LGA    Term LGA   
#> Levels: Preterm SGA Preterm AGA Preterm LGA Term SGA Term AGA Term LGA
```
