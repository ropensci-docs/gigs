# Get size-for-gestational age categories using multiple vectors and the INTERGROWTH-21^(st) weight-for-gestational age standard

Get size-for-gestational age categories using multiple vectors and the
INTERGROWTH-21^(st) weight-for-gestational age standard

## Usage

``` r
compute_sfga(weight_kg, gest_days, sex, severe = FALSE)
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

- severe:

  A single logical value specifying whether to categorise SGA values
  below the third centile (`0.03`) as `"SGA(<3)"`. Default = `FALSE`.

## Value

An object of class factor with the same length as the longest input
vector, containing size-for-GA classifications. If `severe = FALSE`,
levels are `c("SGA", "AGA", "LGA")`. If `severe = TRUE`, levels are
`c("SGA(<3)", "SGA", "AGA", "LGA")`. By default, gigs will inform you
this object contains unused factor levels. You can change this behaviour
using the [GIGS package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## Details

Cut-offs for size-for-gestational age categorisations are:

|                       |                  |                     |
|-----------------------|------------------|---------------------|
| **Category**          | **Factor level** | **Centile bounds**  |
| Severely small-for-GA | `"SGA(<3)"`      | `p` \< 0.03         |
| Small-for-GA          | `"SGA"`          | `p` \< 0.1          |
| Appropriate-for-GA    | `"AGA"`          | 0.1 =\< `p` =\< 0.9 |
| Large-for-GA          | `"LGA"`          | `p` \> 0.9          |

## Note

Input vectors are recycled by
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html),
and must adhere to the [vctrs recycling
rules](https://vctrs.r-lib.org/reference/theory-faq-recycling.html).

## References

WHO. **Physical status: the use and interpretation of anthropometry.
Report of a WHO Expert Committee.** *World Health Organisation Technical
Report Series 1995,* **854: 1–452**

Royal College of Obstetricians and Gynaecologists. **The Investigation
and Management of the Small-for-Gestational-Age Fetus: Green-top
Guideline No. 31.** *Technical report, Royal College of Obstetricians
and Gynaecologists, London, 2013.*

## Examples

``` r
# By default, does not differentiate between p < 0.03 and p < 0.10
compute_sfga(
  weight_kg = c(2.2, 2.5, 3.3, 4.0),
  gest_days = 266:269,
  sex = c("F", "M", "F", "M")
)
#> [1] SGA SGA AGA LGA
#> Levels: SGA AGA LGA

# With severe = TRUE, highlights p < 0.03
compute_sfga(
  weight_kg = c(2.2, 2.5, 3.3, 4.0),
  gest_days = 266:269,
  sex = c("F", "M", "F", "M"),
  severe = TRUE
)
#> [1] SGA(<3) SGA     AGA     LGA    
#> Levels: SGA(<3) SGA AGA LGA
```
