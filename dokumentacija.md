# Projektni zadatak za predmet Uvod u teorijsko racunalstvo

#### Autor: [Mateo Trakostanec](https://github.com/AceTep/UTR-parsiranje)

___


### Dataset: [Journal of Climate](https://drive.google.com/file/d/1wc4Cy8wUP4ETLfy_IpzfhCwp_UHMbD6h/view?usp=drive_link)

Journal of Climate je istraživanje koje unapređuje osnovno razumijevanje dinamike i fizike klimatskog sustava na velikim prostornim razmjerima, uključujući varijabilnost atmosfere, oceana, kopnene površine i kriosfera. Prošle, sadašnje i predviđene buduće promjene u klimatskom sustavu te klimatska simulacija i predviđanje.


### Programska podrska 
Dataseti su parsirani pomocu programskog jezika python te su bile koristene biblioteke [BeautifulSoup4](https://pypi.org/project/beautifulsoup4/) i [pdfminer.six](https://pypi.org/project/pdfminer.six/). 
Ostale koristene biblioteke su [os](https://docs.python.org/3/library/os.html), [re](https://docs.python.org/3/library/re.html) [json](https://docs.python.org/3/library/json.html), [csv](https://docs.python.org/3/library/json.html), [yaml](https://pypi.org/project/PyYAML/) i [xaml](https://pypi.org/project/xaml/).

Zbog premalo prostora na merlinu prvo je potrebno extractati 7.zip koji sadrzi pdfove u working mapu

Spremljeni podaci su dostupni u varijablama te smo ih spremali u JSON, CSV, XML i YAML formate. Parsirani podaci su se spremali u 2D ili 3D liste gdje je prvi element dokument iz kojeg se sadrzaj izvlacio, a drugi element je sam izluceni sadrzaj; drugi element moze biti podnaslov dokumenta te je onda treci element sadrzaj koji je uz taj podnaslov. 

Podaci su strukturirani prema shemi te je cijeli dokument razdjeljen na vise dijelova(gdje je to moguce).
### SHEMA

| Ime stupca | Opis |
| --- | --- |
| Naslov | STRING - Naslov znanstvenog rada: `"The Large-Scale Ocean Dynamical Effect on Uncertainty in the Tropical Pacific SST Warming Pattern in CMIP5 Models"` |
| DOI | STRING - Jedinstveni identifikator rada: `"10.1175/JCLI-D-16-0318.1"` |
| Datum | DATE/STRING - Datum objave rada: `15 NOVEMBER 2016` |
| Datum Preuzimanja | DATE/STRING - Datum preuzimanja rada: `Downloaded 10/26/23 02:50 PM UTC` |
| Autorska prava  | STRING - Copyright rada: `C 2016 American Meteorological Society` |
| **Autori** i institut iz kojeg dolaze| STRING LIST - Lista autora pojedinog rada: `["JUN YING - Center for Monsoon System Research, and LASG, Institute of Atmospheric Physics, Chinese Academy of Sciences, and University of Chinese Academy of Sciences, Beijing, China", "PING HUANG"]` |
| **Sažetak** | STRING - Tekstualni sadržaj sažetka (abstract): `"This study investigates how intermodel differences in large-scale ocean dynamics affect the tropical Pacific sea surface temperature (SST) warming ..."` |
| Sadržaj | STRING - Naslov i Tekstualni sadržaj samog rada: ` 1. Introduction Obtaining accurate projections of the tropical Pacific sea surface temperature (SST) warming (TPSW) ` |
| Reference | STRING - Reference samog rada: ` REFERENCES An, S.-I., and S.-H. Im, 2014: Blunt ocean dynamical thermostat in response of tropical eastern Pacific SST to global warm- ing. Theor. Appl. Climatol., 118, 173—183, doi:10.1007/s00704-013-1048-0. ` |
|     Corresponding author address | STRING - Detalj o glavnom autoru: ` Dr. Ping Huang, Center forMonsoon System Research, Institute of Atmospheric Physics,Chinese Academy of Sciences, Bei-Er-Tiao 6, Zhong-Guan-Cun,Beijing 100190, China ` |
|   Acknowlagments| STRING - priznanja: ` The work was supported by the National Basic Research Program of China (2014CB953904 and 2012CB955604), the National Natural Science Foun- dation of China (Grants... ` |

___
### Problemi tjekom parsiranja
| Problem Description                                            | Example/Explanation                                                                                                                                                                                 |
|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Drugacije postavljeni paragrafi / span elementi                                | Pretvaranjem pdf-a u soup element moze doci do drugacije postavljenih html tagova te dolazi do greske tjekom izvlacenja podataka  |                         
| Drugo koristenje style elemenata                      | Ako se koriste dva razlicita styla za isti naslov u razlicitm dokumentima nije ih moguce dohvatiti s istim upitom te tu dolazi do greske                                                                                                        |
| Pdfovi su skenirani te je nemoguce izluciti tekst iz njih| Posto su dokumenti skenirani nije ih moguce pretvoriti u soup elemente                                                                                                                                        


### Biljeske o izlucivanju



``` markdown
1. Notes and Correspondance - Temperature Change in Eastern Minnesota
    - Skenirani dokument te iz dokumenta dobivamo jedino tekst koji se nalazi u podnozju dokumenta

2. A Detailed Cloud Fraction Climatology of the Upper Indus Basin and Its Implications for Near-Surface Air Temperature
    - Dokument nema naslov
    - Kljucni elementi fale
    - Neuspjelo parsiranje

3. Portraying the Impact of the Tibetan Plateau on Global Climate
    - Tekst je tocno izlucen
    - Sadrzi tocne autore
    - Tocno spremljen u dokument 

4. Structures and Mechanisms of Heatwaves Related to Quasi-Biweekly Variability over Southern China
    - Dokument nema naslov
    - Kljucni elementi fale
    - Neuspjelo parsiranje

5. Regimes of Diurnal Variation of Summer Rainfall over Subtropical East Asia
    - Tekst je tocno izlucen
    - Autori u krivom redosljedu, no to nije kljucan problem
    - Tocno spremljen u dokument    

6. Regional Precipitation Quantile Values for the Continental United States Compited from L-Moments
    - Skenirani dokument te iz dokumenta dobivamo jedino tekst koji se nalazi u podnozju dokumenta

7. Role of the Indian Ocean in the ENSO–Indian Summer Monsoon Teleconnectionin the NCEP Climate Forecast System
    - Tekst je tocno izlucen
    - Autori u krivom redosljedu, no to nije kljucan problem
    - Tocno spremljen u dokument    

8. Improving EnKF-Based Initialization for ENSO Prediction Using a HybridAdaptive Method
    - Tekst je tocno izlucen
    - Autori u krivom redosljedu, no to nije kljucan problem
    - Tocno spremljen u dokument  

9. A New Method for Temperature Spatial Interpolation Based on SparseHistorical Stations
    - Tekst je tocno izlucen
    - Autori u krivom redosljedu, no to nije kljucan problem
    - Tocno spremljen u dokument  
    - fali DOI

10. Spatial and Temporal Characterization of Sea Surface Temperature Responseto Tropical Cyclones*

    - Tekst je tocno izlucen
    - Autori u krivom redosljedu, no to nije kljucan problem
    - Tocno spremljen u dokument 

## Zakljucak
- 14 PDF-ova je skenirano te ih nije bilo moguce parsirati pomocu HTML parsera.
- Najcesce greske koje se pojavljuju kroz dokumente je dohvacanje naslova i sadrzaja svih elemenata. Cesto dolazi do toga da se tekst nalazi u drugacijem span elementu te ga je nemoguce dohvatiti i ostaje prazan. To se moze uociti kroz razne spremljene podatke(json, csv...). 
- Krivi poredak Autora(Autor - Fakultet, Fakulter-Auton), nije problem
- **PROBLEM 1:** U puno dokumenata se nemoze dohvatiti podnaslov + sadrzaj i ostali kljucni elementi.
- **PROBLEM 2:** U dosta dokumenata nije moguce dohvatiti naslov. Treba popraviti dalje.
- **PROBLEM 3:** U formate(json,csv,xml,yamk) je spremljeno samo 50 od 110 dokumenata, treba detaljnije istraziti zasto

```
