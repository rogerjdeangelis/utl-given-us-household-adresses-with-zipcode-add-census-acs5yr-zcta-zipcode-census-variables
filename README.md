# utl-given-us-household-adresses-with-zipcode-add-census-acs5yr-zcta-zipcode-census-variables
Given us household adresses with zipcode add census acs5yr zcta zipcode census variables
    %let pgm=utl-given-us-household-adresses-with-zipcode-add-census-acs5yr-zcta-zipcode-census-variables;

    %stop_submission;

    Given us household adresses with zipcode add census acs5yr zcta zipcode census variables

           CONTENTS

              1 Add zcta level census acs variables to US address database
              2 Label acs variables
              3 Related repos

    NO API NEEDED AND NO RESTRICTIONS

    github
    https://tinyurl.com/puzwf725
    https://github.com/rogerjdeangelis/utl-given-us-household-adresses-with-zipcode-add-census-acs5yr-zcta-zipcode-census-variables

    related repos
    https://tinyurl.com/3js4vmrv
    https://github.com/rogerjdeangelis/utl-given-us-household-adresses-with-geoid-and-census-track-add-acs-census-variables

    https://tinyurl.com/4f5cjxun
    https://communities.sas.com/t5/SAS-Procedures/Convert-Lat-Long-to-Census-Tract/m-p/837174#M82117

    PREP

    You need to download
     ZCTA CENSUS ACS ZCTA(approx zipcodes)
     https://tinyurl.com/58d8y3fv
     download  https://mcdc.missouri.edu/data/acs2020/uszctas5yr.sas7bdat


     RELATED DOWNLOADS

      ADDRESS DATA BASE (use this address instead of the 141 million (there where address repeated wiver very minor lat log, I averaged them)

          1  download adr_fix132e6.exe 1432 million addresses (1.45gb win10) into d:/adr/exe/adr_fix132e6.exe (all have the same data)
             https://1drv.ms/u/c/bb0f3c4c9b1dc58b/EeJAnwdAgy9Oo1C4IIzf_VIBVcUhQGZRHBZZ2ulv0gICSQ?e=LXtbdk
             https://drive.google.com/file/d/1j3u9g9X4t5GYoz4O62oEs63RVp_qSlhq/view?usp=drive_link
             https://www.dropbox.com/scl/fi/hijvujwjotftaqiu93dgt/adr_fix132e6.exe?rlkey=efa8b49x52tpc25kz1vloc06g&st=f8insd26&dl=0

          2  Unzip the self extracting 7-zip file you downloaded save in d:/adr/csv/adr_fix132e6.csv
             Just click on the exe file (131,789,977 records)

          3  proc datasets code to label all acs5yr variables (except MOE variables)

         BLOCK GROUP CENSUS ACS 5YR ALL VARIABLES block group level (SAS DATASET)

             https://tinyurl.com/yc87r36p
             https://mcdc.missouri.edu/cgi-bin/broker?_PROGRAM=utils.uex2dex.sas&path=/data/acs2020&dset=variables5yr

             or self extracting 7-zip
             https://1drv.ms/u/c/bb0f3c4c9b1dc58b/Ea6i-HzmUa5MhassZDRQII0BX_pprBA5Zf3hDiOz23h9KA?e=rqVvfo
             https://drive.google.com/file/d/1UwVNFONyuI7H1mCqDVuPOYbnpvEkFdxB/view?usp=sharing
             https://www.dropbox.com/scl/fi/yifs4uw9o0405a76e9lgb/acs5yr.exe?rlkey=nfvddmf4cgqae9x4sudwxycnv&st=wygkkhfz&dl=0


         TRACT CENSUS ACS 5YR ALL VARIABLES track level (SAS DATASET same as above))

            university of Missouri ACS Track level data
            https://tinyurl.com/33j47jus
            https://mcdc.missouri.edu/cgi-bin/broker?_PROGRAM=utils.uex2dex.sas&path=/data/acs2020&dset=ustracts5yr&view=0


         ZCTA CENSUS ACS ZCTA(approx zipcodes)

          https://mcdc.missouri.edu/data/acs2020/
          download  https://mcdc.missouri.edu/data/acs2020/uszctas5yr.sas7bdat


    Related repo
    https://tinyurl.com/4f5cjxun
    https://communities.sas.com/t5/SAS-Procedures/Convert-Lat-Long-to-Census-Tract/m-p/837174#M82117

    FYI GEOID BREAKDOWM

    110010095101234

    11  001  009510 1234

    The GEOID is a concatenated numeric code that uniquely identifies geographic areas.
    The hierarchy follows this structure:

    11        = Washington DCState FIPS Code: 2 digits
    001       = County FIPS Code: 3 digits
    009510    = Census Tract Number: 6 digits
    009510    = Block Number: 4 digits


    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|



    /*****************************************************************************************************************************************************************************************/
    /*                       INPUT                                        |          PROCESS               |                               OUTPUT                                            */
    /*                       =====                                        |          =======               |                               ======                                            */
    /*                                                                    |                                |                                                                                 */
    /* STATE ZIPCODE   LAT      LON   ADR                                 | proc sql;                      |  Middle Observation(12 ) want - Total Obs 24                                    */
    /*                                                                    | create                         |                                                                                 */
    /*   IN   46701  41.3513  -85.441 0008 S COUNTY RD 50 W 46701         |    table want as               |                                                                                 */
    /*   NC   28277  35.0259  -80.834 10790 ESSEX HALL DR CHARLOTTE 28277 | select                         |   -- CHARACTER --                                                               */
    /*   VT   05343  43.0729  -72.747 115 PINEAPPLE HL LN 05343           |    l.state as stateabv         |  VariableTyp    Value               Label                                       */
    /*   MD   21136  39.4428  -76.806 125 SHETLAND CIR 21136              |   ,l.lat                       |                                                                                 */
    /*   CA   92335  34.0711 -117.501 13910 VLY BLVD 92335                |   ,l.lon                       |  STATEABV C2    OH                  STATEABV                                    */
    /*   FL   32908  27.9204  -80.716 1522 SW KAPLAN ST 32908             |   ,l.adr                       |  ADR      C44   547 N WELL ST 43605 ADR                                         */
    /*   TX   78861  29.6198  -99.283 1700 CRK 121 78861                  |   ,r.*                         |  SUMLEV   C3    860                 SUMLEV                                      */
    /*   IL   61284  41.3871  -90.830 19004 134TH AVE W 61284             | from                           |  STATE    C2    39                  Primary state                               */
    /*   KS   66532  39.7859  -95.322 207 CHERRY ST 66532                 |    sd1.have as l               |  ZCTA5    C5    43605               ZIP Census Tabulation Area                  */
    /*   NY   10705  40.9233  -73.892 224 PARK HILL AVE 10705             | left                           |  ZIPNAME  C40   Toledo, OH          ZIPNAME                                     */
    /*   FL   33565  28.0788  -82.102 2501 E KNIGHTS GRIFFIN RD 33565     |   join acssd1.uszctas5yr as r  |  COUNTY   C5    39095               COUNTY                                      */
    /*   MI   48174  42.1590  -83.313 28055 BREDOW AVE 48174              | on                             |  FIPCO    C5    39095               Primary County                              */
    /*   IL   61242  41.6782  -90.328 303 2ND ST S 61242                  |    l.zipcode = r.zcta5         |  FIPCO2   C5    39173               FIPCO2                                      */
    /*   NY   14738  42.0310  -79.063 32 WHEELER HILL RD 14738            | ;quit;                         |  ALTZIPS  C72                       Alternate ZIP codes associated              */
    /*   ME   04444  44.7495  -68.880 36 EMERSON ML RD 04444              |                                |  STAB     C2    OH                  STAB                                        */
    /*   NJ   08226  39.2659  -74.593 409 21TH ST 08226                   |                                |  ESRIID   C22   43605               ESRIID                                      */
    /*   CO   80917  38.8964 -104.725 4480 CHAPARRAL RD 80917             |                                |  VINTAGE  C4    2020                VINTAGE                                     */
    /*   NE   68003  41.0434  -96.374 501 N 19TH ST 68003                 |                                |  PERIOD   C3    5yr                 PERIOD                                      */
    /*   OH   43605  41.6617  -83.488 547 N WHEELING ST 43605             |                                |  GEOID    C40   86000US43605        GEOID                                       */
    /*   WI   54612  44.2508  -91.491 609 MAIN ST 54612                   |                                |  AREANAME C150  ZCTA 43605          AREANAME                                    */
    /*   WI   53511  42.5562  -89.134 6734 W CLEOPHAS RD 53511            |                                |  COUSUBFP C5                        County subdivision (town) code              */
    /*   MA   02191  42.2405  -70.942 73 NCK ST 02191                     |                                |  PLACEFP  C5                        PLACEFP                                     */
    /*   TN   37115  36.2644  -86.748 818 TUCKAHOE DR 37115               |                                |  CBSA     C5                        CBSA                                        */
    /*   NV   89523  39.5253 -119.950 9095 CABIN CRK TRL 89523            |                                |  CBSATYPE C5                        CBSATYPE                                    */
    /*                                                                    |                                |  METDIV   C5                        Metro Div.                                  */
    /* libname acssd1 "d:/acs/sd1";                                       |                                |  CSA      C3                        Consolidated Stat Area                      */
    /* libname adrsd1 "d:/adr/sd1";                                       |                                |  NECTA    C5                        New England City/Town Area                  */
    /*                                                                    |                                |  UA       C5                        Urban Area/Cluster                          */
    /* options validvarname=upcase;                                       |                                |  PUMA     C5                        PUMA                                        */
    /* libname sd1 "d:/sd1";                                              |                                |  SDELM    C5                        SDELM                                       */
    /* data sd1.have ;                                                    |                                |  SDSEC    C5                        SDSEC                                       */
    /*  informat state $2. zipcode $5. lat 8. lon 8. adr $44.;            |                                |  SDUNI    C5                        Unified School District                     */
    /* input STATE LAT LON ZIPCODE ADR &;                                 |                                |  REGION   C1                        REGION                                      */
    /* cards4;                                                            |                                |  DIVISION C1                        DIVISION                                    */
    /* IN 41.3513 -85.441 46701 0008 S COUNTY RD 50 W 46701               |                                |  CONGDIST C2                        116th Congressional District                */
    /* NC 35.0259 -80.834 28277 10790 ESSEX HALL DR CHARLOTTE 28277       |                                |  CBSAYR   C4                        CBSAYR                                      */
    /* VT 43.0729 -72.747 05343 115 PINEAPPLE HL LN 05343                 |                                |  CONCIT   C5                        CONCIT                                      */
    /* MD 39.4428 -76.806 21136 125 SHETLAND CIR 21136                    |                                |  AIANHHFP C5                        AIANHHFP                                    */
    /* CA 34.0711 -117.501 92335 13910 VLY BLVD 92335                     |                                |  AIHHTLI  C1                        AIHHTLI                                     */
    /* FL 27.9204 -80.716 32908 1522 SW KAPLAN ST 32908                   |                                |  AITS     C5                        AITS                                        */
    /* TX 29.6198 -99.283 78861 1700 CRK 121 78861                        |                                |  ANRC     C5                        ANRC                                        */
    /* IL 41.3871 -90.830 61284 19004 134TH AVE W 61284                   |                                |  MACC     C1                        MACC                                        */
    /* KS 39.7859 -95.322 66532 207 CHERRY ST 66532                       |                                |  MEMI     C1                        MEMI                                        */
    /* NY 40.9233 -73.892 10705 224 PARK HILL AVE 10705                   |                                |  CNECTA   C3                        CNECTA                                      */
    /* FL 28.0788 -82.102 33565 2501 E KNIGHTS GRIFFIN RD 33565           |                                |  NECTADIV C5                        NECTADIV                                    */
    /* MI 42.1590 -83.313 48174 28055 BREDOW AVE 48174                    |                                |  SLDL     C3                        State Legislative District - Lower Chamb    */
    /* IL 41.6782 -90.328 61242 303 2ND ST S 61242                        |                                |  SLDU     C3                        State Legislative District - Upper Chamb    */
    /* NY 42.0310 -79.063 14738 32 WHEELER HILL RD 14738                  |                                |  SUBMCD   C5                        SUBMCD                                      */
    /* ME 44.7495 -68.880 04444 36 EMERSON ML RD 04444                    |                                |  UR       C1                        UR                                          */
    /* NJ 39.2659 -74.593 08226 409 21TH ST 08226                         |                                |  PCIND    C1                        PCIND                                       */
    /* CO 38.8964 -104.725 80917 4480 CHAPARRAL RD 80917                  |                                |  AIANHH   C8                        AIANHH                                      */
    /* NE 41.0434 -96.374 68003 501 N 19TH ST 68003                       |                                |  UACP     C1                        UA central place                            */
    /* OH 41.6617 -83.488 43605 547 N WHEELING ST 43605                   |                                |  TRACT    C7                        TRACT                                       */
    /* WI 44.2508 -91.491 54612 609 MAIN ST 54612                         |                                |  BG       C1                        BG                                          */
    /* WI 42.5562 -89.134 53511 6734 W CLEOPHAS RD 53511                  |                                |                                                                                 */
    /* MA 42.2405 -70.942 02191 73 NCK ST 02191                           |                                |   -- NUMERIC --                                                                 */
    /* TN 36.2644 -86.748 37115 818 TUCKAHOE DR 37115                     |                                |  LAT      N8         41.6617        LAT                                         */
    /* NV 39.5253 -119.950 89523 9095 CABIN CRK TRL 89523                 |                                |  LON      N8         -83.488        LON                                         */
    /* ;;;;                                                               |                                |  PCTCNTY  N8    99.357891083        PCTCNTY                                     */
    /* run;quit;                                                          |                                |  PCTSTATE N8             100        % of ZCTAs total pop in primary State       */
    /*                                                                    |                                |  NALTZIPS N3               0        # of alternative ZIP codes                  */
    /*                                                                    |                                |  INTPTLAT N8      41.6408507        INTPTLAT                                    */
    /*                                                                    |                                |  INTPTLON N8     -83.5115392        INTPTLON                                    */
    /*                                                                    |                                |  LANDSQMI N8    7.0469168197        Land Area Sq. Miles                         */
    /*                                                                    |                                |  AREASQMI N8    8.0753706195        Total Area Sq Mls                           */
    /*                                                                    |                                |  TOTPOPSF1N8           28346        2010 Census total population                */
    /*                                                                    |                                |  LOGRECNO N8           24711        LOGRECNO                                    */
    /*                                                                    |                                |  TOTPOP   N5           25843        Total population                            */
    /*                                                                    |                                |  AGE0_4   N5            2474        Under 5 years                               */
    /*****************************************************************************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    libname acssd1 "d:/acs/sd1";
    libname adrsd1 "d:/adr/sd1";

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have ;
     informat state $2. zipcode $5. lat 8. lon 8. adr $44.;
    input STATE LAT LON ZIPCODE ADR &;
    cards4;
    IN 41.3513 -85.441 46701 0008 S COUNTY RD 50 W 46701
    NC 35.0259 -80.834 28277 10790 ESSEX HALL DR CHARLOTTE 28277
    VT 43.0729 -72.747 05343 115 PINEAPPLE HL LN 05343
    MD 39.4428 -76.806 21136 125 SHETLAND CIR 21136
    CA 34.0711 -117.501 92335 13910 VLY BLVD 92335
    FL 27.9204 -80.716 32908 1522 SW KAPLAN ST 32908
    TX 29.6198 -99.283 78861 1700 CRK 121 78861
    IL 41.3871 -90.830 61284 19004 134TH AVE W 61284
    KS 39.7859 -95.322 66532 207 CHERRY ST 66532
    NY 40.9233 -73.892 10705 224 PARK HILL AVE 10705
    FL 28.0788 -82.102 33565 2501 E KNIGHTS GRIFFIN RD 33565
    MI 42.1590 -83.313 48174 28055 BREDOW AVE 48174
    IL 41.6782 -90.328 61242 303 2ND ST S 61242
    NY 42.0310 -79.063 14738 32 WHEELER HILL RD 14738
    ME 44.7495 -68.880 04444 36 EMERSON ML RD 04444
    NJ 39.2659 -74.593 08226 409 21TH ST 08226
    CO 38.8964 -104.725 80917 4480 CHAPARRAL RD 80917
    NE 41.0434 -96.374 68003 501 N 19TH ST 68003
    OH 41.6617 -83.488 43605 547 N WHEELING ST 43605
    WI 44.2508 -91.491 54612 609 MAIN ST 54612
    WI 42.5562 -89.134 53511 6734 W CLEOPHAS RD 53511
    MA 42.2405 -70.942 02191 73 NCK ST 02191
    TN 36.2644 -86.748 37115 818 TUCKAHOE DR 37115
    NV 39.5253 -119.950 89523 9095 CABIN CRK TRL 89523
    ;;;;
    run;quit;

    /*             _     _                            _        ____       _       _
    / |   __ _  __| | __| |   __ _  ___ ___   _______| |_ __ _| ___|   __| | __ _| |_ __ _
    | |  / _` |/ _` |/ _` |  / _` |/ __/ __| |_  / __| __/ _` |___ \  / _` |/ _` | __/ _` |
    | | | (_| | (_| | (_| | | (_| | (__\__ \  / / (__| || (_| |___) || (_| | (_| | || (_| |
    |_|  \__,_|\__,_|\__,_|  \__,_|\___|___/ /___\___|\__\__,_|____/  \__,_|\__,_|\__\__,_|

    */
    proc sql;
    create
       table want as
    select
       l.state as stateabv
      ,l.lat
      ,l.lon
      ,l.adr
      ,r.*
    from
       sd1.have as l
    left
      join acssd1.uszctas5yr as r
    on
       l.zipcode = r.zcta5
    ;quit;


    /**************************************************************************************************************************/
    /*  Middle Observation(9 ) of table = want - Total Obs 19                                                                 */
    /*                                                                                                                        */
    /*  -- CHARACTER --                                                                                                       */
    /* Variable                        Typ    Value                      Label                                                */
    /*                                                                                                                        */
    /* STATEABV                         C2    OH                         STATEABV                                             */
    /* ADR                              C44   547 N WHEELING ST 43605    ADR                                                  */
    /* SUMLEV                           C3    860                        SUMLEV                                               */
    /* STATE                            C2    39                         Primary state                                        */
    /* ZCTA5                            C5    43605                      ZIP Census Tabulation Area                           */
    /* ZIPNAME                          C40   Toledo, OH                 ZIPNAME                                              */
    /* COUNTY                           C5    39095                      COUNTY                                               */
    /* FIPCO                            C5    39095                      Primary County                                       */
    /* FIPCO2                           C5    39173                      FIPCO2                                               */
    /* ALTZIPS                          C72                              Alternate ZIP codes associated with this             */
    /* STAB                             C2    OH                         STAB                                                 */
    /* ESRIID                           C22   43605                      ESRIID                                               */
    /* VINTAGE                          C4    2020                       VINTAGE                                              */
    /* PERIOD                           C3    5yr                        PERIOD                                               */
    /* GEOID                            C40   86000US43605               GEOID                                                */
    /* AREANAME                         C150  ZCTA 43605                 AREANAME                                             */
    /* COUSUBFP                         C5                               County subdivision (town) code                       */
    /* PLACEFP                          C5                               PLACEFP                                              */
    /* CBSA                             C5                               CBSA                                                 */
    /* CBSATYPE                         C5                               CBSATYPE                                             */
    /* METDIV                           C5                               Metro Div.                                           */
    /* CSA                              C3                               Consolidated Stat Area                               */
    /* NECTA                            C5                               New England City/Town Area                           */
    /* UA                               C5                               Urban Area/Cluster                                   */
    /* PUMA                             C5                               PUMA                                                 */
    /* SDELM                            C5                               SDELM                                                */
    /* SDSEC                            C5                               SDSEC                                                */
    /* SDUNI                            C5                               Unified School District                              */
    /* REGION                           C1                               REGION                                               */
    /* DIVISION                         C1                               DIVISION                                             */
    /* CONGDIST                         C2                               116th Congressional District                         */
    /* CBSAYR                           C4                               CBSAYR                                               */
    /* CONCIT                           C5                               CONCIT                                               */
    /* AIANHHFP                         C5                               AIANHHFP                                             */
    /* AIHHTLI                          C1                               AIHHTLI                                              */
    /* AITS                             C5                               AITS                                                 */
    /* ANRC                             C5                               ANRC                                                 */
    /* MACC                             C1                               MACC                                                 */
    /* MEMI                             C1                               MEMI                                                 */
    /* CNECTA                           C3                               CNECTA                                               */
    /* NECTADIV                         C5                               NECTADIV                                             */
    /* SLDL                             C3                               State Legislative District - Lower Chamb             */
    /* SLDU                             C3                               State Legislative District - Upper Chamb             */
    /* SUBMCD                           C5                               SUBMCD                                               */
    /* UR                               C1                               UR                                                   */
    /* PCIND                            C1                               PCIND                                                */
    /* AIANHH                           C8                               AIANHH                                               */
    /* UACP                             C1                               UA central place                                     */
    /* TRACT                            C7                               TRACT                                                */
    /* BG                               C1                               BG                                                   */
    /*                                                                                                                        */
    /*   -- NUMERIC --                                                                                                        */
    /*  LAT                              N8         38.9146               LAT                                                 */
    /*  LON                              N8        -77.0274               LON                                                 */
    /*  LOGRECNO                         N8              84               LOGRECNO                                            */
    /*  LANDSQMI                         N8           0.106               Land area (square miles)                            */
    /*  AREASQMI                         N8           0.106               Total area (square miles)                           */
    /*  INTPTLAT                         N8      38.9155152               INTPTLAT                                            */
    /*  INTPTLON                         N8     -77.0270354               INTPTLON                                            */
    /*  TOTPOP                           N5            2517               Total population                                    */
    /*  AGE0_4                           N5             161               Under 5 years                                       */
    /*  PCTAGE0_4                        N4    6.3999977112               Under 5 years                                       */
    /*  AGE5_9                           N5              58               5 to 9 years                                        */
    /*  PCTAGE5_9                        N4    2.2999992371               5 to 9 years                                        */
    /*  AGE10_14                         N5               2               10 to 14 years                                      */
    /*  PCTAGE10_14                      N4    0.0999999642               10 to 14 years                                      */
    /*  AGE15_19                         N5              32               15 to 19 years                                      */
    /*  PCTAGE15_19                      N4    1.2999992371               15 to 19 years                                      */
    /*  AGE20_24                         N5             308               20 to 24 years                                      */
    /*  PCTAGE20_24                      N4    12.199996948               20 to 24 years                                      */
    /*  AGE25_34                         N5             764               25 to 34 years                                      */
    /*  PCTAGE25_34                      N4    30.399993896               25 to 34 years                                      */
    /*  AGE35_44                         N5             286               35 to 44 years                                      */
    /*  PCTAGE35_44                      N4    11.399993896               35 to 44 years                                      */
    /*  AGE45_54                         N5             274               45 to 54 years                                      */
    /*  PCTAGE45_54                      N4    10.899993896               45 to 54 years                                      */
    /*  AGE55_59                         N5             185               55 to 59 years                                      */
    /*  PCTAGE55_59                      N4    7.3999977112               55 to 59 years                                      */
    /*  AGE60_64                         N5             198               60 to 64 years                                      */
    /*  PCTAGE60_64                      N4    7.8999977112               60 to 64 years                                      */
    /*  AGE65_74                         N5             199               65 to 74 years                                      */
    /*  PCTAGE65_74                      N4    7.8999977112               65 to 74 years                                      */
    /*  AGE75_84                         N5              50               75 to 84 years                                      */
    /*  PCTAGE75_84                      N4               2               75 to 84 years                                      */
    /*  OVER85                           N5               0               85 years and over                                   */
    /*  PCTOVER85                        N4               0               85 years and over                                   */
    /*  MEDIANAGE                        N4    34.599975586               Median age in years                                 */
    /*  OVER5                            N5               .               Population 5 years and over                         */
    /*  PCTOVER5                         N4               .               Population 5 years and over                         */
    /*  OVER15                           N5            2296               Persons 15 years and over                           */
    /*  PCTOVER15                        N4    91.199951172               15 years and over                                   */
    /*  UNDER18                          N5             251               Under 18 years of age                               */
    /*  PCTUNDER18                       N4              10               Under 18 years of age                               */
    /*  OVER18                           N5            2266               18 years and over                                   */
    /*  PCTOVER18                        N4              90               18 years and over                                   */
    /*  OVER21                           N5            2059               21 years and over                                   */
    /*  PCTOVER21                        N4    81.799987793               21 years and over                                   */
    /*  OVER25                           N5            1956               Population 25 years and over                        */
    /*  PCTOVER25                        N4    77.699951172               25 years and over                                   */
    /*  OVER62                           N5             401               62 years and over                                   */
    /*  PCTOVER62                        N4    15.899993896               62 years and over                                   */
    /*  OVER65                           N5             249               65 years and over                                   */
    /*  PCTOVER65                        N4    9.8999938965               65 years and over                                   */
    /*  MALES                            N5            1238               Male                                                */
    /*  PCTMALES                         N4    49.199981689               Male                                                */
    /*  OVER18MALES                      N5            1084               18 years old and over                               */
    /*  PCTOVER18MALES                   N4    87.599975586               18 years old and over                               */
    /*  OVER65MALES                      N5             144               65 years old and over                               */
    /*  PCTOVER65MALES                   N4    11.599998474               65 years old and over                               */
    /*  FEMALES                          N5            1279               Female                                              */
    /*  PCTFEMALES                       N4    50.799987793               Female                                              */
    /*  OVER18FEMALES                    N5            1182               18 years old and over                               */
    /*  PCTOVER18FEMALES                 N4    92.399963379               18 years old and over                               */
    /*  OVER65FEMALES                    N5             105               65 years old and over                               */
    /*  PCTOVER65FEMALES                 N4    8.1999969482               65 years old and over                               */
    /*  ONERACE                          N5            2095               One race                                            */
    /*  PCTONERACE                       N4    83.199951172               One race                                            */
    /*  WHITE1                           N5            1286               White alone                                         */
    /*  PCTWHITE1                        N4    51.099975586               White alone                                         */
    /*  BLACK1                           N5             560               Black or African American                           */
    /*  PCTBLACK1                        N4    22.199996948               Black or African American                           */
    /*  INDIAN1                          N5               0               American Indian and Alaska Native                   */
    /*  PCTINDIAN1                       N4               0               American Indian and Alaska Native                   */
    /*  ASIAN1                           N5             100               Asian                                               */
    /*  PCTASIAN1                        N4               4               Asian                                               */
    /*  HAWNPI1                          N5               0               Native Hawaiian and Other Pacific Island            */
    /*  PCTHAWNPI1                       N4               0               Native Hawaiian and Other Pacific Island            */
    /*  OTHER1                           N5             149               Some other race                                     */
    /*  PCTOTHER1                        N4    5.8999977112               Some other race                                     */
    /*  MULTIRACE                        N5             422               Two or more races                                   */
    /*  PCTMULTIRACE                     N4    16.799987793               Two or more races                                   */
    /*  WHITE2                           N5            1320               White (alone or in combination)                     */
    /*  PCTWHITE2                        N4    52.399993896               White (alone or in combination)                     */
    /*  BLACK2                           N5             970               Black (alone or in combination)                     */
    /*  PCTBLACK2                        N4            38.5               Black (alone or in combination)                     */
    /*  INDIAN2                          N5             388               American Indian (alone or in combination            */
    /*  PCTINDIAN2                       N4    15.399993896               American Indian (alone or in combination            */
    /*  ASIAN2                           N5             107               Asian (alone or in combination)                     */
    /*  PCTASIAN2                        N4    4.2999992371               Asian (alone or in combination)                     */
    /*  HAWNPI2                          N5               0               Native Hawaiian (alone or in combination            */
    /*  PCTHAWNPI2                       N4               0               Native Hawaiian (alone or in combination            */
    /*  OTHER2                           N5             154               Some other race (alone or in combination            */
    /*  PCTOTHER2                        N4    6.0999984741               Some other race (alone or in combination            */
    /*  HISPANICPOP                      N5             129               Hispanic or Latino of any race                      */
    /*  PCTHISPANICPOP                   N4    5.0999984741               Hispanic or Latino of any race                      */
    /*  NONHISPPOP                       N5            2388               Not Hispanic or Latino                              */
    /*  PCTNONHISPPOP                    N4    94.899963379               Not Hispanic or Latino                              */
    /*  NONHISPWHITE                     N5            1274               White alone                                         */
    /*  PCTNONHISPWHITE                  N4    50.599975586               White alone                                         */
    /*  NONHISPBLACK                     N5             560               Black or African American alone                     */
    /*  PCTNONHISPBLACK                  N4    22.199996948               Black or African American alone                     */
    /*  NONHISPAMIND                     N5               0               American Indian and Alaska Native alone             */
    /*  PCTNONHISPAMIND                  N4               0               American Indian and Alaska Native alone             */
    /*  NONHISPASIAN                     N5             100               Asian alone                                         */
    /*  PCTNONHISPASIAN                  N4               4               Asian alone                                         */
    /*  NONHISPHAWNPI                    N5               0               Native Hawaiian and Other Pacific Island            */
    /*  PCTNONHISPHAWNPI                 N4               0               Native Hawaiian and Other Pacific Island            */
    /*  TOTHHS                           N5             929               Total households                                    */
    /*  HHINC0                           N5              20               Less than $10,000                                   */
    /*  PCTHHINC0                        N4    2.1999988556               Less than $10,000                                   */
    /*  HHINC10                          N5              11               $10,000 to $14,999                                  */
    /*  PCTHHINC10                       N4    1.1999998093               $10,000 to $14,999                                  */
    /*  HHINC15                          N5               0               $15,000 to $24,999                                  */
    /*  PCTHHINC15                       N4               0               $15,000 to $24,999                                  */
    /*  HHINC25                          N5              74               $25,000 to $34,999                                  */
    /*  PCTHHINC25                       N4               8               $25,000 to $34,999                                  */
    /*  HHINC35                          N5               0               $35,000 to $49,999                                  */
    /*  PCTHHINC35                       N4               0               $35,000 to $49,999                                  */
    /*  HHINC50                          N5              79               $50,000 to $74,999                                  */
    /*  PCTHHINC50                       N4             8.5               $50,000 to $74,999                                  */
    /*  HHINC75                          N5             138               $75,000 to $99,999                                  */
    /*  PCTHHINC75                       N4    14.899993896               $75,000 to $99,999                                  */
    /*  HHINC100                         N5             168               $100,000 to $149,999                                */
    /*  PCTHHINC100                      N4    18.099990845               $100,000 to $149,999                                */
    /*  HHINC150                         N5             157               $150,000 to $199,999                                */
    /*  PCTHHINC150                      N4    16.899993896               $150,000 to $199,999                                */
    /*  HHINC200                         N5             282               $200,000 or more                                    */
    /*  PCTHHINC200                      N4    30.399993896               $200,000 or more                                    */
    /*  NUMHHEARNINGS                    N5             816               With earnings                                       */
    /*  PCTNUMHHEARNINGS                 N4    87.799987793               With earnings                                       */
    /*  NUMHHSOCSEC                      N5             113               With social security                                */
    /*  PCTNUMHHSOCSEC                   N4    12.199996948               With social security                                */
    /*  NUMHHRETINC                      N5             190               With retirement income                              */
    /*  PCTNUMHHRETINC                   N4            20.5               With retirement income                              */
    /*  NUMHHSUPPSECINC                  N5              68               With supplemental security income                   */
    /*  PCTNUMHHSUPPSECINC               N4    7.2999992371               With supplemental security income                   */
    /*  NUMHHPUBASSIST                   N5              32               With cash public assistance income                  */
    /*  PCTNUMHHPUBASSIST                N4    3.3999996185               With cash public assistance income                  */
    /*  NUMHHFOODSTMP                    N5              43               With food stamp benefits in the past 12             */
    /*  PCTNUMHHFOODSTMP                 N4    4.5999984741               With food stamp benefits in the past 12             */
    /*  MEDIANHHINC                      N5          138750               Median household income                             */
    /*  AVGHHINC                         N5          203327               Mean household income                               */
    /*  AVGHHEARNINGS                    N5          210023               Mean household earnings                             */
    /*  AVGHHSOCSEC                      N5           16646               Mean household social security income               */
    /*  AVGHHRETINC                      N5           24868               Mean household retirement income                    */
    /*  AVGHHSUPPSECINC                  N5            7678               Mean household supplemental security inc            */
    /*  AVGHHPUBASSIST                   N5               .               Mean household cash public assistance in            */
    /*  FAMHHS                           N5             386               Family households                                   */
    /*  PCTFAMHHS                        N4    41.599975586               Family households                                   */
    /*  FAMHHINC0                        N5              20               Less than $10,000                                   */
    /*  PCTFAMHHINC0                     N4    5.1999969482               Less than $10,000                                   */
    /*  FAMHHINC10                       N5               0               $10,000 to $14,999                                  */
    /*  PCTFAMHHINC10                    N4               0               $10,000 to $14,999                                  */
    /*  FAMHHINC15                       N5               0               $15,000 to $24,999                                  */
    /*  PCTFAMHHINC15                    N4               0               $15,000 to $24,999                                  */
    /*  FAMHHINC25                       N5               0               $25,000 to $34,999                                  */
    /*  PCTFAMHHINC25                    N4               0               $25,000 to $34,999                                  */
    /*  FAMHHINC35                       N5               0               $35,000 to $49,999                                  */
    /*  PCTFAMHHINC35                    N4               0               $35,000 to $49,999                                  */
    /*  FAMHHINC50                       N5              32               $50,000 to $74,999                                  */
    /*  PCTFAMHHINC50                    N4    8.2999954224               $50,000 to $74,999                                  */
    /*  FAMHHINC75                       N5              81               $75,000 to $99,999                                  */
    /*  PCTFAMHHINC75                    N4              21               $75,000 to $99,999                                  */
    /*  FAMHHINC100                      N5              53               $100,000 to $149,999                                */
    /*  PCTFAMHHINC100                   N4    13.699996948               $100,000 to $149,999                                */
    /*  FAMHHINC150                      N5              55               $150,000 to $199,999                                */
    /*  PCTFAMHHINC150                   N4    14.199996948               $150,000 to $199,999                                */
    /*  FAMHHINC200                      N5             145               $200,000 or more                                    */
    /*  PCTFAMHHINC200                   N4    37.599975586               $200,000 or more                                    */
    /*  MEDIANFAMINC                     N5          150318               Median family income                                */
    /*  AVGFAMINC                        N5          229983               Mean family income                                  */
    /*  PCI                              N5           81904               Per-capita income                                   */
    /*  NONFAMHHS                        N5             543               Nonfamily households                                */
    /*  PCTNONFAMHHS                     N4    58.399993896               Nonfamily households                                */
    /*  MEDIANNONFAMINC                  N5          136250               Median nonfamily income                             */
    /*  AVGNONFAMINC                     N5          184379               Mean nonfamily income                               */
    /*  FULLTIMEWORKERS                  N5            1069               All full-time workers                               */
    /*  FULLTIMEWORKERSMALE              N5             622               All male full-time workers                          */
    /*  PCTFULLTIMEWORKERSMALE           N4    58.199981689               All male full-time workers                          */
    /*  FULLTIMEWORKERSFEMALE            N5             447               All female full-time workers                        */
    /*  PCTFULLTIMEWORKERSFEMALE         N4    41.799987793               All female full-time workers                        */
    /*  MEDIANEARNINGS                   N5           70278               Median earnings for workers                         */
    /*  MEDIANEARNINGSMALE               N5           79148               Median earnings for male full-time, year            */
    /*  MEDIANEARNINGSFEMALE             N5           96042               Median earnings for female full-time, ye            */
    /*  POVUNIVERSE                      N5            2509               Persons for whom poverty status is deter            */
    /*  POOR                             N5             150               Persons below poverty                               */
    /*  PCTPOOR                          N4               6               Persons below poverty                               */
    /*  POVRATIOUNDERHALF                N5              97               Poverty ratio under 0.5                             */
    /*  PCTPOVRATIOUNDERHALF             N4    3.8999996185               Poverty ratio under 0.5                             */
    /*  POVRATIOV5TOV99                  N5              53               Poverty ratio in 0.5 to 0.99                        */
    /*  PCTPOVRATIOV5TOV99               N4    2.0999984741               Poverty ratio in 0.5 to 0.99                        */
    /*  POVRATIO1TO2                     N5              39               Poverty ratio in 1 to 2                             */
    /*  PCTPOVRATIO1TO2                  N4    1.5999994278               Poverty ratio in 1 to 2                             */
    /*  POVRATIOOVER2                    N5            2320               Poverty ratio in 2 and over                         */
    /*  PCTPOVRATIOOVER2                 N4            92.5               Poverty ratio in 2 and over                         */
    /*  POVUNIVERSEUNDER18               N5             245               Persons under 18 for whom poverty status            */
    /*  POORUNDER18                      N5              26               Persons under 18 in poverty                         */
    /*  PCTPOORUNDER18                   N4    10.599998474               Persons under 18 in poverty                         */
    /*  POVUNIVERSE18_64                 N5            2015               Persons aged 18 to 64 for whom poverty s            */
    /*  POOR18TO64                       N5              93               Persons aged 18 to 64 in poverty                    */
    /*  PCTPOOR18TO64                    N4    4.5999984741               Persons aged 18 to 64 in poverty                    */
    /*  POVUNIVERSEOVER65                N5             249               Persons over 65 for whom poverty status             */
    /*  POOROVER65                       N5              31               Persons over 65 in poverty                          */
    /*  PCTPOOROVER65                    N4    12.399993896               Persons over 65 in poverty                          */
    /*  POVUNIVERSEFAMILYPOP             N5            1530               Persons in families for whom poverty sta            */
    /*  POVUNIVERSEUNRELATED             N5             979               Unrelated individuals for whom poverty s            */
    /*  POORINFAMILY                     N5              69               Persons in families in poverty                      */
    /*  PCTPOORINFAMILY                  N4             4.5               Persons in families in poverty                      */
    /*  POORFAMILIES                     N5              20               Family households in poverty                        */
    /*  PCTPOORFAMILIES                  N4    5.1999969482               Family households in poverty                        */
    /*  POORUNRELATED                    N5              81               Unrelated persons in poverty 15 years an            */
    /*  PCTPOORUNRELATED                 N4    8.2999954224               Unrelated persons in poverty 15 years an            */
    /*  OVER16                           N5            2268               Population 16 years and over                        */
    /*  LABORFORCE                       N5            1597               In labor force                                      */
    /*  PCTLABORFORCE                    N4    70.399963379               In labor force                                      */
    /*  CIVLABFORCE                      N5            1597               Civilian labor force                                */
    /*  PCTCIVLABFORCE                   N4    70.399963379               Civilian labor force                                */
    /*  EMPLOYEDCLF                      N5            1261               Employed civilians                                  */
    /*  PCTEMPLOYEDCLF                   N4              79               Employed civilians                                  */
    /*  UNEMPLOYEDCLF                    N5             336               Unemployed civilians                                */
    /*  PCTUNEMPLOYEDCLF                 N4              21               Unemployed civilians                                */
    /*  MILITARY                         N5               0               In military                                         */
    /*  PCTMILITARY                      N4               0               In military                                         */
    /*  NOTINLF                          N5             671               Not in labor force                                  */
    /*  PCTNOTINLF                       N4    29.599990845               Not in labor force                                  */
    /*  OVER16FEMALES                    N5            1184               Females 16 years and over                           */
    /*  PCTOVER16FEMALES                 N4    52.199981689               Females 16 years and over                           */
    /*  LABORFORCEFEMALES                N5             764               Females in labor force                              */
    /*  PCTLABORFORCEFEMALES             N4    33.699981689               Females in labor force                              */
    /*  CIVLABFORCEFEMALES               N5             764               Females in civilian labor force                     */
    /*  PCTCIVLABFORCEFEMALES            N4    33.699981689               Females in civilian labor force                     */
    /*  EMPLOYEDFEMALES                  N5             547               Employed females                                    */
    /*  PCTEMPLOYEDFEMALES               N4    71.599975586               Employed females                                    */
    /*  OWNKIDSUNDER6                    N5             164               (Own) children under 6                              */
    /*  OWNKIDSU6ALLPRNTSWK              N5             105               All parents working                                 */
    /*  PCTOWNKIDSU6ALLPRNTSWK           N4              64               All parents working                                 */
    /*  OWNKIDSOVER6                     N5              81               (Own) children aged 6 to 17                         */
    /*  OWNKIDSO6ALLPRNTSWK              N5               0               All parents working                                 */
    /*  PCTOWNKIDSO6ALLPRNTSWK           N4               0               All parents working                                 */
    /*  WORKER16                         N5            1251               Workers 16 years and over                           */
    /*  COMMUTERS                        N5            1189               Workers 16+ who commute to work                     */
    /*  PCTCOMMUTERS                     N4              95               Workers 16+ who commute to work                     */
    /*  DRIVEALONE                       N5             356               Car, truck, or van; drove alone                     */
    /*  PCTDRIVEALONE                    N4            28.5               Car, truck, or van; drove alone                     */
    /*  CARPOOL                          N5              11               Car, truck, or van; carpooled                       */
    /*  PCTCARPOOL                       N4    0.8999996185               Car, truck, or van; carpooled                       */
    /*  PUBLICTRANS                      N5             353               Public transportation (excluding taxicab            */
    /*  PCTPUBLICTRANS                   N4    28.199996948               Public transportation (excluding taxicab            */
    /*  WALKTOWORK                       N5             372               Walked to work                                      */
    /*  PCTWALKTOWORK                    N4    29.699996948               Walked to work                                      */
    /*  OTHERCOMMUTE                     N5              97               Other means of commuting                            */
    /*  PCTOTHERCOMMUTE                  N4    7.7999992371               Other means of commuting                            */
    /*  WORKATHOME                       N5              62               Worked at home                                      */
    /*  PCTWORKATHOME                    N4               5               Worked at home                                      */
    /*  AVGCOMMUTE                       N6            25.9               Mean travel time to work in minutes                 */
    /*  MANPROFOCCS                      N5             935               Management, business, science, and arts             */
    /*  PCTMANPROFOCCS                   N4    74.099975586               Management, business, science, and arts             */
    /*  SERVICEOCCS                      N5              57               Service occupations                                 */
    /*  PCTSERVICEOCCS                   N4             4.5               Service occupations                                 */
    /*  SALESOFFOCCS                     N5             174               Sales and office occupations                        */
    /*  PCTSALESOFFOCCS                  N4    13.799995422               Sales and office occupations                        */
    /*  FARMFISHOCCS                     N5               0               Farming, fishing, and forestry occupatio            */
    /*  PCTFARMFISHOCCS                  N4               0               Farming, fishing, and forestry occupatio            */
    /*  CONSOCCS                         N5              32               Construction, extraction, installation,             */
    /*  PCTCONSOCCS                      N4             2.5               Construction, extraction, installation,             */
    /*  TRANSOCCS                        N5              63               Production, transportation, and material            */
    /*  PCTTRANSOCCS                     N4               5               Production, transportation, and material            */
    /*  AGRICULTURE                      N5               0               Agriculture, forestry, fishing and hunti            */
    /*  PCTAGRICULTURE                   N4               0               Agriculture, forestry, fishing and hunti            */
    /*  CONSTRUCTION                     N5               0               Construction                                        */
    /*  PCTCONSTRUCTION                  N4               0               Construction                                        */
    /*  MANUFACTURING                    N5              28               Manufacturing                                       */
    /*  PCTMANUFACTURING                 N4    2.1999988556               Manufacturing                                       */
    /*  WHOLESALETRADE                   N5               5               Wholesale trade                                     */
    /*  PCTWHOLESALETRADE                N4    0.3999998569               Wholesale trade                                     */
    /*  RETAILTRADE                      N5               0               Retail trade                                        */
    /*  PCTRETAILTRADE                   N4               0               Retail trade                                        */
    /*  TRANSPORTATION                   N5              14               Transportation and warehousing, and util            */
    /*  PCTTRANSPORTATION                N4    1.0999994278               Transportation and warehousing, and util            */
    /*  INFORMATION                      N5             183               Information                                         */
    /*  PCTINFORMATION                   N4            14.5               Information                                         */
    /*  FINANCE_INS                      N5             148               Finance and insurance, and real estate a            */
    /*  PCTFINANCE_INS                   N4    11.699996948               Finance and insurance, and real estate a            */
    /*  PROFESSIONAL                     N5             361               Professional, scientific, management, an            */
    /*  PCTPROFESSIONAL                  N4    28.599990845               Professional, scientific, management, an            */
    /*  EDUC_HEALTH_SOCSVCS              N5             164               Educational services, and health care an            */
    /*  PCTEDUC_HEALTH_SOCSVCS           N4              13               Educational services, and health care an            */
    /*  RECREATIONETC                    N5              30               Arts, entertainment, and recreation, and            */
    /*  PCTRECREATIONETC                 N4    2.3999996185               Arts, entertainment, and recreation, and            */
    /*  OTHERINDUSTRIES                  N5             153               Other services, except public administra            */
    /*  PCTOTHERINDUSTRIES               N4    12.099998474               Other services, except public administra            */
    /*  PUBLICADMIN                      N5             175               Public administration                               */
    /*  PCTPUBLICADMIN                   N4    13.899993896               Public administration                               */
    /*  PRIVWAGEWORKERS                  N5             880               Private wage and salary workers                     */
    /*  PCTPRIVWAGEWORKERS               N4    69.799987793               Private wage and salary workers                     */
    /*  GOVWORKERS                       N5             276               Government workers                                  */
    /*  PCTGOVWORKERS                    N4    21.899993896               Government workers                                  */
    /*  SELFEMPWORKERS                   N5             105               Self-employed workers in own not incorpo            */
    /*  PCTSELFEMPWORKERS                N4    8.2999954224               Self-employed workers in own not incorpo            */
    /*  UNPAIDFAMWORKERS                 N5               0               Unpaid family workers                               */
    /*  PCTUNPAIDFAMWORKERS              N4               0               Unpaid family workers                               */
    /*  TOTPOPNONINST                    N5            2509               Civilian noninstitutionalized persons               */
    /*  NONINSTUNDER65                   N5            2260               Under 65 years of age                               */
    /*  PCTNONINSTUNDER65                N4    90.099975586               Under 65 years of age                               */
    /*  NOTINSUREDUNDER65                N5              31               Without insurance coverage                          */
    /*  PCTNOTINSUREDUNDER65             N4    1.3999996185               Without insurance coverage                          */
    /*  PUBLICINSURANCEUNDER65           N5             513               With public insurance                               */
    /*  PCTPUBLICINSURANCEUNDER65        N4    22.699996948               With public insurance                               */
    /*  PRIVATEINSURANCEONLYUNDER65      N5            1730               With private insurance                              */
    /*  PCTPRIVATEINSURANCEONLYUNDER65   N4            76.5               With private insurance                              */
    /*  NONINSTUNDER18                   N5             245               Under 19 years of age                               */
    /*  PCTNONINSTUNDER18                N4    9.7999954224               Under 19 years of age                               */
    /*  NOTINSUREDUNDER18                N5               0               Without insurance coverage                          */
    /*  PCTNOTINSUREDUNDER18             N4               0               Without insurance coverage                          */
    /*  FAMILIES                         N5             386               Family households                                   */
    /*  PCTFAMILIES                      N4    41.599975586               Family households                                   */
    /*  FAMSWITHKIDS                     N5             127               With own children under 18 years                    */
    /*  PCTFAMSWITHKIDS                  N4    13.699996948               With own children under 18 years                    */
    /*  MARRIEDCOUPLES                   N5             283               Married-couple families                             */
    /*  PCTMARRIEDCOUPLES                N4            30.5               Married-couple families                             */
    /*  COUPLESWITHKIDS                  N5             127               With own children under 18 years                    */
    /*  PCTCOUPLESWITHKIDS               N4    13.699996948               With own children under 18 years                    */
    /*  SINGLEMALEFAMILIES               N5             103               Male householder, no spouse present                 */
    /*  PCTSINGLEMALEFAMILIES            N4    11.099998474               Male householder, no spouse present                 */
    /*  SINGLEFATHERS                    N5               0               With own children under 18 years                    */
    /*  PCTSINGLEFATHERS                 N4               0               With own children under 18 years                    */
    /*  SINGLEFEMALEFAMILIES             N5               0               Female householder, no spouse present               */
    /*  PCTSINGLEFEMALEFAMILIES          N4               0               Female householder, no spouse present               */
    /*  SINGLEMOTHERS                    N5               0               With own children under 18 years                    */
    /*  PCTSINGLEMOTHERS                 N4               0               With own children under 18 years                    */
    /*  LIVINGALONE                      N5             309               Living alone                                        */
    /*  PCTLIVINGALONE                   N4    56.899993896               Living alone                                        */
    /*  OVER65ALONE                      N5              92               65 years and over living alone                      */
    /*  PCTOVER65ALONE                   N4    16.899993896               65 years and over living alone                      */
    /*  HHSWITHKIDS                      N5             127               Households with one or more people under            */
    /*  PCTHHSWITHKIDS                   N4    13.699996948               Households with one or more people under            */
    /*  HHSWITHELDERS                    N5             152               Households with one or more people 65 ye            */
    /*  PCTHHSWITHELDERS                 N4    16.399993896               Households with one or more people 65 ye            */
    /*  AVGHHSIZE                        N6            2.69               Average household size                              */
    /*  AVGFAMSIZE                       N6            3.96               Average family size                                 */
    /*  HHPOP                            N5            2503               Household population                                */
    /*  PCTHHPOP                         N4    99.399963379               Household population                                */
    /*  FAMHHPOP                         N5            1530               Living in family households                         */
    /*  PCTFAMHHPOP                      N4    61.099975586               Living in family households                         */
    /*  NONFAMHHPOP                      N5             973               Living in nonfamily households                      */
    /*  PCTNONFAMHHPOP                   N4    38.899993896               Living in nonfamily households                      */
    /*  GRPQUARTERS                      N5              14               Living in group quarters                            */
    /*  PCTGRPQUARTERS                   N4    0.5999999046               Living in group quarters                            */
    /*  HOUSEHOLDER                      N5             929               Householder                                         */
    /*  PCTHOUSEHOLDER                   N4    37.099975586               Householder                                         */
    /*  SPOUSE                           N5             293               Spouse                                              */
    /*  PCTSPOUSE                        N4    11.699996948               Spouse                                              */
    /*  CHILD                            N5             381               Child                                               */
    /*  PCTCHILD                         N4    15.199996948               Child                                               */
    /*  OTHERRELATIVE                    N5             470               Other relatives                                     */
    /*  PCTOTHERRELATIVE                 N4    18.799987793               Other relatives                                     */
    /*  NONRELATIVE                      N5             296               Nonrelatives                                        */
    /*  PCTNONRELATIVE                   N4    11.799995422               Nonrelatives                                        */
    /*  UNMARRIEDPARTNER                 N5             134               Unmarried partner                                   */
    /*  PCTUNMARRIEDPARTNER              N4    5.3999977112               Unmarried partner                                   */
    /*  UMPARTNERHHSPERK                 N5             144               Unmarried-partner HHs per 1000                      */
    /*  NEVERMARRIED                     N5            1593               Never married                                       */
    /*  PCTNEVERMARRIED                  N4    69.399963379               Never married                                       */
    /*  MARRIED                          N5             603               Now married, except separated                       */
    /*  PCTMARRIED                       N4    26.299987793               Now married, except separated                       */
    /*  SEPARATED                        N5               0               Separated                                           */
    /*  PCTSEPARATED                     N4               0               Separated                                           */
    /*  WIDOWED                          N5               0               Widowed                                             */
    /*  PCTWIDOWED                       N4               0               Widowed                                             */
    /*  DIVORCED                         N5             100               Divorced, and not currently married                 */
    /*  PCTDIVORCED                      N4    4.3999977112               Divorced, and not currently married                 */
    /*  WOMEN15TO50                      N5             790               Women 15 to 50 years old                            */
    /*  UNMARRIEDWOMEN15TO50             N5             615               Unmarried women 15 to 50 years old                  */
    /*  PCTUNMARRIEDWOMEN15TO50          N4    77.799987793               Unmarried women 15 to 50 years old                  */
    /*  WOMENGIVINGBIRTH                 N5              16               Women 15 to 50 years old who had a birth            */
    /*  PCTWOMENGIVINGBIRTH              N4               2               Women 15 to 50 years old who had a birth            */
    /*  UNMARRIEDGIVINGBIRTH             N5               0               Unmarried women who gave birth                      */
    /*  PCTUNMARRIEDGIVINGBIRTH          N4               0               Unmarried women who gave birth                      */
    /*  WOMEN15TO19                      N5               0               Women 15 to 19 years of age                         */
    /*  PCTWOMEN15TO19                   N4               0               Women 15 to 19 years of age                         */
    /*  WOMEN20TO34                      N5              16               Women 20 to 34 years of age                         */
    /*  PCTWOMEN20TO34                   N4             100               Women 20 to 34 years of age                         */
    /*  WOMEN35TO50                      N5               0               Women 35 to 50 years of age                         */
    /*  PCTWOMEN35TO50                   N4               0               Women 35 to 50 years of age                         */
    /*  UNMARRIEDGIVINGBIRTHPERK         N5               0               Per 1,000 unmarried women                           */
    /*  GIVINGBIRTHPERK                  N5              20               Per 1,000 women 15 to 50 years old                  */
    /*  BIRTHRATE15_19                   N5               0               Per 1,000 women 15 to 19 years old                  */
    /*  BIRTHRATE20_34                   N5              24               Per 1,000 women 20 to 34 years old                  */
    /*  BIRTHRATE35_50                   N5               0               Per 1,000 women 35 to 50 years old                  */
    /*  GRANDPRNTSLVNGWITHGRNDKID        N5               0               Grandparents living with own grandchildr            */
    /*  GRANDPRNTSCARING                 N5               0               Grandparents responsible for grandchildr            */
    /*  PCTGRANDPRNTSCARING              N4               .               Grandparents responsible for grandchildr            */
    /*  GRANDPRNTSCARINGLT1              N5               0               Less than 1 year                                    */
    /*  PCTGRANDPRNTSCARINGLT1           N4               .               Less than 1 year                                    */
    /*  GRANDPRNTSCARING1OR2             N5               0               1 or 2 years                                        */
    /*  PCTGRANDPRNTSCARING1OR2          N4               .               1 or 2 years                                        */
    /*  GRANDPRNTSCARING3OR4             N5               0               3 or 4 years                                        */
    /*  PCTGRANDPRNTSCARING3OR4          N4               .               3 or 4 years                                        */
    /*  GRANDPRNTSCARING5ORMORE          N5               0               5 or more years                                     */
    /*  PCTGRANDPRNTSCARING5ORMORE       N4               .               5 or more years                                     */
    /*  OVER3                            N5            2359               Population 3 years and over                         */
    /*  ENROLLEDOVER3                    N5             179               Population 3 years and over enrolled in             */
    /*  PCTENROLLEDOVER3                 N4    7.5999984741               Population 3 years and over enrolled in             */
    /*  INNURSERY                        N5               3               In nursery school, preschool                        */
    /*  PCTINNURSERY                     N4    1.6999998093               In nursery school, preschool                        */
    /*  INKINDERGARTEN                   N5               3               In kindergarten                                     */
    /*  PCTINKINDERGARTEN                N4    1.6999998093               In kindergarten                                     */
    /*  INELEMENTARY                     N5              57               In elementary school, grades 1-8                    */
    /*  PCTINELEMENTARY                  N4    31.799987793               In elementary school, grades 1-8                    */
    /*  INHIGHSCHOOL                     N5              32               In high school, grades 9-12                         */
    /*  PCTINHIGHSCHOOL                  N4    17.899993896               In high school, grades 9-12                         */
    /*  INCOLLEGE                        N5              84               In college or graduate school                       */
    /*  PCTINCOLLEGE                     N4    46.899993896               In college or graduate school                       */
    /*  LESSTHAN9TH                      N5               0               Less than 9th grade                                 */
    /*  PCTLESSTHAN9TH                   N4               0               Less than 9th grade                                 */
    /*  SOMEHIGHSCHOOL                   N5              78               9th to 12th grade, no diploma                       */
    /*  PCTSOMEHIGHSCHOOL                N4               4               9th to 12th grade, no diploma                       */
    /*  HIGHSCHOOL                       N5             438               High school graduate (includes equivalen            */
    /*  PCTHIGHSCHOOL                    N4    22.399993896               High school graduate (includes equivalen            */
    /*  SOMECOLLEGE                      N5             108               Some college, no degree                             */
    /*  PCTSOMECOLLEGE                   N4             5.5               Some college, no degree                             */
    /*  ASSOCIATES                       N5              78               Associates degree                                   */
    /*  PCTASSOCIATES                    N4               4               Associates degree                                   */
    /*  BACHELORS                        N5             461               Bachelors degree                                    */
    /*  PCTBACHELORS                     N4    23.599990845               Bachelors degree                                    */
    /*  GRADPROF                         N5             793               Graduate or professional degree                     */
    /*  PCTGRADPROF                      N4            40.5               Graduate or professional degree                     */
    /*  HIGHSCHOOLORMORE                 N5            1878               High school graduate or higher                      */
    /*  PCTHIGHSCHOOLORMORE              N4              96               High school graduate or higher                      */
    /*  BACHELORSORMORE                  N5            1254               Bachelor degree or higher                           */
    /*  PCTBACHELORSORMORE               N4    64.099975586               Bachelor degree or higher                           */
    /*  CIVILIAN                         N5            2266               Civilian population 18 years and over               */
    /*  PCTCIVILIAN                      N4             100               Civilian population 18 years and over               */
    /*  VETERAN                          N5              10               Civilian veterans                                   */
    /*  PCTVETERAN                       N4    0.3999998569               Civilian veterans                                   */
    /*  DISABLED                         N5             370               With a disability                                   */
    /*  PCTDISABLED                      N4    14.699996948               With a disability                                   */
    /*  DISABLEDUNDER18                  N5              26               With a disability                                   */
    /*  PCTDISABLEDUNDER18               N4    10.599998474               With a disability                                   */
    /*  NONINST18_64                     N5            2015               Persons 19 to 64 years                              */
    /*  PCTNONINST18_64                  N4    80.299987793               Persons 19 to 64 years                              */
    /*  DISABLED18_64                    N5             224               With a disability                                   */
    /*  PCTDISABLED18_64                 N4    11.099998474               With a disability                                   */
    /*  NONINSTOVER65                    N5             249               Persons 65 years and over                           */
    /*  PCTNONINSTOVER65                 N4    9.8999938965               Persons 65 years and over                           */
    /*  DISABLEDELDER                    N5             120               With a disability                                   */
    /*  PCTDISABLEDELDER                 N4    48.199981689               With a disability                                   */
    /*  OVER1                            N5            2496               Population 1 year and over                          */
    /*  SAMEHOUSE                        N5            1986               Same house                                          */
    /*  PCTSAMEHOUSE                     N4    79.599975586               Same house                                          */
    /*  DIFFHOUSE                        N5             510               Different house in the U.S.                         */
    /*  PCTDIFFHOUSE                     N4    20.399993896               Different house in the U.S.                         */
    /*  DIFFHOUSESAMECOUNTY              N5             330               Same county                                         */
    /*  PCTDIFFHOUSESAMECOUNTY           N4    64.699951172               Same county                                         */
    /*  DIFFCOUNTY                       N5             180               Different county (any)                              */
    /*  PCTDIFFCOUNTY                    N4    35.299987793               Different county (any)                              */
    /*  DIFFCNTYSAMESTATE                N5               0               Different county (same state)                       */
    /*  PCTDIFFCNTYSAMESTATE             N4               0               Different county (same state)                       */
    /*  DIFFSTATE                        N5             180               Different state                                     */
    /*  PCTDIFFSTATE                     N4    35.299987793               Different state                                     */
    /*  LIVEDABROAD                      N5               0               Lived abroad 1 year ago                             */
    /*  PCTLIVEDABROAD                   N4               0               Lived abroad 1 year ago                             */
    /*  USNATIVE                         N5            2236               U.S. native                                         */
    /*  PCTUSNATIVE                      N4    88.799987793               U.S. native                                         */
    /*  BORNINUS                         N5            2053               Born in United States                               */
    /*  PCTBORNINUS                      N4    91.799987793               Born in United States                               */
    /*  BORNINCURRSTATE                  N5            1018               Born in state of current residence                  */
    /*  PCTBORNINCURRSTATE               N4    49.599975586               Born in state of current residence                  */
    /*  BORNINDIFFSTATE                  N5            1035               Born in different state than current res            */
    /*  PCTBORNINDIFFSTATE               N4    50.399993896               Born in different state than current res            */
    /*  BORNABROAD                       N5             183               Born in Puerto Rico, U.S. Island areas,             */
    /*  PCTBORNABROAD                    N4    8.1999969482               Born in Puerto Rico, U.S. Island areas,             */
    /*  FOREIGNBORN                      N5             281               Foreign born                                        */
    /*  PCTFOREIGNBORN                   N4    11.199996948               Foreign born                                        */
    /*  NATURALIZED                      N5             239               Naturalized U.S. citizen                            */
    /*  PCTNATURALIZED                   N4    85.099975586               Naturalized U.S. citizen                            */
    /*  NONCITIZEN                       N5              42               Not a U.S. citizen                                  */
    /*  PCTNONCITIZEN                    N4    14.899993896               Not a U.S. citizen                                  */
    /*  BORNOUTSIDEUS                    N5             464               Population born outside the United State            */
    /*  PCTBORNOUTSIDEUS                 N4    18.399993896               Population born outside the United State            */
    /*  BORNOUTSIDEUSNATIVE              N5             183               Native, born outside U.S.                           */
    /*  PCTBORNOUTSIDEUSNATIVE           N4    39.399993896               Native, born outside U.S.                           */
    /*  NATIVEENTEREDGE2000              N5             124               Entered U.S. 2000 or later                          */
    /*  PCTNATIVEENTEREDGE2000           N4    67.799987793               Entered U.S. 2000 or later                          */
    /*  NATIVEENTEREDLT2000              N5              24               Entered U.S. before 2000                            */
    /*  PCTNATIVEENTEREDLT2000           N4    13.099998474               Entered U.S. before 2000                            */
    /*  FBENTEREDGE2000                  N5             133               Entered U.S. 2000 or later                          */
    /*  PCTFBENTEREDGE2000               N4    47.299987793               Entered U.S. 2000 or later                          */
    /*  FBENTEREDLT2000                  N5             148               Entered U.S. before 2000                            */
    /*  PCTFBENTEREDLT2000               N4    52.699981689               Entered U.S. before 2000                            */
    /*  FBMINUSSEA                       N5             281               Foreign-born population, excluding popul            */
    /*  PCTFBMINUSSEA                    N4    11.199996948               Foreign-born population, excluding popul            */
    /*  FBEUROPE                         N5              16               Europe                                              */
    /*  PCTFBEUROPE                      N4    5.6999969482               Europe                                              */
    /*  FBASIA                           N5             117               Asia                                                */
    /*  PCTFBASIA                        N4    41.599975586               Asia                                                */
    /*  FBAFRICA                         N5             114               Africa                                              */
    /*  PCTFBAFRICA                      N4    40.599975586               Africa                                              */
    /*  FBOCEANIA                        N5               0               Oceania                                             */
    /*  PCTFBOCEANIA                     N4               0               Oceania                                             */
    /*  FBLATINAMERICA                   N5              28               South and Central America (includes Mexi            */
    /*  PCTFBLATINAMERICA                N4              10               South and Central America (includes Mexi            */
    /*  FBNORTHAMERICA                   N5               6               Northern America                                    */
    /*  PCTFBNORTHAMERICA                N4    2.0999984741               Northern America                                    */
    /*  ENGLISHONLY                      N5            1982               English only                                        */
    /*  PCTENGLISHONLY                   N4               .               English only                                        */
    /*  OTHLANG                          N5             374               Language other than English                         */
    /*  PCTOTHLANG                       N4               .               Language other than English                         */
    /*  OTHLANGENGLISHLTD                N5             132               Speaks English less than very well                  */
    /*  PCTOTHLANGENGLISHLTD             N4    35.299987793               Speaks English less than very well                  */
    /*  SPANISH                          N5              68               Speak Spanish                                       */
    /*  PCTSPANISH                       N4               .               Speak Spanish                                       */
    /*  SPANISHENGLISHLTD                N5               0               Speaks English less than very well                  */
    /*  PCTSPANISHENGLISHLTD             N4               0               Speaks English less than very well                  */
    /*  NOCOMPUTER                       N5              81               Households with no computer                         */
    /*  PCTNOCOMPUTER                    N4    8.6999969482               Households with no computer                         */
    /*  COMPUTER                         N5             848               Households with a computer                          */
    /*  PCTCOMPUTER                      N4    91.299987793               Households with a computer                          */
    /*  DIALUPINTERNET                   N5               0               With a dial-up internet subscription alo            */
    /*  PCTDIALUPINTERNET                N4               0               With a dial-up internet subscription alo            */
    /*  BROADBANDINTERNET                N5             837               With a broadband internet subscription              */
    /*  PCTBROADBANDINTERNET             N4    98.699951172               With a broadband internet subscription              */
    /*  NOINTERNET                       N5              11               No internet subscription                            */
    /*  PCTNOINTERNET                    N4    1.2999992371               No internet subscription                            */
    /*  TOTHUS                           N5            1091               Total housing units                                 */
    /*  OCCHUS                           N5             929               Occupied housing units                              */
    /*  PCTOCCHUS                        N4    85.199951172               Occupied housing units                              */
    /*  OWNEROCC                         N5             505               Owner-occupied                                      */
    /*  PCTOWNEROCC                      N4    54.399993896               Owner-occupied                                      */
    /*  RENTEROCC                        N5             424               Renter-occupied                                     */
    /*  PCTRENTEROCC                     N4    45.599975586               Renter-occupied                                     */
    /*  AVGOWNERHHSIZE                   N6            2.74               Average household size of owner-occupied            */
    /*  AVGRENTERHHSIZE                  N6            2.64               Average household size of renter-occupie            */
    /*  VACHUS                           N5             162               Vacant housing units                                */
    /*  PCTVACHUS                        N4    14.799995422               Vacant housing units                                */
    /*  VACANTFORSALE                    N5              17               For sale                                            */
    /*  PCTVACANTFORSALE                 N4            10.5               For sale                                            */
    /*  VACANTFORRENT                    N5              78               For rent                                            */
    /*  PCTVACANTFORRENT                 N4    48.099975586               For rent                                            */
    /*  VACANTSEASONAL                   N5               0               For seasonal, recreational, or occasiona            */
    /*  PCTVACANTSEASONAL                N4               0               For seasonal, recreational, or occasiona            */
    /*  TOTALOWNERUNITS                  N5             522               Total owner units                                   */
    /*  OWNERVACRATE                     N6             3.3               Homeowner vacancy rate                              */
    /*  TOTALRENTALUNITS                 N5             502               Total rental units                                  */
    /*  RENTERVACRATE                    N6            15.5               Rental vacancy rate                                 */
    /*  PERSONSINOWNERUNITS              N5            1382               People living in owned homes                        */
    /*  PCTPERSONSINOWNERUNITS           N4    54.899993896               People living in owned homes                        */
    /*  PERSONSINRENTERUNITS             N5            1121               People living in rental homes                       */
    /*  PCTPERSONSINRENTERUNITS          N4            44.5               People living in rental homes                       */
    /*  UNITS1                           N5             366               Single-family units                                 */
    /*  PCTUNITS1                        N4            33.5               Single-family units                                 */
    /*  UNITS1DETACHED                   N5               9               Single unit, detached                               */
    /*  PCTUNITS1DETACHED                N4             2.5               Single unit, detached                               */
    /*  UNITS1ATTACHED                   N5             357               Single unit, attached                               */
    /*  PCTUNITS1ATTACHED                N4            97.5               Single unit, attached                               */
    /*  UNITS2                           N5             314               Duplexes                                            */
    /*  PCTUNITS2                        N4    28.799987793               Duplexes                                            */
    /*  UNITS3_4                         N5              63               3 or 4 units                                        */
    /*  PCTUNITS3_4                      N4    5.7999992371               3 or 4 units                                        */
    /*  UNITS5_9                         N5              32               5 to 9 units                                        */
    /*  PCTUNITS5_9                      N4    2.8999996185               5 to 9 units                                        */
    /*  UNITS10_19                       N5              20               10 to 19 units                                      */
    /*  PCTUNITS10_19                    N4    1.7999992371               10 to 19 units                                      */
    /*  UNITS20UP                        N5             296               20 or more units                                    */
    /*  PCTUNITS20UP                     N4    27.099990845               20 or more units                                    */
    /*  MOBILEHOMES                      N5               0               Mobile home                                         */
    /*  PCTMOBILEHOMES                   N4               0               Mobile home                                         */
    /*  BOATRV                           N5               0               Boat, RV, van, etc.                                 */
    /*  PCTBOATRV                        N4               0               Boat, RV, van, etc.                                 */
    /*  MOBILEHOMESPERK                  N5               0               Mobile homes per 1000 HUs                           */
    /*  BUILT2010ORLATER                 N5             229               Built 2010 or later                                 */
    /*  PCTBUILT2010ORLATER              N4              21               Built 2010 or later                                 */
    /*  BUILT2000_2009                   N5              86               Built 2000 to 2009                                  */
    /*  PCTBUILT2000_2009                N4    7.8999977112               Built 2000 to 2009                                  */
    /*  BUILT1990_1999                   N5               0               Built 1990 to 1999                                  */
    /*  PCTBUILT1990_1999                N4               0               Built 1990 to 1999                                  */
    /*  BUILT1980_1989                   N5              38               Built 1980 to 1989                                  */
    /*  PCTBUILT1980_1989                N4             3.5               Built 1980 to 1989                                  */
    /*  BUILT1970_1979                   N5              12               Built 1970 to 1979                                  */
    /*  PCTBUILT1970_1979                N4    1.0999994278               Built 1970 to 1979                                  */
    /*  BUILT1960_1969                   N5              20               Built 1960 to 1969                                  */
    /*  PCTBUILT1960_1969                N4    1.7999992371               Built 1960 to 1969                                  */
    /*  BUILT1950_1959                   N5              10               Built 1950 to 1959                                  */
    /*  PCTBUILT1950_1959                N4    0.8999996185               Built 1950 to 1959                                  */
    /*  BUILT1940_1949                   N5               8               Built 1940 to 1949                                  */
    /*  PCTBUILT1940_1949                N4    0.6999998093               Built 1940 to 1949                                  */
    /*  BUILTBEFORE1940                  N5             688               Built 1939 or earlier                               */
    /*  PCTBUILTBEFORE1940               N4    63.099975586               Built 1939 or earlier                               */
    /*  MOVEDIN2010ORLATER               N5             674               Moved in 2010 or later                              */
    /*  PCTMOVEDIN2010ORLATER            N4    72.599975586               Moved in 2010 or later                              */
    /*  MOVEDIN2000_2009                 N5              52               Moved in 2000 to 2009                               */
    /*  PCTMOVEDIN2000_2009              N4    5.5999984741               Moved in 2000 to 2009                               */
    /*  MOVEDIN1990_1999                 N5              92               Moved in 1990 to 1999                               */
    /*  PCTMOVEDIN1990_1999              N4    9.8999938965               Moved in 1990 to 1999                               */
    /*  MOVEDINBEFORE1990                N5             111               Moved in 1989 or earlier                            */
    /*  PCTMOVEDINBEFORE1990             N4    11.899993896               Moved in 1989 or earlier                            */
    /*  NOVEHICLES                       N5             268               No vehicles available                               */
    /*  PCTNOVEHICLES                    N4    28.799987793               No vehicles available                               */
    /*  VEHICLES1                        N5             426               1 vehicle available                                 */
    /*  PCTVEHICLES1                     N4    45.899993896               1 vehicle available                                 */
    /*  VEHICLES2                        N5             207               2 vehicles available                                */
    /*  PCTVEHICLES2                     N4    22.299987793               2 vehicles available                                */
    /*  VEHICLESGE3                      N5              28               3 or more vehicles available                        */
    /*  PCTVEHICLESGE3                   N4               3               3 or more vehicles available                        */
    /*  HHFUTILGAS                       N5             526               Utility gas                                         */
    /*  PCTHHFUTILGAS                    N4    56.599975586               Utility gas                                         */
    /*  HHFLPGAS                         N5               0               Bottled, tank, or LP gas                            */
    /*  PCTHHFLPGAS                      N4               0               Bottled, tank, or LP gas                            */
    /*  HHFELECTRIC                      N5             403               Electricity                                         */
    /*  PCTHHFELECTRIC                   N4    43.399993896               Electricity                                         */
    /*  HHFKEROSENE                      N5               0               Fuel oil, kerosene, etc.                            */
    /*  PCTHHFKEROSENE                   N4               0               Fuel oil, kerosene, etc.                            */
    /*  HHFCOAL                          N5               0               Coal or coke                                        */
    /*  PCTHHFCOAL                       N4               0               Coal or coke                                        */
    /*  HHFWOOD                          N5               0               Wood                                                */
    /*  PCTHHFWOOD                       N4               0               Wood                                                */
    /*  HHFSOLAR                         N5               0               Solar energy                                        */
    /*  PCTHHFSOLAR                      N4               0               Solar energy                                        */
    /*  HHFOTHER                         N5               0               Other fuel                                          */
    /*  PCTHHFOTHER                      N4               0               Other fuel                                          */
    /*  HHFNOFUEL                        N5               0               No fuel used                                        */
    /*  PCTHHFNOFUEL                     N4               0               No fuel used                                        */
    /*  NOPLUMBING                       N5              30               Lacking complete plumbing facilities                */
    /*  PCTNOPLUMBING                    N4    3.1999988556               Lacking complete plumbing facilities                */
    /*  NOKITCHEN                        N5              30               Lacking complete kitchen facilities                 */
    /*  PCTNOKITCHEN                     N4    3.1999988556               Lacking complete kitchen facilities                 */
    /*  NOPHONE                          N5              30               No telephone service available                      */
    /*  PCTNOPHONE                       N4    3.1999988556               No telephone service available                      */
    /*  PERSONSPERROOMLOW                N5             901               1.00 or less                                        */
    /*  PCTPERSONSPERROOMLOW             N4              97               1.00 or less                                        */
    /*  PERSONSPERROOMMEDIUM             N5               0               1.01 to 1.50                                        */
    /*  PCTPERSONSPERROOMMEDIUM          N4               0               1.01 to 1.50                                        */
    /*  PERSONSPERROOMHIGH               N5              28               1.51 or more                                        */
    /*  PCTPERSONSPERROOMHIGH            N4               3               1.51 or more                                        */
    /*  HVALUNDER50                      N5              60               Less than $50,000                                   */
    /*  PCTHVALUNDER50                   N4    11.899993896               Less than $50,000                                   */
    /*  HVAL50                           N5               0               $50,000 to $99,999                                  */
    /*  PCTHVAL50                        N4               0               $50,000 to $99,999                                  */
    /*  HVAL100                          N5               0               $100,000 to $149,999                                */
    /*  PCTHVAL100                       N4               0               $100,000 to $149,999                                */
    /*  HVAL150                          N5               0               $150,000 to $199,999                                */
    /*  PCTHVAL150                       N4               0               $150,000 to $199,999                                */
    /*  HVAL200                          N5               0               $200,000 to $299,999                                */
    /*  PCTHVAL200                       N4               0               $200,000 to $299,999                                */
    /*  HVAL300                          N5               8               $300,000 to $499,999                                */
    /*  PCTHVAL300                       N4    1.5999994278               $300,000 to $499,999                                */
    /*  HVAL500                          N5             224               $500,000 to $999,999                                */
    /*  PCTHVAL500                       N4    44.399993896               $500,000 to $999,999                                */
    /*  HVALOVERMILLION                  N5             208               $1,000,000 or more                                  */
    /*  PCTHVALOVERMILLION               N4    41.199981689               $1,000,000 or more                                  */
    /*  HVALOVER2MILLION                 N5               5               $2,000,000 or more                                  */
    /*  PCTHVALOVER2MILLION              N4               1               $2,000,000 or more                                  */
    /*  MEDIANHVALUE                     N5          934200               Median home value                                   */
    /*  AVGHVALUE                        N5          965287               Average home value                                  */
    /*  HUSMORT                          N5             438               Housing units with a mortgage                       */
    /*  PCTHUSMORT                       N4    86.699951172               Housing units with a mortgage                       */
    /*  HUSMORTOVER30PCT                 N5              70               Owner costs 30% or more of HH income                */
    /*  PCTHUSMORTOVER30PCT              N4              16               Owner costs 30% or more of HH income                */
    /*  MEDIANOWNERCOSTSMORT             N5            1982               Median owner costs                                  */
    /*  HUSNOMORT                        N5              67               Housing units without a mortgage                    */
    /*  PCTHUSNOMORT                     N4    13.299995422               Housing units without a mortgage                    */
    /*  HUSNOMORTOVER30PCT               N5               0               Nonmortgage owner costs 30% or more of H            */
    /*  PCTHUSNOMORTOVER30PCT            N4               0               Nonmortgage owner costs 30% or more of H            */
    /*  MEDIANOWNERCOSTSNOMORT           N5               .               Median owner costs                                  */
    /*  CASHRENTER                       N5             424               Paying cash rent                                    */
    /*  PCTCASHRENTER                    N4             100               Paying cash rent                                    */
    /*  NOCASHRENTER                     N5               0               Paying no cash rent                                 */
    /*  PCTNOCASHRENTER                  N4               0               Paying no cash rent                                 */
    /*  MEDIANGROSSRENT                  N5            2543               Median rent                                         */
    /*  AVGGROSSRENT                     N5            2374               Average gross rent                                  */
    /*  CASHRENTEROVER30PCT              N5             113               Gross rent 30% or more of HH income                 */
    /*  PCTCASHRENTEROVER30PCT           N4    26.699996948               Gross rent 30% or more of HH income                 */
    /*  CASHRENTEROVER750                N5             193               Gross rent of $750 or more                          */
    /*  PCTCASHRENTEROVER750             N4            45.5               Gross rent of $750 or more                          */
    /*  DATECREATED                      N8           22735               DATECREATED                                         */
    /*  TOTPOP_MOE                       N5             662               TotPop_moe                                          */
    /*  AGE0_4_MOE                       N5             110               Age0_4_moe                                          */
    /*  AGE5_9_MOE                       N5              38               Age5_9_moe                                          */
    /*  AGE10_14_MOE                     N5              15               Age10_14_moe                                        */
    /*  AGE15_19_MOE                     N5              55               Age15_19_moe                                        */
    /*  AGE20_24_MOE                     N5             317               Age20_24_moe                                        */
    /*  AGE25_34_MOE                     N5             263               Age25_34_moe                                        */
    /*  AGE35_44_MOE                     N5             133               Age35_44_moe                                        */
    /*  AGE45_54_MOE                     N5             138               Age45_54_moe                                        */
    /*  AGE55_59_MOE                     N5             118               Age55_59_moe                                        */
    /*  AGE60_64_MOE                     N5             199               Age60_64_moe                                        */
    /*  AGE65_74_MOE                     N5             127               Age65_74_moe                                        */
    /*  AGE75_84_MOE                     N5              81               Age75_84_moe                                        */
    /*  OVER85_MOE                       N5              18               Over85_moe                                          */
    /*  MEDIANAGE_MOE                    N4    4.6999969482               MedianAge_moe                                       */
    /*  OVER5_MOE                        N5                                                                                   */
    /**************************************************************************************************************************/

    /*___              _     _   _       _          _
    |___ \    __ _  __| | __| | | | __ _| |__   ___| |___
      __) |  / _` |/ _` |/ _` | | |/ _` | `_ \ / _ \ / __|
     / __/  | (_| | (_| | (_| | | | (_| | |_) |  __/ \__ \
    |_____|  \__,_|\__,_|\__,_| |_|\__,_|_.__/ \___|_|___/

    */

    proc datasets lib=work; modify want; label
    Age10_14="10 to 14 years"
    Age15_19="15 to 19 years"
    Age20_24="20 to 24 years"
    Age25_34="25 to 34 years"
    Age35_44="35 to 44 years"
    Age45_54="45 to 54 years"
    Age55_59="55 to 59 years"
    Age5_9="5 to 9 years"
    Age60_64="60 to 64 years"
    Age65_74="65 to 74 years"
    Age75_84="75 to 84 years"
    Agriculture="Agriculture, forestry, fishing and hunting, and mining"
    Asian1="Asian"
    Asian2="Asian (alone or in combination)"
    Associates="Associates degree"
    AvgCommute="Mean travel time to work in minutes"
    AvgFamInc="Mean family income"
    AvgFamSize="Average family size"
    AvgGrossRent="Average gross rent"
    AvgHHEarnings="Mean household earnings"
    AvgHHInc="Mean household income"
    AvgHHPubAssist="Mean household cash public assistance income"
    AvgHHRetInc="Mean household retirement income"
    AvgHHSize="Average household size"
    AvgHHSocSec="Mean household social security income"
    AvgHHSuppSecInc="Mean household supplemental security income"
    AvgHValue="Average home value"
    AvgNonFamInc="Mean nonfamily income"
    AvgOwnerHHSize="Average household size of owner-occupied unit"
    AvgRenterHHSize="Average household size of renter-occupied unit"
    Bachelors="Bachelors degree"
    Bachelorsormore="Bachelor degree or higher"
    BirthRate15_19="Per 1,000 women 15 to 19 years old"
    BirthRate20_34="Per 1,000 women 20 to 34 years old"
    BirthRate35_50="Per 1,000 women 35 to 50 years old"
    Black1="Black or African American"
    Black2="Black (alone or in combination)"
    BoatRV="Boat, RV, van, etc."
    BornAbroad="Born in Puerto Rico, U.S. Island areas, or born abroad to American parents"
    BornInCurrState="Born in state of current residence"
    BornInDiffState="Born in different state than current residence"
    BornInUS="Born in United States"
    BornOutsideUS="Population born outside the United States"
    BornOutsideUSNative="Native, born outside U.S."
    BroadbandInternet="With a broadband internet subscription"
    Built1940_1949="Built 1940 to 1949"
    Built1950_1959="Built 1950 to 1959"
    Built1960_1969="Built 1960 to 1969"
    Built1970_1979="Built 1970 to 1979"
    Built1980_1989="Built 1980 to 1989"
    Built1990_1999="Built 1990 to 1999"
    Built2000_2009="Built 2000 to 2009"
    Built2010orLater="Built 2010 or later"
    BuiltBefore1940="Built 1939 or earlier"
    Carpool="Car, truck, or van; carpooled"
    CashRenter="Paying cash rent"
    CashRenterOver30Pct="Gross rent 30% or more of HH income"
    CashRenterOver750="Gross rent of $750 or more"
    Child="Child"
    CivLabForce="Civilian labor force"
    CivLabForceFemales="Females in civilian labor force"
    Civilian="Civilian population 18 years and over"
    Commuters="Workers 16+ who commute to work"
    Computer="Households with a computer"
    ConsOccs="Construction, extraction, installation, maintenance, and repair occupations"
    Construction="Construction"
    CouplesWithKids="With own children under 18 years"
    DialupInternet="With a dial-up internet subscription alone"
    DiffCntySameState="Different county (same state)"
    DiffCounty="Different county (any)"
    DiffHouse="Different house in the U.S."
    DiffHouseSameCounty="Same county"
    DiffState="Different state"
    Disabled18_64="With a disability"
    Disabled="With a disability"
    DisabledElder="With a disability"
    DisabledUnder18="With a disability"
    Divorced="Divorced, and not currently married"
    DriveAlone="Car, truck, or van; drove alone"
    Educ_Health_SocSvcs="Educational services, and health care and social assistance"
    EmployedCLF="Civilian employed population 16 years and over"
    EmployedCLF="Employed civilians"
    EmployedFemales="Employed females"
    EnglishOnly="English only"
    EnrolledOver3="Population 3 years and over enrolled in school"
    FBAfrica="Africa"
    FBAsia="Asia"
    FBEnteredGE2000="Entered U.S. 2000 or later"
    FBEnteredLT2000="Entered U.S. before 2000"
    FBEurope="Europe"
    FBLatinAmerica="South and Central America (includes Mexico)"
    FBMinusSea="Foreign-born population, excluding population born at sea"
    FBNorthAmerica="Northern America"
    FBOceania="Oceania"
    FamHHInc0="Less than $10,000"
    FamHHInc100="$100,000 to $149,999"
    FamHHInc10="$10,000 to $14,999"
    FamHHInc150="$150,000 to $199,999"
    FamHHInc15="$15,000 to $24,999"
    FamHHInc200="$200,000 or more"
    FamHHInc25="$25,000 to $34,999"
    FamHHInc35="$35,000 to $49,999"
    FamHHInc50="$50,000 to $74,999"
    FamHHInc75="$75,000 to $99,999"
    FamHHpop="Living in family households"
    FamHHs="Family households"
    Families="Family households"
    FamsWithKids="With own children under 18 years"
    FarmFishOccs="Farming, fishing, and forestry occupations"
    Females="Female"
    Finance_Ins="Finance and insurance, and real estate and rental and leasing"
    ForeignBorn="Foreign born"
    FullTimeWorkers="All full-time workers"
    FullTimeWorkersFemale="All female full-time workers"
    FullTimeWorkersMale="All male full-time workers"
    GivingBirthPerk="Per 1,000 women 15 to 50 years old"
    GovWorkers="Government workers"
    GradProf="Graduate or professional degree"
    GrandPrntsCaring1or2="1 or 2 years"
    GrandPrntsCaring3or4="3 or 4 years"
    GrandPrntsCaring5orMore="5 or more years"
    GrandPrntsCaring="Grandparents responsible for grandchildren"
    GrandPrntsCaringLT1="Less than 1 year"
    GrandPrntsLvngWithGrndkid="Grandparents living with own grandchildren under 18 years"
    GrpQuarters="Living in group quarters"
    HHFCoal="Coal or coke"
    HHFElectric="Electricity"
    HHFKerosene="Fuel oil, kerosene, etc."
    HHFLPGas="Bottled, tank, or LP gas"
    HHFNoFuel="No fuel used"
    HHFOther="Other fuel"
    HHFSolar="Solar energy"
    HHFUtilGas="Utility gas"
    HHFWood="Wood"
    HHInc0="Less than $10,000"
    HHInc100="$100,000 to $149,999"
    HHInc10="$10,000 to $14,999"
    HHInc150="$150,000 to $199,999"
    HHInc15="$15,000 to $24,999"
    HHInc200="$200,000 or more"
    HHInc25="$25,000 to $34,999"
    HHInc35="$35,000 to $49,999"
    HHInc50="$50,000 to $74,999"
    HHInc75="$75,000 to $99,999"
    HHPop="Household population"
    HHsWithElders="Households with one or more people 65 years and over"
    HHsWithKids="Households with one or more people under 18 years"
    HUsMort="Housing units with a mortgage"
    HUsMortOver30Pct="Owner costs 30% or more of HH income"
    HUsNoMort="Housing units without a mortgage"
    HUsNoMortOver30Pct="Nonmortgage owner costs 30% or more of HH income"
    HawnPI1="Native Hawaiian and Other Pacific Islander"
    HawnPI2="Native Hawaiian (alone or in combination)"
    HighSchool="High school graduate (includes equivalency)"
    HighSchoolOrMore="High school graduate or higher"
    HispanicPop="Hispanic or Latino of any race"
    Householder="Householder"
    Hval100="$100,000 to $149,999"
    Hval150="$150,000 to $199,999"
    Hval200="$200,000 to $299,999"
    Hval300="$300,000 to $499,999"
    Hval500="$500,000 to $999,999"
    Hval50="$50,000 to $99,999"
    HvalOver2Million="$2,000,000 or more"
    HvalOverMillion="$1,000,000 or more"
    HvalUnder50="Less than $50,000"
    InCollege="In college or graduate school"
    InElementary="In elementary school, grades 1-8"
    InHighSchool="In high school, grades 9-12"
    InKindergarten="In kindergarten"
    InNursery="In nursery school, preschool"
    Indian1="American Indian and Alaska Native"
    Indian2="American Indian (alone or in combination)"
    Information="Information"
    LaborForce="In labor force"
    LaborForceFemales="Females in labor force"
    LessThan9th="Less than 9th grade"
    LivedAbroad="Lived abroad 1 year ago"
    LivingAlone="Householder living alone"
    LivingAlone="Living alone"
    Males="Male"
    ManProfOccs="Management, business, science, and arts occupations"
    Manufacturing="Manufacturing"
    Married="Now married, except separated"
    MarriedCouples="Married-couple families"
    MedianAge="Median age in years"
    MedianEarnings="Median earnings for workers"
    MedianEarningsFemale="Median earnings for female full-time, year-round workers"
    MedianEarningsMale="Median earnings for male full-time, year-round workers"
    MedianFamInc="Median family income"
    MedianGrossRent="Median rent"
    MedianHHInc="Median household income"
    MedianHValue="Median home value"
    MedianNonFamInc="Median nonfamily income"
    MedianOwnerCostsMort="Median owner costs"
    MedianOwnerCostsNoMort="Median owner costs"
    Military="In military"
    MobileHomes="Mobile home"
    MobileHomesPerK="Mobile homes per 1000 HUs"
    MovedIn1990_1999="Moved in 1990 to 1999"
    MovedIn2000_2009="Moved in 2000 to 2009"
    MovedIn2010orLater="Moved in 2010 or later"
    MovedInBefore1990="Moved in 1989 or earlier"
    MultiRace="Two or more races"
    NativeEnteredGE2000="Entered U.S. 2000 or later"
    NativeEnteredLT2000="Entered U.S. before 2000"
    Naturalized="Naturalized U.S. citizen"
    NeverMarried="Never married"
    NoCashRenter="Paying no cash rent"
    NoComputer="Households with no computer"
    NoInternet="No internet subscription"
    NoKitchen="Lacking complete kitchen facilities"
    NoPhone="No telephone service available"
    NoPlumbing="Lacking complete plumbing facilities"
    NoVehicles="No vehicles available"
    NonCitizen="Not a U.S. citizen"
    NonFamHHpop="Living in nonfamily households"
    NonFamHHs="Nonfamily households"
    NonHispAmInd="American Indian and Alaska Native alone"
    NonHispAsian="Asian alone"
    NonHispBlack="Black or African American alone"
    NonHispHawnPI="Native Hawaiian and Other Pacific Islander alone"
    NonHispPop="Not Hispanic or Latino"
    NonHispWhite="White alone"
    NonInst18_64="Persons 19 to 64 years"
    NonInstOver65="Persons 65 years and over"
    NonInstUnder18="Persons 18 and under"
    NonInstUnder18="Under 19 years of age"
    NonInstUnder65="Under 65 years of age"
    NonRelative="Nonrelatives"
    NotInLF="Not in labor force"
    NotInsuredUnder18="Without insurance coverage"
    NotInsuredUnder65="Without insurance coverage"
    NumHHEarnings="With earnings"
    NumHHFoodStmp="With food stamp benefits in the past 12 months"
    NumHHPubAssist="With cash public assistance income"
    NumHHRetInc="With retirement income"
    NumHHSocSec="With social security"
    NumHHSuppSecInc="With supplemental security income"
    OccHUs="Occupied housing units"
    OneRace="One race"
    OthLang="Language other than English"
    OthLangEnglishLTD="Speaks English less than very well"
    Other1="Some other race"
    Other2="Some other race (alone or in combination)"
    OtherCommute="Other means of commuting"
    OtherIndustries="Other services, except public administration"
    OtherRelative="Other relatives"
    Over15="15 years and over"
    Over15="Persons 15 years and over"
    Over16="Population 16 years and over"
    Over16Females="Females 16 years and over"
    Over18="18 years and over"
    Over18Females="18 years old and over"
    Over18Males="18 years old and over"
    Over1="Population 1 year and over"
    Over21="21 years and over"
    Over25="25 years and over"
    Over25="Population 25 years and over"
    Over3="Population 3 years and over"
    Over5="5 years and over"
    Over5="Population 5 years and over"
    Over62="62 years and over"
    Over65="65 years and over"
    Over65Alone="65 years and over living alone"
    Over65Females="65 years old and over"
    Over65Males="65 years old and over"
    Over85="85 years and over"
    OwnKidsO6AllPrntsWk="All parents working"
    OwnKidsOver6="(Own) children aged 6 to 17"
    OwnKidsU6AllPrntsWk="All parents working"
    OwnKidsUnder6="(Own) children under 6"
    OwnerOcc="Owner-occupied units"
    OwnerOcc="Owner-occupied"
    OwnerVacRate="Homeowner vacancy rate"
    PCI="Per-capita income"
    PersonsInOwnerUnits="People living in owned homes"
    PersonsInRenterUnits="People living in rental homes"
    PersonsPerRoomHigh="1.51 or more"
    PersonsPerRoomLow="1.00 or less"
    PersonsPerRoomMedium="1.01 to 1.50"
    Poor18to64="Persons aged 18 to 64 in poverty"
    Poor="Persons below poverty"
    PoorFamilies="Family households in poverty"
    PoorInFamily="Persons in families in poverty"
    PoorOver65="Persons over 65 in poverty"
    PoorUnder18="Persons under 18 in poverty"
    PoorUnrelated="Unrelated persons in poverty 15 years and over"
    PovRatio1to2="Poverty ratio in 1 to 2"
    PovRatioOver2="Poverty ratio in 2 and over"
    PovRatioUnderHalf="Poverty ratio under 0.5"
    PovRatiov5tov99="Poverty ratio in 0.5 to 0.99"
    PovUniverse18_64="Persons aged 18 to 64 for whom poverty status is determined"
    PovUniverse="Persons for whom poverty status is determined"
    PovUniverseFamilyPop="Persons in families for whom poverty status is determined"
    PovUniverseOver65="Persons over 65 for whom poverty status is determined"
    PovUniverseUnder18="Persons under 18 for whom poverty status is determined"
    PovUniverseUnrelated="Unrelated individuals for whom poverty status is determined"
    PrivWageWorkers="Private wage and salary workers"
    PrivateInsuranceOnlyUnder65="With private insurance"
    Professional="Professional, scientific, management, and administrative"
    PublicAdmin="Public administration"
    PublicInsuranceUnder65="With public insurance"
    PublicTrans="Public transportation (excluding taxicab)"
    RecreationEtc="Arts, entertainment, and recreation, and accommodation and food services"
    RenterOcc="Renter-occupied units"
    RenterOcc="Renter-occupied"
    RenterVacRate="Rental vacancy rate"
    RetailTrade="Retail trade"
    SalesOffOccs="Sales and office occupations"
    SameHouse="Same house"
    SelfEmpWorkers="Self-employed workers in own not incorporated business"
    Separated="Separated"
    ServiceOccs="Service occupations"
    SingleFathers="With own children under 18 years"
    SingleFemaleFamilies="Female householder, no spouse present"
    SingleMaleFamilies="Male householder, no spouse present"
    SingleMothers="With own children under 18 years"
    SomeCollege="Some college, no degree"
    SomeHighSchool="9th to 12th grade, no diploma"
    Spanish="Speak Spanish"
    SpanishEnglishLTD="Speaks English less than very well"
    Spouse="Spouse"
    TotHHs="Total households"
    TotHUs="Total housing units"
    TotPop="Total population"
    TotPopNonInst="Civilian noninstitutionalized persons"
    TotalOwnerUnits="Total owner units"
    TotalRentalUnits="Total rental units"
    TransOccs="Production, transportation, and material moving occupations"
    Transportation="Transportation and warehousing, and utilities"
    UMPartnerHHsPerK="Unmarried-partner HHs per 1000"
    USNative="U.S. native"
    Under18="Under 18 years of age"
    UnemployedCLF="Unemployed civilians"
    Units10_19="10 to 19 units"
    Units1="Single-family units"
    Units1Attached="Single unit, attached"
    Units1Detached="Single unit, detached"
    Units20up="20 or more units"
    Units2="Duplexes"
    Units3_4="3 or 4 units"
    Units5_9="5 to 9 units"
    UnmarriedGivingBirth="Unmarried women who gave birth"
    UnmarriedGivingBirthPerk="Per 1,000 unmarried women"
    UnmarriedPartner="Unmarried partner"
    UnmarriedWomen15to50="Unmarried women 15 to 50 years old"
    UnpaidFamWorkers="Unpaid family workers"
    VacHUs="Vacant housing units"
    VacantForRent="For rent"
    VacantForSale="For sale"
    VacantSeasonal="For seasonal, recreational, or occasional use"
    Vehicles1="1 vehicle available"
    Vehicles2="2 vehicles available"
    VehiclesGE3="3 or more vehicles available"
    Veteran="Civilian veterans"
    WalkToWork="Walked to work"
    White1="White alone"
    White2="White (alone or in combination)"
    WholesaleTrade="Wholesale trade"
    Widowed="Widowed"
    Women15to19="Women 15 to 19 years of age"
    Women15to50="Women 15 to 50 years old"
    Women20to34="Women 20 to 34 years of age"
    Women35to50="Women 35 to 50 years of age"
    WomenGivingBirth="Women 15 to 50 years old who had a birth in the past 12 months"
    WorkAtHome="Worked at home"
    Worker16="Workers 16 years and over"
    pctAge0_4="Under 5 years"
    pctAge10_14="10 to 14 years"
    pctAge15_19="15 to 19 years"
    pctAge20_24="20 to 24 years"
    pctAge25_34="25 to 34 years"
    pctAge35_44="35 to 44 years"
    pctAge45_54="45 to 54 years"
    pctAge55_59="55 to 59 years"
    pctAge5_9="5 to 9 years"
    pctAge60_64="60 to 64 years"
    pctAge65_74="65 to 74 years"
    pctAge75_84="75 to 84 years"
    pctAgriculture="Agriculture, forestry, fishing and hunting, and mining"
    pctAsian1="Asian"
    pctAsian2="Asian (alone or in combination)"
    pctAssociates="Associates degree"
    pctBachelors="Bachelors degree"
    pctBachelorsormore="Bachelor degree or higher"
    pctBlack1="Black or African American"
    pctBlack2="Black (alone or in combination)"
    pctBoatRV="Boat, RV, van, etc."
    pctBornAbroad="Born in Puerto Rico, U.S. Island areas, or born abroad to American parents"
    pctBornInCurrState="Born in state of current residence"
    pctBornInDiffState="Born in different state than current residence"
    pctBornInUS="Born in United States"
    pctBornOutsideUS="Population born outside the United States"
    pctBornOutsideUSNative="Native, born outside U.S."
    pctBroadbandInternet="With a broadband internet subscription"
    pctBuilt1940_1949="Built 1940 to 1949"
    pctBuilt1950_1959="Built 1950 to 1959"
    pctBuilt1960_1969="Built 1960 to 1969"
    pctBuilt1970_1979="Built 1970 to 1979"
    pctBuilt1980_1989="Built 1980 to 1989"
    pctBuilt1990_1999="Built 1990 to 1999"
    pctBuilt2000_2009="Built 2000 to 2009"
    pctBuilt2010orLater="Built 2010 or later"
    pctBuiltBefore1940="Built 1939 or earlier"
    pctCarpool="Car, truck, or van; carpooled"
    pctCashRenter="Paying cash rent"
    pctCashRenterOver30Pct="Gross rent 30% or more of HH income"
    pctCashRenterOver750="Gross rent of $750 or more"
    pctChild="Child"
    pctCivLabForce="Civilian labor force"
    pctCivLabForceFemales="Females in civilian labor force"
    pctCivilian="Civilian population 18 years and over"
    pctCommuters="Workers 16+ who commute to work"
    pctComputer="Households with a computer"
    pctConsOccs="Construction, extraction, installation, maintenance, and repair occupations"
    pctConstruction="Construction"
    pctCouplesWithKids="With own children under 18 years"
    pctDialupInternet="With a dial-up internet subscription alone"
    pctDiffCntySameState="Different county (same state)"
    pctDiffCounty="Different county (any)"
    pctDiffHouse="Different house in the U.S."
    pctDiffHouseSameCounty="Same county"
    pctDiffState="Different state"
    pctDisabled18_64="With a disability"
    pctDisabled="With a disability"
    pctDisabledElder="With a disability"
    pctDisabledUnder18="With a disability"
    pctDivorced="Divorced, and not currently married"
    pctDriveAlone="Car, truck, or van; drove alone"
    pctEduc_Health_SocSvcs="Educational services, and health care and social assistance"
    pctEmployedCLF="Employed civilians"
    pctEmployedFemales="Employed females"
    pctEnglishOnly="English only"
    pctEnrolledOver3="Population 3 years and over enrolled in school"
    pctFBAfrica="Africa"
    pctFBAsia="Asia"
    pctFBEnteredGE2000="Entered U.S. 2000 or later"
    pctFBEnteredLT2000="Entered U.S. before 2000"
    pctFBEurope="Europe"
    pctFBLatinAmerica="South and Central America (includes Mexico)"
    pctFBMinusSea="Foreign-born population, excluding population born at sea"
    pctFBNorthAmerica="Northern America"
    pctFBOceania="Oceania"
    pctFamHHInc0="Less than $10,000"
    pctFamHHInc100="$100,000 to $149,999"
    pctFamHHInc10="$10,000 to $14,999"
    pctFamHHInc150="$150,000 to $199,999"
    pctFamHHInc15="$15,000 to $24,999"
    pctFamHHInc200="$200,000 or more"
    pctFamHHInc25="$25,000 to $34,999"
    pctFamHHInc35="$35,000 to $49,999"
    pctFamHHInc50="$50,000 to $74,999"
    pctFamHHInc75="$75,000 to $99,999"
    pctFamHHpop="Living in family households"
    pctFamHHs="Family households"
    pctFamilies="Family households"
    pctFamsWithKids="With own children under 18 years"
    pctFarmFishOccs="Farming, fishing, and forestry occupations"
    pctFemales="Female"
    pctFinance_Ins="Finance and insurance, and real estate and rental and leasing"
    pctForeignBorn="Foreign born"
    pctFullTimeWorkersFemale="All female full-time workers"
    pctFullTimeWorkersMale="All male full-time workers"
    pctGovWorkers="Government workers"
    pctGradProf="Graduate or professional degree"
    pctGrandPrntsCaring1or2="1 or 2 years"
    pctGrandPrntsCaring3or4="3 or 4 years"
    pctGrandPrntsCaring5orMore="5 or more years"
    pctGrandPrntsCaring="Grandparents responsible for grandchildren"
    pctGrandPrntsCaringLT1="Less than 1 year"
    pctGrpQuarters="Living in group quarters"
    pctHHFCoal="Coal or coke"
    pctHHFElectric="Electricity"
    pctHHFKerosene="Fuel oil, kerosene, etc."
    pctHHFLPGas="Bottled, tank, or LP gas"
    pctHHFNoFuel="No fuel used"
    pctHHFOther="Other fuel"
    pctHHFSolar="Solar energy"
    pctHHFUtilGas="Utility gas"
    pctHHFWood="Wood"
    pctHHInc0="Less than $10,000"
    pctHHInc100="$100,000 to $149,999"
    pctHHInc10="$10,000 to $14,999"
    pctHHInc150="$150,000 to $199,999"
    pctHHInc15="$15,000 to $24,999"
    pctHHInc200="$200,000 or more"
    pctHHInc25="$25,000 to $34,999"
    pctHHInc35="$35,000 to $49,999"
    pctHHInc50="$50,000 to $74,999"
    pctHHInc75="$75,000 to $99,999"
    pctHHPop="Household population"
    pctHHsWithElders="Households with one or more people 65 years and over"
    pctHHsWithKids="Households with one or more people under 18 years"
    pctHUsMort="Housing units with a mortgage"
    pctHUsMortOver30Pct="Owner costs 30% or more of HH income"
    pctHUsNoMort="Housing units without a mortgage"
    pctHUsNoMortOver30Pct="Nonmortgage owner costs 30% or more of HH income"
    pctHawnPI1="Native Hawaiian and Other Pacific Islander"
    pctHawnPI2="Native Hawaiian (alone or in combination)"
    pctHighSchool="High school graduate (includes equivalency)"
    pctHighSchoolOrMore="High school graduate or higher"
    pctHispanicPop="Hispanic or Latino of any race"
    pctHouseholder="Householder"
    pctHval100="$100,000 to $149,999"
    pctHval150="$150,000 to $199,999"
    pctHval200="$200,000 to $299,999"
    pctHval300="$300,000 to $499,999"
    pctHval500="$500,000 to $999,999"
    pctHval50="$50,000 to $99,999"
    pctHvalOver2Million="$2,000,000 or more"
    pctHvalOverMillion="$1,000,000 or more"
    pctHvalUnder50="Less than $50,000"
    pctInCollege="In college or graduate school"
    pctInElementary="In elementary school, grades 1-8"
    pctInHighSchool="In high school, grades 9-12"
    pctInKindergarten="In kindergarten"
    pctInNursery="In nursery school, preschool"
    pctIndian1="American Indian and Alaska Native"
    pctIndian2="American Indian (alone or in combination)"
    pctInformation="Information"
    pctLaborForce="In labor force"
    pctLaborForceFemales="Females in labor force"
    pctLessThan9th="Less than 9th grade"
    pctLivedAbroad="Lived abroad 1 year ago"
    pctLivingAlone="Householder living alone"
    pctLivingAlone="Living alone"
    pctMales="Male"
    pctManProfOccs="Management, business, science, and arts occupations"
    pctManufacturing="Manufacturing"
    pctMarried="Now married, except separated"
    pctMarriedCouples="Married-couple families"
    pctMilitary="In military"
    pctMobileHomes="Mobile home"
    pctMovedIn1990_1999="Moved in 1990 to 1999"
    pctMovedIn2000_2009="Moved in 2000 to 2009"
    pctMovedIn2010orLater="Moved in 2010 or later"
    pctMovedInBefore1990="Moved in 1989 or earlier"
    pctMultiRace="Two or more races"
    pctNativeEnteredGE2000="Entered U.S. 2000 or later"
    pctNativeEnteredLT2000="Entered U.S. before 2000"
    pctNaturalized="Naturalized U.S. citizen"
    pctNeverMarried="Never married"
    pctNoCashRenter="Paying no cash rent"
    pctNoComputer="Households with no computer"
    pctNoInternet="No internet subscription"
    pctNoKitchen="Lacking complete kitchen facilities"
    pctNoPhone="No telephone service available"
    pctNoPlumbing="Lacking complete plumbing facilities"
    pctNoVehicles="No vehicles available"
    pctNonCitizen="Not a U.S. citizen"
    pctNonFamHHpop="Living in nonfamily households"
    pctNonFamHHs="Nonfamily households"
    pctNonHispAmInd="American Indian and Alaska Native alone"
    pctNonHispAsian="Asian alone"
    pctNonHispBlack="Black or African American alone"
    pctNonHispHawnPI="Native Hawaiian and Other Pacific Islander alone"
    pctNonHispPop="Not Hispanic or Latino"
    pctNonHispWhite="White alone"
    pctNonInst18_64="Persons 19 to 64 years"
    pctNonInstOver65="Persons 65 years and over"
    pctNonInstUnder18="Persons 18 and under"
    pctNonInstUnder18="Under 19 years of age"
    pctNonInstUnder65="Under 65 years of age"
    pctNonRelative="Nonrelatives"
    pctNotInLF="Not in labor force"
    pctNotInsuredUnder18="Without insurance coverage"
    pctNotInsuredUnder65="Without insurance coverage"
    pctNumHHEarnings="With earnings"
    pctNumHHFoodStmp="With food stamp benefits in the past 12 months"
    pctNumHHPubAssist="With cash public assistance income"
    pctNumHHRetInc="With retirement income"
    pctNumHHSocSec="With social security"
    pctNumHHSuppSecInc="With supplemental security income"
    pctOccHUs="Occupied housing units"
    pctOneRace="One race"
    pctOthLang="Language other than English"
    pctOthLangEnglishLTD="Speaks English less than very well"
    pctOther1="Some other race"
    pctOther2="Some other race (alone or in combination)"
    pctOtherCommute="Other means of commuting"
    pctOtherIndustries="Other services, except public administration"
    pctOtherRelative="Other relatives"
    pctOver15="15 years and over"
    pctOver16Females="Females 16 years and over"
    pctOver18="18 years and over"
    pctOver18Females="18 years old and over"
    pctOver18Males="18 years old and over"
    pctOver21="21 years and over"
    pctOver25="25 years and over"
    pctOver5="5 years and over"
    pctOver5="Population 5 years and over"
    pctOver62="62 years and over"
    pctOver65="65 years and over"
    pctOver65Alone="65 years and over living alone"
    pctOver65Females="65 years old and over"
    pctOver65Males="65 years old and over"
    pctOver85="85 years and over"
    pctOwnKidsO6AllPrntsWk="All parents working"
    pctOwnKidsU6AllPrntsWk="All parents working"
    pctOwnerOcc="Owner-occupied"
    pctPersonsInOwnerUnits="People living in owned homes"
    pctPersonsInRenterUnits="People living in rental homes"
    pctPersonsPerRoomHigh="1.51 or more"
    pctPersonsPerRoomLow="1.00 or less"
    pctPersonsPerRoomMedium="1.01 to 1.50"
    pctPoor18to64="Persons aged 18 to 64 in poverty"
    pctPoor="Persons below poverty"
    pctPoorFamilies="Family households in poverty"
    pctPoorInFamily="Persons in families in poverty"
    pctPoorOver65="Persons over 65 in poverty"
    pctPoorUnder18="Persons under 18 in poverty"
    pctPoorUnrelated="Unrelated persons in poverty 15 years and over"
    pctPovRatio1to2="Poverty ratio in 1 to 2"
    pctPovRatioOver2="Poverty ratio in 2 and over"
    pctPovRatioUnderHalf="Poverty ratio under 0.5"
    pctPovRatiov5tov99="Poverty ratio in 0.5 to 0.99"
    pctPrivWageWorkers="Private wage and salary workers"
    pctPrivateInsuranceOnlyUnder65="With private insurance"
    pctProfessional="Professional, scientific, management, and administrative"
    pctPublicAdmin="Public administration"
    pctPublicInsuranceUnder65="With public insurance"
    pctPublicTrans="Public transportation (excluding taxicab)"
    pctRecreationEtc="Arts, entertainment, and recreation, and accommodation and food services"
    pctRenterOcc="Renter-occupied"
    pctRetailTrade="Retail trade"
    pctSalesOffOccs="Sales and office occupations"
    pctSameHouse="Same house"
    pctSelfEmpWorkers="Self-employed workers in own not incorporated business"
    pctSeparated="Separated"
    pctServiceOccs="Service occupations"
    pctSingleFathers="With own children under 18 years"
    pctSingleFemaleFamilies="Female householder, no spouse present"
    pctSingleMaleFamilies="Male householder, no spouse present"
    pctSingleMothers="With own children under 18 years"
    pctSomeCollege="Some college, no degree"
    pctSomeHighSchool="9th to 12th grade, no diploma"
    pctSpanish="Speak Spanish"
    pctSpanishEnglishLTD="Speaks English less than very well"
    pctSpouse="Spouse"
    pctTransOccs="Production, transportation, and material moving occupations"
    pctTransportation="Transportation and warehousing, and utilities"
    pctUSNative="U.S. native"
    pctUnder18="Under 18 years of age"
    pctUnemployedCLF="Unemployed civilians"
    pctUnits10_19="10 to 19 units"
    pctUnits1="Single-family units"
    pctUnits1Attached="Single unit, attached"
    pctUnits1Detached="Single unit, detached"
    pctUnits20up="20 or more units"
    pctUnits2="Duplexes"
    pctUnits3_4="3 or 4 units"
    pctUnits5_9="5 to 9 units"
    pctUnmarriedGivingBirth="Unmarried women who gave birth"
    pctUnmarriedPartner="Unmarried partner"
    pctUnmarriedWomen15to50="Unmarried women 15 to 50 years old"
    pctUnpaidFamWorkers="Unpaid family workers"
    pctVacHUs="Vacant housing units"
    pctVacantForRent="For rent"
    pctVacantForSale="For sale"
    pctVacantSeasonal="For seasonal, recreational, or occasional use"
    pctVehicles1="1 vehicle available"
    pctVehicles2="2 vehicles available"
    pctVehiclesGE3="3 or more vehicles available"
    pctVeteran="Civilian veterans"
    pctWalkToWork="Walked to work"
    pctWhite1="White alone"
    pctWhite2="White (alone or in combination)"
    pctWholesaleTrade="Wholesale trade"
    pctWidowed="Widowed"
    pctWomen15to19="Women 15 to 19 years of age"
    pctWomen20to34="Women 20 to 34 years of age"
    pctWomen35to50="Women 35 to 50 years of age"
    pctWomenGivingBirth="Women 15 to 50 years old who had a birth in the past 12 months"
    pctWorkAtHome="Worked at home"
    ;run;quit;


    /*____            _       _           _
    |___ /   _ __ ___| | __ _| |_ ___  __| |  _ __ ___ _ __   ___  ___
      |_ \  | `__/ _ \ |/ _` | __/ _ \/ _` | | `__/ _ \ `_ \ / _ \/ __|
     ___) | | | |  __/ | (_| | ||  __/ (_| | | | |  __/ |_) | (_) \__ \
    |____/  |_|  \___|_|\__,_|\__\___|\__,_| |_|  \___| .__/ \___/|___/
                                                      |_|
    */

    https://github.com/rogerjdeangelis/utl-Open-GIS-Data-Access-for-the-Commonwealth-of-Pennsylvania
    https://github.com/rogerjdeangelis/utl-add-points-to-a-map-of-slovakia
    https://github.com/rogerjdeangelis/utl-an-additional-algorithm-to-map-codes-to-decodes
    https://github.com/rogerjdeangelis/utl-anonymization-of-zipcodes_000501-through_99950_encrypting
    https://github.com/rogerjdeangelis/utl-compute-the-area-inside-a-latitude-and-longitude-polygon-in-square-km-gis-graph
    https://github.com/rogerjdeangelis/utl-computing-the-minimum-distance-between-a-polygon-and-a-point-gis-graph-plot-ai
    https://github.com/rogerjdeangelis/utl-converting-census-tracks-to-latitiudes-and-longitudes-using-R-packages
    https://github.com/rogerjdeangelis/utl-converting-us-gps-decimal-latitude-and-longitude-to-census-zcta-zipcodes-geocode
    https://github.com/rogerjdeangelis/utl-creating-zipcode-zcta-choropleth-maps-in-R-and-SAS
    https://github.com/rogerjdeangelis/utl-dept-of-trans-address-database-to-sas-wps-tables-for-geocoding-and-reverse-geocoding
    https://github.com/rogerjdeangelis/utl-drawing-a-world-map-using-the-eckert-projection-ggplot-map-rnaturalearth
    https://github.com/rogerjdeangelis/utl-free-unlimited-geocoding-reverse-geocoding-wps-aprox-I41-million-addresses-with-gps
    https://github.com/rogerjdeangelis/utl-gis-census-zipcode-maps-no-credit-card-api-or-restrictions-wps-r-tmap
    https://github.com/rogerjdeangelis/utl-gis-download-all-the-census_2023-tiger-line-files
    https://github.com/rogerjdeangelis/utl-gis-mapping-with-r-package-rnaturalearth-no-api-credit-card-or-access-limits-
    https://github.com/rogerjdeangelis/utl-given-a-list-of-messy-addresses-geocode-and-reverse-geocode-using-us-address-database
    https://github.com/rogerjdeangelis/utl-ipv4-ipaddress-in-four-binary-bytes-or-five-or-fewer-printable-characters
    https://github.com/rogerjdeangelis/utl-openaddress-database-to-sas-wps-tables-for-geocoding-and-reverse-geocoding
    https://github.com/rogerjdeangelis/utl-programatically-download-census-tiger-shapefiles-and-map-us-labeling-largest-cities
    https://github.com/rogerjdeangelis/utl-python-send-a-list-of-zipcodes-to-a-website-and-get-associated--latititude-and-longitudes
    https://github.com/rogerjdeangelis/utl-standardize-address-suffix-using-usps-abreviations
    https://github.com/rogerjdeangelis/utl-use-geo-fencing-to-find-all-addresses-in-a-latitude-longitude-quadrangle-reverse-geocoding
    https://github.com/rogerjdeangelis/utl_US_address-standardization
    https://github.com/rogerjdeangelis/utl_geocode_and_reverse_geocode_netherland_addresses_and_latitudes_longitudes
    https://github.com/rogerjdeangelis/utl_geocode_reverse_geocode
    https://github.com/rogerjdeangelis/utl_geocoding_us_cities_using_sas_zipcode_dataset
    https://github.com/rogerjdeangelis/utl_graphics_zipcode_boundary_maps
    https://github.com/rogerjdeangelis/utl_web_scrape_23_separate_pages_one_per_state_for_all_whole_food_store_addresses

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
