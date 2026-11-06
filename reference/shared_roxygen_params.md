# Shared roxygen parameters

Many of the parameters in `[gigs]` are shared between different
functions. This roxygen block makes sharing these parameters more
simple.

## Arguments

- y:

  Numeric vector of length one or more with anthropometric
  measurement(s) to convert to centiles/z-scores. Units depend on which
  `acronym` is in use.

- z, p:

  Numeric vector of length one or more with centiles/z-scores to convert
  to values. For `p`, gigs will warn you if elements of `p` are not
  between `0` and `1`. You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- sex:

  Character vector of length one or more with sex(es), either `"M"`
  (male) or `"F"` (female). This argument is case-sensitive. By default,
  gigs will replace elements of `sex` which are not `"M"` or `"F"` with
  `NA` and warn you. You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

## Note

Input vectors other than `acronym` and `family` are recycled by
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html),
and must adhere to the [vctrs recycling
rules](https://vctrs.r-lib.org/reference/theory-faq-recycling.html).
