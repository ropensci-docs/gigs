# Estimate gestational age using INTERGROWTH-21^(st) predictive equations

Estimate gestational age using INTERGROWTH-21^(st) predictive equations

## Usage

``` r
ig_fet_estimate_ga(crl_mm = NULL, headcirc_mm = NULL, femurlen_mm = NULL)
```

## Arguments

- crl_mm:

  Numeric vector with crown-rump length value(s) in mm taken from an
  ultrasound scan obtained 56 to 97 days since the last menstrual
  period. If not `NULL` (the default), should be of length one or the
  same length as other inputs. The function will return NA for all
  elements of `crl_mm` which are not between 15 and 95 mm and have no
  `headcirc_mm` or `abdocirc_mm` values.

- headcirc_mm:

  Numeric vector with head circumference value(s) in cm taken from an
  ultrasound scan obtained 98 to 181 days since the last menstrual
  period. If not `NULL` (the default), should have length one or same
  length as other inputs.

- femurlen_mm:

  Numeric vector with femur length value(s) in cm. If not `NULL` (the
  default), should have length one or same length as other arguments
  inputs.

## Value

A numeric vector with estimated gestational ages in days. This vector
will have a length equal to the outputs from
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html).

## Note

Vector inputs to this function are recycled using
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html).
The function will attempt to estimate the gestational age (GA) in three
steps, from highest to lowest accuracy. First, using crown-rump length
measurements obtained in early pregnancy, then with both head
circumference and femur length measurements, and finally with head
circumference alone.

## References

Papageorghiou AT, Kennedy SH, Salomon LJ, Ohuma EO, Cheikh Ismail L,
Barros FC et al. **International standards for early fetal size and
pregnancy dating based on ultrasound measurement of crown-rump length in
the first trimester of pregnancy.** *Ultrasound Obstet Gynecol* 2014,
**44(6):641-48**
[doi:10.1002/uog.13448](https://doi.org/10.1002/uog.13448)

Papageorghiou AT, Kemp B, Stones W, Ohuma EO, Kennedy SH, Purwar M et
al. **Ultrasound-based gestational age estimation in late pregnancy.**
*Ultrasound Obstet Gynecol* 2016. **48(6):719-26**
[doi:10.1002/uog.15894](https://doi.org/10.1002/uog.15894)

## Examples

``` r
# Estimate gestational age in days using crown-rump length (most accurate)
ig_fet_estimate_ga(crl_mm = 40:45)
#> [1] 75.20116 75.80278 76.40134 76.99695 77.58970 78.17970

# Estimate gestational age in days using head circumference and femur length
# (second-most accurate)
ig_fet_estimate_ga(headcirc_mm = 250:255, femurlen_mm = 55:60)
#> [1] 200.5229 202.7155 204.9335 207.1772 209.4469 211.7429

# Estimate gestational age in days using head circumference only (least
# accurate)
ig_fet_estimate_ga(headcirc_mm = 250:255)
#> [1] 189.8030 190.5331 191.2662 192.0023 192.7416 193.4839

# The function defaults to CRL if available
ig_fet_estimate_ga(crl_mm = 40:45,
                   headcirc_mm = 250:255,
                   femurlen_mm = 55:60)
#> [1] 75.20116 75.80278 76.40134 76.99695 77.58970 78.17970

# Inputs are recycled using [vctrs::vec_recycle_common]
ig_fet_estimate_ga(headcirc_mm = 252,
                   femurlen_mm = 55:60)
#> [1] 201.2413 203.0790 204.9335 206.8049 208.6934 210.5992
```
