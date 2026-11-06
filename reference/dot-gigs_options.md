# Package-level gigs options

An environment containing seven named character vectors. The first six
define how **gigs** handles input data with missing, undefined, or
invalid elements in input data. The last (`"handle_unused_levels"`)
defines how **gigs** responds to unused factor levels when performing
growth categorisations.

- `"handle_missing_data"` - How should gigs handle missing (`NA`)
  elements?

- `"handle_undefined_data"` - How should gigs handle undefined (`NaN`,
  `Inf`, `-Inf`) elements?

- `"handle_oob_xvar"` - How should gigs handle elements of `x` variables
  which are out of bounds for the standard in use?

- `"handle_invalid_sex"` - How should gigs handle elements of `sex`
  which are not one of `"M"` or `"F"`?

- `"handle_oob_centiles"` - In `centile2value` functions, how should
  gigs handle elements of `p` that are not between `0` and `1`?

- `"handle_unused_levels"` - When generating growth categories as
  factors, should gigs drop or keep unused factor levels, and should it
  issue warnings when unused factor levels occur?

Each of the input-checking options can take one of three values:

- `"quiet"` - Invalid elements are set to `NA`, silently.

- `"warn"` - Invalid elements are set to `NA`, with warnings issued when
  this is done.

- `"error"` - Invalid elements will cause informative errors.

For "handle_unused_levels", there are four valid choices:

- `"keep_quiet"` - Keep unused factor levels, and don't issue a warning.

- `"keep_warn"` - Keep unused factor levels, whilst issuing a warning.

- `"drop_quiet"` - Drop unused factor levels, and don't issue a warning.

- `"drop_warn"` - Drop unused factor levels, whilst issuing a warning.

You can use
[`gigs_option_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
or
[`gigs_option_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
to change these options on a one-by-one basis. To change all the
input-checking options to a specific value, use
[`gigs_input_options_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md).

## Value

A named environment, where each name maps onto a specific **gigs**
option.

## See also

The
[`gigs_option_get()`](https://docs.ropensci.org/gigs/reference/gigs_options.md),
[`gigs_option_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
and
[`gigs_input_options_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
functions, which can be used to get and set values in `.gigs_options`.

## Examples

``` r
# Get the names of all available options
names(.gigs_options)
#> [1] "handle_oob_centiles"   "handle_unused_levels"  "handle_undefined_data"
#> [4] "handle_oob_xvar"       "handle_missing_data"   "handle_invalid_sex"   
```
