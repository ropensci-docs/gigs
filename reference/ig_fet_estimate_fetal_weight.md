# Estimate fetal weight in grams using the INTERGROWTH-21^(st) predictive equation

Estimate fetal weight in grams using the INTERGROWTH-21^(st) predictive
equation

## Usage

``` r
ig_fet_estimate_fetal_weight(abdocirc_mm, headcirc_mm)
```

## Arguments

- abdocirc_mm:

  Numeric vector with abdominal circumference value(s) in mm. Should
  have length one or same length as `headcirc_mm`.

- headcirc_mm:

  Numeric vector with head circumference value(s) in mm. Should have
  length one or same length as `abdocirc_mm`.

## Value

Numeric vector with estimated fetal weight(s) in g, with the same length
as the longest input vector.

## Note

Inputs are recycled using
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html).

## References

Stirnemann J, Villar J, Salomon LJ, Ohuma EO, Lamber A, Victoria CG et
al. **International Estimated Fetal Weight Standards of the
INTERGROWTH-21st Project.** *Ultrasound Obstet Gynecol* 2016,
**49:478-486**
[doi:10.1002/uog.17347](https://doi.org/10.1002/uog.17347)

## Examples

``` r
# Estimate fetal weight in grams
ig_fet_estimate_fetal_weight(abdocirc_mm = 31:33,
                             headcirc_mm = 25:27)
#> [1] 176.1847 176.8672 177.5590

# Input vectors are recycled using vctrs::vec_recycle_common
ig_fet_estimate_fetal_weight(abdocirc_mm = 25.0,
                             headcirc_mm = 24:26)
#> [1] 174.9972 175.5469 176.0984
```
