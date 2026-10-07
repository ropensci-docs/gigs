# Convert anthropometric measures to z-scores/centiles using international growth standards

Convert anthropometric measures to z-scores/centiles using international
growth standards

## Usage

``` r
value2zscore(y, x, sex = NULL, family, acronym)

value2centile(y, x, sex = NULL, family, acronym)
```

## Arguments

- y:

  Numeric vector of length one or more with anthropometric
  measurement(s) to convert to centiles/z-scores. Units depend on which
  combination of `family` and `acronym` are in use, which you can check
  with
  [`report_units()`](https://docs.ropensci.org/gigs/reference/report_units.md).
  By default, GIGS will warn you if elements in `y` are missing (`NA`)
  or undefined (`NaN`/`Inf`), and replace the latter with `NA`. You can
  customise this behaviour using the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- x:

  Numeric vector of x values, which take on different units depending on
  the growth standard in use. To know which units to use, run
  `report_units(family, acronym)`. Limits for each combination are as
  follows:

  - WHO Growth Standards (family = `"who_gs"`)

    - Between 0 and 1856 days for `"wfa"`, `"bfa"`, `"lhfa"`, and
      `"hcfa"`.

    - Between 45 and 110 cm for `"wfl"`.

    - Between 65 and 120 cm for `"wfh"`.

    - Between 91 and 1856 days for `"acfa"`, `"ssfa"`, `"tsfa"`.

  - INTERGROWTH-21^(st) Fetal Standards (family = `"ig_fet"`)

    - Between 98 and 280 days for `"hcfga"`, `"bpdfga"`, `"acfga"`,
      `"flfga"`, `"ofdfga"`, and  
      `"tcdfga"`.

    - Between 154 and 280 days for `"efwfga"`.

    - Between 112 and 294 days for `"sfhfga"`.

    - Between 58 and 105 days for `"crlfga"`.

    - Between 19 and 95 mm for `"gafcrl"`.

    - Between 105 and 280 days for `"gwgfga"`.

    - Between 168 and 280 days for `"pifga"`, `"rifga"`, and `"sdrfga"`
      (the INTERGROWTH-21^(st) Fetal Doppler standards).

    - Between 12 and 55 mm for`"tcdfga"`.

    - Between 105 and 252 days for `"poffga"`, `"sffga"`, `"avfga"`,
      `"pvfga"`, and `"cmfga"` (the INTERGROWTH-21^(st) Fetal Brain
      Development standards).

    - Between 126 and 287 days for `"hefwfga"` (the INTERGROWTH-21^(st)
      standard for Hadlock-based estimated fetal weight).

  - INTERGROWTH-21^(st) Newborn Size Standards (family = `"ig_nbs"`)

    - Between 168 and 300 days for `"wfga"`, `"lfga"`, `"hcfga"`, and
      `"wlrfga"`.

    - Between 266 and 280 days for `"fmfga"`, `"bfpfga"`, and
      `"ffmfga"`.

  - Extended INTERGROWTH-21^(st) Newborn Size Standards (family =
    `"ig_nbs_ext"`)

    - Between 154 and 314 days for `"wfga"`, `"lfga"`, and `"hcfga"`.

  - INTERGROWTH-21^(st) Postnatal Growth Standards (family = `"ig_png"`)

    - Between 27 and 64 weeks for `"wfa"`, `"lfa"`, and `"hcfa"`.

    - Between 35 and 65 cm for `"wfl"`.

  By default, gigs will replace out-of-bounds elements in `x` with `NA`
  and warn you. It will also warn you about elements in `x` which are
  missing (`NA`) or undefined (`NaN`/`Inf`). You can customise this
  behaviour using the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- sex:

  Character vector of length one or more with sex(es), either `"M"`
  (male) or `"F"` (female). This argument should be left as `NULL` (the
  default) if `family == "ig_fet"`. This argument is case-sensitive. By
  default, gigs will replace elements of `sex` which are not `"M"` or
  `"F"` with `NA` and warn you. You can customise this behaviour using
  the [GIGS package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- family:

  A single string denoting the family of growth standards in use. Must
  be one of `"ig_fet"`, `"ig_nbs"`, `"ig_png"`, or `"who_gs"`, or the
  function will throw an error. This argument is case-sensitive.

- acronym:

  A single string denoting the specific growth standard in use. The
  allowed values of `acronym` depend on the value of `family`, and are
  listed in the documentation for the `x` argument. Incompatible
  `family` and `acronym` values will cause errors to be thrown. This
  argument is case-sensitive.

## Value

Numeric vector of z-scores/centiles with length equal to the longest
input vector.

## Note

Inputs other than `acronym` and `family` will be recycled by
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html),
and must adhere to the [vctrs recycling
rules](https://vctrs.r-lib.org/reference/theory-faq-recycling.html).

## References

- For the INTERGROWTH-21^(st) Fetal standards see the
  [`gigs::ig_fet`](https://docs.ropensci.org/gigs/reference/ig_fet.md)
  documentation

- For the INTERGROWTH-21^(st) Newborn Size standards see the
  [`gigs::ig_nbs`](https://docs.ropensci.org/gigs/reference/ig_nbs.md)
  documentation

- For the INTERGROWTH-21^(st) Postnatal Growth standards see the
  [`gigs::ig_png`](https://docs.ropensci.org/gigs/reference/ig_png.md)
  documentation

- For the WHO Growth standards see the
  [`gigs::who_gs`](https://docs.ropensci.org/gigs/reference/who_gs.md)
  documentation

## See also

[`report_units()`](https://docs.ropensci.org/gigs/reference/report_units.md)
will tell you the units needed for `y` and `x`, for any combination of
`family` and `acronym`.

## Examples

``` r
# Convert in the weight-for-age standard from the WHO Child Growth Standards
value2zscore(3, 0, "M", family = "who_gs", acronym = "wfa")
#> [1] -0.7342639

# Or obtain centiles...
value2centile(3, 0, "M", family = "who_gs", acronym = "wfa")
#> [1] 0.231394

# Inputs will be recycled if necessary
value2centile(2.5, 280, c("M", "F"), family = "ig_nbs", acronym = "wfga")
#> [1] 0.01444696 0.02267229
```
