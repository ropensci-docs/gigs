# Calculate z-scores for anthropometric measures according to GIGS guidance

These functions calculate z-scores for weight-for-age (WAZs),
length/height-for-age (LHAZs), weight-for-length/height (WLZs), or head
circumference-for-age (HCAZs).

The growth standard used for each observation differs based on the
gestational and post-menstrual age of the infant being analysed. The
different procedures are based on the advised use of each growth
standard, where a measurement is considered a 'birth measurement' if it
is the first measurement taken from an infant and was taken \<3 days
after birth:

- `gest_days` \< 24 weeks (168 days):

  - Birth: No standard available

  - Postnatal: IG-21^(st) Postnatal Growth standards from 27 to 64
    weeks' PMA

  - Postnatal: Uncorrected WHO standard after 64 weeks' PMA

- `gest_days` \>= 24 weeks (168 days):

  - Birth: IG-21^(st) Newborn Size standards at birth (including Very
    Preterm Newborn Size standards if born before 33 weeks).

  - Postnatal: IG-21^(st) Postnatal Growth standards from 27 to 64
    weeks' PMA

  - Postnatal: Uncorrected WHO Child Growth standards after 64 weeks'
    PMA

- `gest_days` \>= 37 weeks (259 days):

  - Birth: IG-21^(st) Newborn Size standards

  - Postnatal: Uncorrected WHO Child Growth standards

- `gest_days` \>= 43 weeks (301 days):

  - Birth: No standard available

  - Postnatal: Uncorrected WHO Child Growth standards

For `gigs_wlz()`, two WHO standards are available:

- The weight-for-length standard, which is applied when
  `age_days < 731`.

- The weight-for-height standard, which is applied when
  `age_days >= 731`.

## Usage

``` r
gigs_waz(weight_kg, age_days, gest_days, sex, id = NULL)

gigs_lhaz(lenht_cm, age_days, gest_days, sex, id = NULL)

gigs_wlz(weight_kg, lenht_cm, age_days, gest_days, sex, id = NULL)

gigs_hcaz(headcirc_cm, age_days, gest_days, sex, id = NULL)
```

## Arguments

- weight_kg:

  A numeric vector of length one or more with weight in kg.

- age_days:

  A numeric vector of length one or more with ages in days.

- gest_days:

  A numeric vector of length one or more with gestational ages in days.

- sex:

  Character vector of length one or more with sex(es), either `"M"`
  (male) or `"F"` (female). This argument is case-sensitive. By default,
  gigs will replace elements of `sex` which are not `"M"` or `"F"` with
  `NA` and warn you. You can customise this behaviour using the [GIGS
  package-level
  options](https://docs.ropensci.org/gigs/reference/gigs_options.md).

- id:

  A factor of length one or more with an ID for each observation, either
  ordered or unordered, containing no missing (`NA`) values. When
  supplied, `id` is used to ensure that only the earliest measurement
  for each individual is used as a birth measure. Leave this argument as
  `NULL` if all your data comes from the same individual. Default =
  `NULL`.

- lenht_cm:

  A numeric vector of length one or more with length or height in cm.
  Should be recumbent length when `age_days < 731`, and standing height
  when `age_days >= 731`.

- headcirc_cm:

  Numeric vector of length one or more with head circumference in cm.

## Value

A numeric vector of z-scores, derived using the appropriate growth
standard for each element-wise combination of `gest_days` and
`age_days`. For `gigs_wlz()`, all birth WLZs will be missing (`NA`), as
there is no INTERGROWTH-21^(st) Newborn standard for weight-for-length.

## Note

These functions expect vectors which are recyclable with
[`vctrs::vec_recycle_common()`](https://vctrs.r-lib.org/reference/vec_recycle.html).

## Examples

``` r
gest_days <- c(rep(35 * 7, 3), rep(35 * 7, 3))
age_days <- c(0, 100, 500, 2, 100, 500)
sex <- rep.int(c("M", "F"), c(3, 3))
wt_kg <- c(3, 6, 9, 3, 6, 9)
len_cm <- rep.int(c(52.2, 60.4, 75), 2)
head_cm <- rep.int(c(30, 40, 49), 2)
ids <- factor(rep.int(c("A", "B"), c(3, 3)))

# Weight-for-age z-score (WAZ)
waz <- gigs_waz(weight_kg = wt_kg,
                age_days = age_days,
                gest_days = gest_days,
                sex = sex,
                id = ids)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
print(waz)
#> [1]  1.2230003  0.7413417 -1.4866806  1.5420839  1.4395342 -0.7859202

# Note - if you don't specify 'id' you'll get different results!
waz_no_id <- gigs_waz(weight_kg = wt_kg,
                      age_days = age_days,
                      gest_days = gest_days,
                      sex = sex)
print(waz == waz_no_id)
#> [1]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE

# Length/height-for-age z-score (LHAZ)
lhaz <- gigs_lhaz(lenht_cm = len_cm,
                  age_days = age_days,
                  gest_days = gest_days,
                  sex = sex,
                  id = ids)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
print(lhaz)
#> [1]  2.8236856  0.8876444 -2.1690082  3.4154524  1.8205012 -1.4423063

# Weight-for-length/height z-score (WLZ)
#   Note: There's no at-birth standards for weight-for-length, so elements 1
#   and 4 have `NA` values
wlz <- gigs_wlz(weight_kg = wt_kg,
                lenht_cm = len_cm,
                age_days = age_days,
                gest_days = gest_days,
                sex = sex,
                id = ids)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
print(wlz)
#> [1]         NA  1.6408675 -0.6621871         NA  1.3314150 -0.1829182

# Head circumference-for-age z-score (HCAZ)
hcaz <- gigs_hcaz(headcirc_cm = head_cm,
                  age_days = age_days,
                  gest_days = gest_days,
                  sex = sex,
                  id = ids)
#> Warning: There was 1 'at birth' observation where `age_days` > 0.5.
#> ℹ This occurred for ID B.
print(hcaz)
#> [1] -1.5588136  0.9510032  1.4502711 -1.3289704  1.7433668  2.2148421
```
