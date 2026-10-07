# Get small vulnerable newborn categories using multiple vectors and the INTERGROWTH-21^(st) weight-for-gestational age standard

Get small vulnerable newborn categories using multiple vectors and the
INTERGROWTH-21^(st) weight-for-gestational age standard

## Usage

``` r
compute_svn(weight_kg, gest_days, sex)
```

## Arguments

- weight_kg:

  Numeric vector of length one or more with weight value(s) in kg. It is
  assumed that weight measurements provided to this function are birth
  weights recorded \<12 hours after an infant's birth.

- gest_days:

  Numeric vector of length one or more with gestational ages in days.
  Classifications can only be computed when `gest_days` is between `168`
  and `300`, as these are the limits of the INTERGROWTH-21^(st) Newborn
  Size standards (including the Very Preterm standards). By default,
  gigs will warn you about elements of `gest_days` which are either
  outside these bounds, are `NA`, or are `Inf`. You can customise this
  behaviour using the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- sex:

  Character vector of length one or more with sex(es), either `"M"`
  (male) or `"F"` (female). This argument is case-sensitive. By default,
  gigs will replace elements of `sex` which are not `"M"` or `"F"` with
  `NA` and warn you. You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

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

## Examples

``` r
compute_svn(
  weight_kg = c(1.5, 2.6, 2.6, 3.5),
  gest_days = c(235, 257, 275, 295),
  sex = c("F", "M", "F", "M")
)
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm LGA" and "Term LGA".
#> [1] Preterm SGA Preterm AGA Term SGA    Term AGA   
#> Levels: Preterm SGA Preterm AGA Preterm LGA Term SGA Term AGA Term LGA
```
