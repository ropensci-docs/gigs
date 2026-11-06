# Categorise birthweight centiles into size-for-gestational age strata

Categorise birthweight centiles into size-for-gestational age strata

## Usage

``` r
categorise_sfga(p, severe = FALSE)
```

## Arguments

- p:

  A numeric vector with birth weight centiles from the
  INTERGROWTH-21^(st) Newborn Size standard. If elements of `p` are not
  between `0` and `1`, gigs will warn you. You can customise this
  behaviour with the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- severe:

  A single logical value specifying whether to categorise SGA values
  below the third centile as `"SGA(<3)"`. Default = `FALSE`.

## Value

An object of class factor with the same length as `p`, containing
size-for-GA classifications. If `severe = FALSE`, levels are
`c("SGA", "AGA", "LGA")`. If `severe = TRUE`, levels are
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

## See also

[`classify_sfga()`](https://docs.ropensci.org/gigs/reference/classify_sfga.md),
which wraps this function for easy use in `data.frame`-based analytic
pipelines.

## Examples

``` r
p <- c(0.01, 0.07, 0.25, 0.75, 0.93, 0.99)
categorise_sfga(p = p, severe = FALSE)
#> [1] SGA SGA AGA AGA LGA LGA
#> Levels: SGA AGA LGA
categorise_sfga(p = p, severe = TRUE)
#> [1] SGA(<3) SGA     AGA     AGA     LGA     LGA    
#> Levels: SGA(<3) SGA AGA LGA
```
