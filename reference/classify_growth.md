# Classify multiple growth indicators at the same time using GIGS-recommended growth standards

This function permits classification of multiple growth indicators
(stunting, wasting, weight-for-age, and more) at once in
`data.frame`-like objects.

## Usage

``` r
classify_growth(
  .data,
  gest_days,
  age_days,
  sex,
  weight_kg = NULL,
  lenht_cm = NULL,
  headcirc_cm = NULL,
  id = NULL,
  .outcomes = c("sfga", "svn", "stunting", "wasting", "wfa", "headsize"),
  .new = list(sfga = c("birthweight_centile", "sfga", "sfga_severe"), svn =
    c("birthweight_centile", "svn"), stunting = c("lhaz", "stunting",
    "stunting_outliers"), wasting = c("wlz", "wasting", "wasting_outliers"), wfa =
    c("waz", "wfa", "wfa_outliers"), headsize = c("hcaz", "headsize")),
  .verbose = TRUE
)
```

## Arguments

- .data:

  A `data.frame`-like tabular object with one or more rows. Must be
  permissible by
  [`checkmate::assert_data_frame()`](https://mllg.github.io/checkmate/reference/checkDataFrame.html),
  so you can also supply a `tibble`, `data.table`, or similar.

- gest_days:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of
  gestational age(s) at birth in days. This column, in conjunction with
  the column referred to by `age_days`, is used to select which growth
  standard to use for each observation.

- age_days:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of age
  values in days.

- sex:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a case-sensitive character
  vector of sexes, either `"M"` (male) or `"F"` (female). By default,
  gigs will warn you if any elements of `sex` are not `"M"` or `"F"`, or
  are missing (`NA`). You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- weight_kg:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of weight
  values in kg. When performing size-for-GA and small vulnerable newborn
  classifications, centiles and classifications will only be provided
  where measurements were taken \<12hrs after birth, i.e.
  `age_days < 0.5`.

- lenht_cm:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of
  length/height values in cm.

- headcirc_cm:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a numeric vector of head
  circumference values in cm.

- id:

  \<[`data-masking`](https://rlang.r-lib.org/reference/args_data_masking.html)\>
  The name of a column in `.data` which is a factor variable with IDs
  for each observation. When not `NULL`, this variable is used to ensure
  that only the first measurement taken from each infant is used as a
  birth measure. If all your data is from one individual, leave this
  parameter as `NULL`. Default = `NULL`.

- .outcomes:

  A character vector of up to six elements in length describing which
  growth outcomes you want to assess. Use this when you supply data that
  can be used to generate multiple growth indicators, but only want to
  run a specific set. This argument is case-sensitive, and an error will
  be thrown if you supply a string in `.analyses` which is either `NA`
  or is not a member of this argument's default. Default =
  `c("sfga", "svn", "stunting", "wasting", "wfa", "headsize")`.

- .new:

  A list with names corresponding to `.analyses`, which describes the
  names of new columns to be added to `.data`. If any elements of the
  vectors in `.new` are equal to existing elements of `colnames(.data)`,
  the function will throw an error. Excluding the birthweight centiles
  produced when getting size-for-gestational age (`"sfga"`) and small
  vulnerable newborn (`"svn"`) classifications, all strings in `.new`
  must be unique. Each character vector in `.new` is repaired with
  `vctrs::as_names()`, which will issue messages if any elements in
  `.new` are changed.

  `"sfga"`:

  :   `c("birthweight_centile", "sfga", "sfga_severe")`

  `"svn"`:

  :   `c("birthweight_centile", "svn")`

  `"stunting"`:

  :   `c("lhaz", "stunting", "stunting_outliers")`

  `"wasting"`:

  :   `c("wlz", "wasting", "wasting_outliers")`

  `"wfa"`:

  :   `c("waz", "wfa", "wfa_outliers")`

  `"headsize"`:

  :   `c("hcaz", "headsize")`

- .verbose:

  A single logical value. When `TRUE` (the default), messages about
  which analyses were requested versus which were performed will be
  printed to the console. Warnings from `classify_growth()` will still
  be printed even if `.verbose` is `FALSE`.

## Value

A tabular object of the same class that was provided as `.data`, with
new columns named according to `.new`. The new columns will depend on
the values supplied for `.outcomes`.

## Note

For size-for-GA and small vulnerable newborn analyses, centiles and
categorisations will only be applied for birth measurements. These are
considered to be the observation per level of `id` where `age_days` is
smallest, provided that `age_days` is `<3`.

Categorical (factor) columns produced here may contain unused factor
levels. By default, gigs will inform you if these columns have unused
factor levels. You can change this behaviour using the [GIGS
package-level
option](https://docs.ropensci.org/gigs/reference/gigs_options.md)
`.gigs_options$handle_unused_levels`.

## References

WHO. **Physical status: the use and interpretation of anthropometry.
Report of a WHO Expert Committee.** *World Health Organisation Technical
Report Series 1995,* **854: 1–452**

Royal College of Obstetricians and Gynaecologists. **The Investigation
and Management of the Small-for-Gestational-Age Fetus: Green-top
Guideline No. 31.** *Technical report, Royal College of Obstetricians
and Gynaecologists, London, 2013.*

Lawn JE, Ohuma EO, Bradley E, Idueta LS, Hazel E, Okwaraji YB et al.
**Small babies, big risks: global estimates of prevalence and mortality
for vulnerable newborns to accelerate change and improve counting.**
*The Lancet* 2023, *401(10389):1707-1719.*
[doi:10.1016/S0140-6736(23)00522-6](https://doi.org/10.1016/S0140-6736%2823%2900522-6)

**'Implausible z-score values'** *in* World Health Organization (ed.)
*Recommendations for data collection, analysis and reporting on
anthropometric indicators in children under 5 years old*. Geneva: World
Health Organization and the United Nations Children's Fund UNICEF,
(2019). pp. 64-65.

**'Percentage of children stunted, wasted, and underweight, and mean
z-scores for stunting, wasting and underweight'** *in* *Guide to DHS
Statistics DHS-7* Rockville, Maryland, USA: ICF (2020). pp. 431-435.
<https://dhsprogram.com/data/Guide-to-DHS-Statistics/Nutritional_Status.htm>

Victora CG, Schuler-Faccini L, Matijasevich A, Ribeiro E, Pessoa A,
Barros FC. **Microcephaly in Brazil: how to interpret reported
numbers?** *The Lancet* 2016, *387(10019):621-624*
[doi:10.1016/S0140-6736(16)00273-7](https://doi.org/10.1016/S0140-6736%2816%2900273-7)

Accogli A, Geraldo AF, Piccolo G, Riva A, Scala M, Balagura G, et al.
**Diagnostic Approach to Macrocephaly in Children**. *Frontiers in
Paediatrics* 2022, *9:794069*
[doi:10.3389/fped.2021.794069](https://doi.org/10.3389/fped.2021.794069)

## See also

See
[`gigs_waz()`](https://docs.ropensci.org/gigs/reference/gigs_zscoring.md)
to learn which growth standard will be used for different combinations
of gestational/chronological age.

## Examples

``` r
# This dummy dataset contains data from two people, from birth (<3 days) to
# 500 days of age.
data <- data.frame(
  child = factor(rep.int(c("A", "B"), c(3, 3))),
  agedays = c(0, 100, 500, 2, 100, 500),
  gestage  = c(rep(35 * 7, 3), rep(35 * 7, 3)),
  sex = rep.int(c("M", "F"), c(3, 3)),
  wt_kg = c(3, 6, 9, 3, 6, 9),
  len_cm = rep.int(c(52.2, 60.4, 75), 2),
  head_cm = rep.int(c(30, 40, 49), 2)
)

data_classified <- classify_growth(data,
                                   age_days = agedays,
                                   gest_days = gestage,
                                   weight_kg = wt_kg,
                                   lenht_cm = len_cm,
                                   headcirc_cm = head_cm,
                                   sex = sex,
                                   id = child)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after size-for-GA categorisation: "SGA".
#> ! Unused factor levels kept after size-for-GA categorisation: "SGA(<3)" and
#> "SGA".
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm SGA", "Term SGA", "Term AGA", and "Term LGA".
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe".
#> ! Unused factor levels kept after stunting categorisation: "stunting_severe"
#> and "outlier".
#> ! Unused factor levels kept after wasting categorisation: "wasting_severe",
#> "wasting", and "overweight".
#> ! Unused factor levels kept after wasting categorisation: "wasting_severe",
#> "wasting", "overweight", and "outlier".
#> ! Unused factor levels kept after weight-for-age (underweight) categorisation:
#> "underweight_severe", "underweight", and "overweight".
#> ! Unused factor levels kept after weight-for-age (underweight) categorisation:
#> "underweight_severe", "underweight", "overweight", and "outlier".
#> ! Unused factor levels kept after head size categorisation:
#> "microcephaly_severe", "microcephaly", and "macrocephaly_severe".
#> 
#> ── `gigs::classify_growth()` ───────────────────────────────────────────────────
#> ✔ Size-for-gestational age: Success
#> ✔ Small vulnerable newborns: Success
#> ✔ Stunting: Success
#> ✔ Wasting: Success
#> ✔ Weight-for-age: Success
#> ✔ Head size: Success

data_classified
#>   child agedays gestage sex wt_kg len_cm head_cm birthweight_centile sfga
#> 1     A       0     245   M     3   52.2      30           0.8893352  AGA
#> 2     A     100     245   M     6   60.4      40                  NA <NA>
#> 3     A     500     245   M     9   75.0      49                  NA <NA>
#> 4     B       2     245   F     3   52.2      30           0.9384734  LGA
#> 5     B     100     245   F     6   60.4      40                  NA <NA>
#> 6     B     500     245   F     9   75.0      49                  NA <NA>
#>   sfga_severe         svn       lhaz     stunting stunting_outliers        wlz
#> 1         AGA Preterm AGA  2.8236856 not_stunting      not_stunting         NA
#> 2        <NA>        <NA>  0.8876444 not_stunting      not_stunting  1.6408675
#> 3        <NA>        <NA> -2.1690082     stunting          stunting -0.6621871
#> 4         LGA Preterm LGA  3.4154524 not_stunting      not_stunting         NA
#> 5        <NA>        <NA>  1.8205012 not_stunting      not_stunting  1.3314150
#> 6        <NA>        <NA> -1.4423063 not_stunting      not_stunting -0.1829182
#>       wasting wasting_outliers        waz           wfa  wfa_outliers
#> 1        <NA>             <NA>  1.2230003 normal_weight normal_weight
#> 2 not_wasting      not_wasting  0.7413417 normal_weight normal_weight
#> 3 not_wasting      not_wasting -1.4866806 normal_weight normal_weight
#> 4        <NA>             <NA>  1.5420839 normal_weight normal_weight
#> 5 not_wasting      not_wasting  1.4395342 normal_weight normal_weight
#> 6 not_wasting      not_wasting -0.7859202 normal_weight normal_weight
#>         hcaz        headsize
#> 1 -1.5588136 normal_headcirc
#> 2  0.9510032 normal_headcirc
#> 3  1.4502711 normal_headcirc
#> 4 -1.3289704 normal_headcirc
#> 5  1.7433668 normal_headcirc
#> 6  2.2148421    macrocephaly

# Use `.outcomes` to set which growth indicators will be computed
data_svn <- classify_growth(data,
                            age_days = agedays,
                            gest_days = gestage,
                            sex = sex,
                            weight_kg = wt_kg,
                            id = child,
                            .outcomes = "svn")
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm SGA", "Term SGA", "Term AGA", and "Term LGA".
#> 
#> ── `gigs::classify_growth()` ───────────────────────────────────────────────────
#> ✔ Small vulnerable newborns: Success

data_svn
#>   child agedays gestage sex wt_kg len_cm head_cm birthweight_centile
#> 1     A       0     245   M     3   52.2      30           0.8893352
#> 2     A     100     245   M     6   60.4      40                  NA
#> 3     A     500     245   M     9   75.0      49                  NA
#> 4     B       2     245   F     3   52.2      30           0.9384734
#> 5     B     100     245   F     6   60.4      40                  NA
#> 6     B     500     245   F     9   75.0      49                  NA
#>           svn
#> 1 Preterm AGA
#> 2        <NA>
#> 3        <NA>
#> 4 Preterm LGA
#> 5        <NA>
#> 6        <NA>

# Use `.new` to specify new column names
data_svn <- classify_growth(data,
                            age_days = agedays,
                            gest_days = gestage,
                            sex = sex,
                            weight_kg = wt_kg,
                            id = child,
                            .outcomes = "svn",
                            .new = list("svn" = c("ig_nbs_centile",
                                                  "SVN_Category")))
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm SGA", "Term SGA", "Term AGA", and "Term LGA".
#> 
#> ── `gigs::classify_growth()` ───────────────────────────────────────────────────
#> ✔ Small vulnerable newborns: Success
data_svn
#>   child agedays gestage sex wt_kg len_cm head_cm ig_nbs_centile SVN_Category
#> 1     A       0     245   M     3   52.2      30      0.8893352  Preterm AGA
#> 2     A     100     245   M     6   60.4      40             NA         <NA>
#> 3     A     500     245   M     9   75.0      49             NA         <NA>
#> 4     B       2     245   F     3   52.2      30      0.9384734  Preterm LGA
#> 5     B     100     245   F     6   60.4      40             NA         <NA>
#> 6     B     500     245   F     9   75.0      49             NA         <NA>

# The function will warn you if you don't provide data for your outcomes
data_svn_stunting <- classify_growth(data,
                                     age_days = agedays,
                                     gest_days = gestage,
                                     sex = sex,
                                     weight_kg = wt_kg,
                                     id = child,
                                     .outcomes = c("svn", "stunting"))
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
#> ! Unused factor levels kept after small vulnerable newborn categorisation:
#> "Preterm SGA", "Term SGA", "Term AGA", and "Term LGA".
#> 
#> ── `gigs::classify_growth()` ───────────────────────────────────────────────────
#> ✔ Small vulnerable newborns: Success
#> ! Stunting: Not computed (`lenht_cm` not supplied)
data_svn_stunting
#>   child agedays gestage sex wt_kg len_cm head_cm birthweight_centile
#> 1     A       0     245   M     3   52.2      30           0.8893352
#> 2     A     100     245   M     6   60.4      40                  NA
#> 3     A     500     245   M     9   75.0      49                  NA
#> 4     B       2     245   F     3   52.2      30           0.9384734
#> 5     B     100     245   F     6   60.4      40                  NA
#> 6     B     500     245   F     9   75.0      49                  NA
#>           svn
#> 1 Preterm AGA
#> 2        <NA>
#> 3        <NA>
#> 4 Preterm LGA
#> 5        <NA>
#> 6        <NA>
```
