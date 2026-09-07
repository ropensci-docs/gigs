# Get and set gigs package-level options

By default, gigs will handle invalid input data, e.g. missing (`NA`) or
undefined (`NaN`, `Inf` and `-Inf`) values, by warning you of their
presence and replacing the invalid values with `NA`. It will also warn
you about unused factor levels when running growth outcome analyses.

You can change this input-checking behaviour with `gigs_option_set()` so
that gigs does this silently, or make gigs throw errors when confronted
with bad data. You can also make gigs drop unused factor levels in its
outputs, or silence its warnings about unused factor levels. You can
also change all options for gigs input-checking at once using
`gigs_input_options_set()`.

## Usage

``` r
gigs_option_get(option, silent = FALSE)

gigs_option_set(option, new_value, silent = FALSE)

gigs_input_options_set(new_value, silent = FALSE)
```

## Arguments

- option:

  A single case-sensitive character variable, one of:

  - `"handle_missing_data"` - How should gigs handle missing (`NA`)
    elements?

  - `"handle_undefined_data"` - How should gigs handle undefined (`NaN`,
    `Inf`, `-Inf`) elements?

  - `"handle_oob_xvar"` - How should gigs handle elements of `x`
    variables which are out of bounds for the standard in use?

  - `"handle_invalid_sex"` - How should gigs handle elements of `sex`
    which are not one of `"M"` or `"F"`?

  - `"handle_oob_centiles"` - In `centile2value` functions, how should
    gigs handle elements of `p` that are not between `0` and `1`?

  - `"handle_unused_levels"` - When generating growth categories as
    factors, should gigs drop or keep unused factor levels, and should
    it issue warnings when unused factor levels occur?

- silent:

  A single logical value controlling whether a message will be printed
  to the console describing either:

  - The current value of `option` in `gigs_option_get()`.

  - The `new_value` of `option` in `gigs_option_set()`.

  This argument will not accept an integer in place of a logical value.

- new_value:

  A single case-sensitive character variable. For all options **except**
  `"handle_unused_levels"`, this should be one of:

  - `"quiet"` - gigs will replace invalid vector elements with `NA`
    quietly.

  - `"warn"` - gigs will replace invalid vector elements with `NA`
    loudly.

  - `"error"` - gigs will throw informative errors if any invalid inputs
    are encountered.

  For "handle_unused_levels", `new_value` should be one of:

  - `"keep_quiet"` - Keep unused factor levels, and don't issue a
    warning.

  - `"keep_warn"` - Keep unused factor levels, whilst issuing a warning.

  - `"drop_quiet"` - Drop unused factor levels, and don't issue a
    warning.

  - `"drop_warn"` - Drop unused factor levels, whilst issuing a warning.

  By default, GIGS options are `"warn"` for input handling and
  `"keep_warn"` for `"handle_unused_levels"`.

## Value

A single-length character vector. For `gigs_option_get()`, the current
value of `option`; for `gigs_option_get()`, the new value of `option`;
for `gigs_input_options_set()`, `new_value`. If `silent = FALSE`
(default), then informative messages will be printed to the console
regarding the current/new values of `option`.

## Examples

``` r
# Show the names of all available options
names(.gigs_options)
#> [1] "handle_oob_centiles"   "handle_unused_levels"  "handle_undefined_data"
#> [4] "handle_oob_xvar"       "handle_missing_data"   "handle_invalid_sex"   

# Retrieve the value of a gigs option (if `silent = FALSE`, would print a
# message)
option_value <- gigs_option_get("handle_missing_data", silent = TRUE)
print(option_value)
#> [1] "warn"

# Set the value of an option
gigs_option_set("handle_undefined_data", "error", silent = TRUE)

# Check that change has occurred
option_value <- gigs_option_get("handle_undefined_data", silent = TRUE)
print(option_value)
#> [1] "error"

# Suppress printed output with `silent = TRUE`
gigs_option_set("handle_undefined_data", "quiet", silent = TRUE)

# Set all GIGS options for input checking
gigs_input_options_set("warn", silent = TRUE)
```
