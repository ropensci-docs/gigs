# Check required units for a conversion using gigs

Check required units for a conversion using gigs

## Usage

``` r
report_units(family, acronym)
```

## Arguments

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

Returns a message describing which units are required for conversion in
the desired growth standard.

## Examples

``` r
# Get units for working with the IG-21st Newborn Size Standard for
# weight-for-GA
report_units("ig_nbs", "wfga")
#> You're using "wfga" from the INTERGROWTH-21st Newborn Size Standards
#> ("ig_nbs").
#> ℹ Units for `y`: Weight (kg).
#> ℹ Units for `x`: Gestational age (days).

# Get units for working with the IG-21st Fetal Standard for
# gestational weight gain
report_units("ig_fet", "gwgfga")
#> You're using "gwgfga" from the INTERGROWTH-21st Fetal Standards ("ig_fet").
#> ℹ Units for `y`: Gestational weight gain (g).
#> ℹ Units for `x`: Gestational age (days).
```
