# Package index

## Get growth indicator classifications in `data.frame`-like objects

- [`classify_growth()`](https://docs.ropensci.org/gigs/reference/classify_growth.md)
  : Classify multiple growth indicators at the same time using
  GIGS-recommended growth standards

- [`classify_sfga()`](https://docs.ropensci.org/gigs/reference/classify_sfga.md)
  :

  Classify size-for-gestational age in `data.frame`-like objects with
  the INTERGROWTH-21^(st) weight-for-gestational age standard

- [`classify_svn()`](https://docs.ropensci.org/gigs/reference/classify_svn.md)
  :

  Classify small vulnerable newborns in `data.frame`-like objects with
  the INTERGROWTH-21^(st) weight-for-gestational age standard

- [`classify_stunting()`](https://docs.ropensci.org/gigs/reference/classify_stunting.md)
  :

  Classify stunting in `data.frame`-like objects with GIGS-recommended
  growth standards

- [`classify_wasting()`](https://docs.ropensci.org/gigs/reference/classify_wasting.md)
  :

  Classify wasting in `data.frame`-like objects with GIGS-recommended
  growth standards

- [`classify_wfa()`](https://docs.ropensci.org/gigs/reference/classify_wfa.md)
  :

  Classify weight-for-age in `data.frame`-like objects with
  GIGS-recommended growth standards

- [`classify_headsize()`](https://docs.ropensci.org/gigs/reference/classify_headsize.md)
  :

  Classify head size in `data.frame`-like objects with GIGS-recommended
  growth standards

## Get growth indicator classifications using multiple vectors

- [`compute_sfga()`](https://docs.ropensci.org/gigs/reference/compute_sfga.md)
  :

  Get size-for-gestational age categories using multiple vectors and the
  INTERGROWTH-21^(st) weight-for-gestational age standard

- [`compute_svn()`](https://docs.ropensci.org/gigs/reference/compute_svn.md)
  :

  Get small vulnerable newborn categories using multiple vectors and the
  INTERGROWTH-21^(st) weight-for-gestational age standard

- [`compute_stunting()`](https://docs.ropensci.org/gigs/reference/compute_stunting.md)
  : Get stunting categories using multiple vectors and GIGS-recommended
  growth standards

- [`compute_wasting()`](https://docs.ropensci.org/gigs/reference/compute_wasting.md)
  : Get wasting categories using multiple vectors and GIGS-recommended
  growth standards

- [`compute_wfa()`](https://docs.ropensci.org/gigs/reference/compute_wfa.md)
  : Get weight-for-age categories using multiple vectors and
  GIGS-recommended growth standards

- [`compute_headsize()`](https://docs.ropensci.org/gigs/reference/compute_headsize.md)
  : Get head size categories using multiple vectors and GIGS-recommended
  growth standards

## Get growth indicator classifications from z-scores/centiles

- [`categorise_sfga()`](https://docs.ropensci.org/gigs/reference/categorise_sfga.md)
  : Categorise birthweight centiles into size-for-gestational age strata
- [`categorise_svn()`](https://docs.ropensci.org/gigs/reference/categorise_svn.md)
  : Categorise birthweight centiles and gestational ages into small
  vulnerable newborn strata
- [`categorise_stunting()`](https://docs.ropensci.org/gigs/reference/categorise_stunting.md)
  : Categorise length/height-for-age z-scores into stunting strata
- [`categorise_wasting()`](https://docs.ropensci.org/gigs/reference/categorise_wasting.md)
  : Categorise weight-for-length/height z-scores into wasting strata
- [`categorise_wfa()`](https://docs.ropensci.org/gigs/reference/categorise_wfa.md)
  : Categorise weight-for-age z-scores into weight-for-age strata
- [`categorise_headsize()`](https://docs.ropensci.org/gigs/reference/categorise_headsize.md)
  : Categorise head circumference-for-age z-scores into head
  circumference-for-age strata

## Get z-scores using recommended standards

- [`gigs_waz()`](https://docs.ropensci.org/gigs/reference/gigs_zscoring.md)
  [`gigs_lhaz()`](https://docs.ropensci.org/gigs/reference/gigs_zscoring.md)
  [`gigs_wlz()`](https://docs.ropensci.org/gigs/reference/gigs_zscoring.md)
  [`gigs_hcaz()`](https://docs.ropensci.org/gigs/reference/gigs_zscoring.md)
  : Calculate z-scores for anthropometric measures according to GIGS
  guidance

## Convert between values and z-scores/centiles using international growth standards

- [`value2zscore()`](https://docs.ropensci.org/gigs/reference/value2zscore.md)
  [`value2centile()`](https://docs.ropensci.org/gigs/reference/value2zscore.md)
  : Convert anthropometric measures to z-scores/centiles using
  international growth standards
- [`zscore2value()`](https://docs.ropensci.org/gigs/reference/zscore2value.md)
  [`centile2value()`](https://docs.ropensci.org/gigs/reference/zscore2value.md)
  : Convert z-scores/centiles to anthropometric measures using
  international growth standards
- [`report_units()`](https://docs.ropensci.org/gigs/reference/report_units.md)
  : Check required units for a conversion using gigs

## INTERGROWTH-21^(st) Estimation Functions

Estimation functions from the INTERGROWTH-21^(st) Project.

- [`ig_fet_estimate_fetal_weight()`](https://docs.ropensci.org/gigs/reference/ig_fet_estimate_fetal_weight.md)
  :

  Estimate fetal weight in grams using the INTERGROWTH-21^(st)
  predictive equation

- [`ig_fet_estimate_ga()`](https://docs.ropensci.org/gigs/reference/ig_fet_estimate_ga.md)
  :

  Estimate gestational age using INTERGROWTH-21^(st) predictive
  equations

## Reference data and coefficient tables

Lists containing data frames with growth curve data, model parameters
for WHO and some INTERGROWTH-21^(st) standards, and data from the LIFE
study.

- [`ig_nbs`](https://docs.ropensci.org/gigs/reference/ig_nbs.md) :

  INTERGROWTH-21^(st) Newborn Size Standards (including very preterm)
  growth curve data

- [`ig_nbs_coeffs`](https://docs.ropensci.org/gigs/reference/ig_nbs_coeffs.md)
  :

  INTERGROWTH-21^(st) Newborn Size Standards GAMLSS coefficients

- [`ig_nbs_ext`](https://docs.ropensci.org/gigs/reference/ig_nbs_ext.md)
  :

  Extended INTERGROWTH-21^(st) Newborn Size Standards (including very
  preterm) growth curve data

- [`ig_nbs_ext_coeffs`](https://docs.ropensci.org/gigs/reference/ig_nbs_ext_coeffs.md)
  :

  Extended INTERGROWTH-21^(st) Newborn Size Standards GAMLSS
  coefficients

- [`ig_png`](https://docs.ropensci.org/gigs/reference/ig_png.md) :

  INTERGROWTH-21^(st) Postnatal Growth Standards growth curve data

- [`ig_fet`](https://docs.ropensci.org/gigs/reference/ig_fet.md) :

  INTERGROWTH-21^(st) Fetal Standards growth curve data

- [`who_gs`](https://docs.ropensci.org/gigs/reference/who_gs.md) : WHO
  Child Growth Standards growth curve data

- [`who_gs_coeffs`](https://docs.ropensci.org/gigs/reference/who_gs_coeffs.md)
  : WHO Child Growth Standards LMS coefficients

- [`life6mo`](https://docs.ropensci.org/gigs/reference/life6mo.md) :
  Data extract from the Low birthweight Infant Feeding Exploration
  (LIFE) study

## Package-level options

Options to control how gigs should handle missing or undefined data, and
some out-of-bounds values.

- [`.gigs_options`](https://docs.ropensci.org/gigs/reference/dot-gigs_options.md)
  : Package-level gigs options
- [`gigs_option_get()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
  [`gigs_option_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
  [`gigs_input_options_set()`](https://docs.ropensci.org/gigs/reference/gigs_options.md)
  : Get and set gigs package-level options
