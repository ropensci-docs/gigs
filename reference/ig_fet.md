# INTERGROWTH-21^(st) Fetal Standards growth curve data

A set of nested lists containing tables with reference values at
different z-scores/centiles for valid gestational ages in days. The list
is ordered by acronym first, then by z-score/centile (as available -
some Fetal standards only have centile tables).

## Source

[INTERGROWTH-21^(st) Pregnancy Dating
(CRL)](https://intergrowth21.com/tools-resources/pregnancy-dating/)

[INTERGROWTH-21^(st) Symphysis-Fundal Height
standard](https://intergrowth21.com/tools-resources/symphysis-fundal-height/)

[INTERGROWTH-21^(st) Fetal Growth
standards](https://intergrowth21.com/tools-resources/fetal-growth/)

[INTERGROWTH-21^(st) Fetal Doppler
standards](https://intergrowth21.com/tools-resources/fetal-doppler/)

[INTERGROWTH-21^(st) Gestational Weight Gain
standard](https://intergrowth21.com/tools-resources/gestational-weight-gain/)

## Note

Where possible, tables were taken from the online sources here. If not
available on the INTERGROWTH-21^(st) website, they were taken from the
publications listed here.

## References

Papageorghiou AT, Ohuma EO, Altman DG, Todros T, Cheikh Ismail L,
Lambert A et al. **International standards for fetal growth based on
serial ultrasound measurements: the Fetal Growth Longitudinal Study of
the INTERGROWTH-21st Project.** *Lancet* 2014, **384(9946):869-79.**
[doi:10.1016/S0140-6736(14)61490-2](https://doi.org/10.1016/S0140-6736%2814%2961490-2)

Stirnemann J, Villar J, Salomon LJ, Ohuma EO, Lamber A, Victoria CG et
al. **International Estimated Fetal Weight Standards of the
INTERGROWTH-21st Project.** *Ultrasound Obstet Gynecol* 2016,
**49:478-486**
[doi:10.1002/uog.17347](https://doi.org/10.1002/uog.17347)

Stirnemann J, Salomon LJ, Papageorghiou AT. **INTERGROWTH-21st standards
for Hadlock's estimation of fetal weight.** *Ultrasound Obstet Gynecol*
2020, **56(6):946-948**
[doi:10.1002/uog.22000](https://doi.org/10.1002/uog.22000)

Papageorghiou AT, Ohuma EO, Gravett MG, Lamber A, Noble JA, Pang R et
al. **International standards for symphysis-fundal height based on
serial measurements from the Fetal Growth Longitudinal Study of the
INTERGROWTH-21st Project: prospective cohort study in eight countries.**
*BMJ* 2016, **355:i5662**
[doi:10.1136/bmj.i5662](https://doi.org/10.1136/bmj.i5662)

Papageorghiou AT, Kennedy SH, Salomon LJ, Ohuma EO, Cheikh Ismail L,
Barros FC et al. **International standards for early fetal size and
pregnancy dating based on ultrasound measurement of crown-rump length in
the first trimester of pregnancy.** *Ultrasound Obstet Gynecol* 2014,
**44(6):641-48**
[doi:10.1002/uog.13448](https://doi.org/10.1002/uog.13448)

Cheikh Ismail L, Bishop DC, Pang R, Ohuma EO, Kac G, Abrams B et al.
**Gestational weight gain standards based on women enrolled in the Fetal
Growth Longitudinal Study of the INTERGROWTH-21st Project: a prospective
longitudinal cohort study.** *BMJ* 2016, **352:i555**
[doi:10.1136/bmj.i555](https://doi.org/10.1136/bmj.i555)

Drukker L, Staines-Urias E, Villar J, Barros FC, Carvalho M, Munim S et
al. **International gestational age-specific centiles for umbilical
artery Doppler indices: a longitudinal prospective cohort study of the
INTERGROWTH-21st Project.** *Am J Obstet Gynecol* 2021,
**222(6):602.e1-602.e15**
[doi:10.1016/j.ajog.2020.01.012](https://doi.org/10.1016/j.ajog.2020.01.012)

Rodriguez-Sibaja MJ, Villar J, Ohuma EO, Napolitano R, Heyl S, Carvalho
M et al. **Fetal cerebellar growth and Sylvian fissure maturation:
international standards from Fetal Growth Longitudinal Study of
INTERGROWTH-21st Project** *Ultrasound Obstet Gynecol* 2021,
**57(4):614-623**
[doi:10.1002/uog.22017](https://doi.org/10.1002/uog.22017)

Napolitano R, Molloholli M, Donadono V, Ohuma EO, Wanyonyi SZ, Kemp B et
al. **International standards for fetal brain structures based on serial
ultrasound measurements from Fetal Growth Longitudinal Study of
INTERGROWTH-21st Project** *Ultrasound Obstet Gynecol* 2020,
**56(3):359-370**
[doi:10.1002/uog.21990](https://doi.org/10.1002/uog.21990)

## Examples

``` r
names(gigs::ig_fet)
#>  [1] "hcfga"   "bpdfga"  "acfga"   "flfga"   "ofdfga"  "efwfga"  "sfhfga" 
#>  [8] "crlfga"  "gafcrl"  "gwgfga"  "pifga"   "rifga"   "sdrfga"  "tcdfga" 
#> [15] "gaftcd"  "poffga"  "sffga"   "avfga"   "pvfga"   "cmfga"   "hefwfga"
head(gigs::ig_fet$hcfga$zscores)
#>   gest_days SD3neg SD2neg SD1neg   SD0   SD1   SD2   SD3
#> 1        98   81.1   86.7   92.3  97.9 103.5 109.0 114.6
#> 2       105   92.6   98.5  104.4 110.4 116.3 122.2 128.2
#> 3       112  104.1  110.4  116.6 122.9 129.2 135.5 141.7
#> 4       119  115.7  122.3  128.8 135.4 142.0 148.6 155.2
#> 5       126  127.2  134.1  141.0 147.9 154.8 161.7 168.6
#> 6       133  138.7  145.9  153.1 160.3 167.4 174.6 181.8
```
