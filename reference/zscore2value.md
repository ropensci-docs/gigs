# Convert z-scores/centiles to anthropometric measures using international growth standards

Convert z-scores/centiles to anthropometric measures using international
growth standards

## Usage

``` r
zscore2value(z, x, sex = NULL, family, acronym)

centile2value(p, x, sex = NULL, family, acronym)
```

## Arguments

- z, p:

  Numeric vector of length one or more with centiles/z-scores to convert
  to values. For `p`, gigs will warn you if elements of `p` are not
  between `0` and `1`. You can customise this behaviour using the [GIGS
  package-level
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

Numeric vector of expected measurements with length equal to the longest
input vector.

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

## Examples

``` r
# Convert in the weight-for-age standard from the WHO Child Growth Standards
zscore2value(-2:2, 0, "M", family = "who_gs", acronym = "wfa")
#> [1] 2.459312 2.880651 3.346400 3.858619 4.419354

# Or obtain centiles...
centile2value(pnorm(-2:2), 0, "M", family = "who_gs", acronym = "wfa")
#> [1] 2.459312 2.880651 3.346400 3.858619 4.419354

# Inputs will be recycled if necessary
centile2value(3, 280, c("M", "F"), family = "ig_nbs", acronym = "wfga")
#> Warning: Input arguments have invalid values:
#> ℹ Argument `p`: All (1) elements were not between 0 and 1.
#> [1] NA NA
```
