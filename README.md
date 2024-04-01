# utl-r-compute-the-area--of-an-image-which-is-under-a-curve-AI-image-processing-AI
    %let pgm=utl-r-compute-the-area--of-an-image-which-is-under-a-curve-AI-image-processing-AI;

    R compute the area of an image which is under a curve AI image processing AI

      1 compute area
      2 create graph

    Has implications for image processing when using
    https://github.com/rogerjdeangelis/utl_digitize_data_from_image

    see
    https://goo.gl/Btm1In
    http://stackoverflow.com/questions/42640558/calculating-area-between-two-plots-in-r

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                   X                                                                                    */
    /*        0       135      270      405      540      675      810                                                        */
    /*     Y +-+--------+--------+--------+--------+--------+--------+--+                                                     */
    /*       |                                                          |    _                   _                            */
    /*       |                                                          |   (_)_ __  _ __  _   _| |_ ___                      */
    /*       | AREA UNDER TWO POINT EAUATIONS                           |   | | `_ \| `_ \| | | | __/ __|                     */
    /*       | BAR 1 FROM 125 to 175                                    |   | | | | | |_) | |_| | |_\__ \                     */
    /*       +                                                          +   |_|_| |_| .__/ \__,_|\__|___/                     */
    /*       | TWO POINT EQUATION                                       |           |_|                                       */
    /*       |  X      Y                                                |                                                     */
    /*       | 101 1.04591                                              |    BAR DATA                                         */
    /*       | 201 0.79109                                              |
    /*       |                                                          |    Up to 40 obs SD1.BARDF total obs=3               */
    /*       + Y=-.00255*X+1.30                                         +                                                     */
    /*       |                                                          |    Obs     X     HEIGHT    WIDTH                    */
    /*       | BAR WIDTH = 50 (125 to 175)                              |                                                     */
    /*       | CENTERED AT 150                                          |     1     150     1.40       50                     */
    /*       |                                                          |     2     500     1.40       70                     */
    /*       + INTERGRATING                                             +     3     750     1.18      100                     */
    /*       |                                                          |                                                     */
    /*       |  / 125                                                   |    LINE DATA                                        */
    /*       | |  -.00255*X  + 1.30328 dx           Just area under bar |                                                     */
    /*       | / 175                                    AREA UNDER      |    Up to 40 obs SD1.DF total obs=9                  */
    /*       +                         175              BAR HEIGHT=1.18 +                                                     */
    /*       | AREA=-.00127*X**2+1.30*x|                                |    Obs     X1       Y1                              */
    /*       |                         125               Hgt  Wdt|h     |                                                     */
    /*       |                                          1.18  100       |     1       1    0.84339                            */
    /*       | AREA=189.0271-142.9881=46.04                             |     2     101    1.04591                            */
    /*       +                                          1.18*100 = 118  +     3     201    0.79109                            */
    /*       |                                                          |     4     301    1.39882                            */
    /*       |                                                          |     5     401    1.08238                            */
    /*       |          1.40                   1.40                     |     6     501    0.79488                            */
    /*  1.40 +         +----+                 +----+ AREA=1.18*(700-800)+     7     601    1.12186                            */
    /*       |         |    |       /\        |    |           =118     |     8     701    1.18000                            */
    /*       |         |AREA|      /  \       |AREA|           1.18     |     9     801    1.18000                            */
    /*       | X   Y   |    |     /    \      |    |        .-+-----+   |                                                     */
    /*       |101,1.04 |23.9|    /      \     |38.6|  -----/  |     |   |                 _               _                   */
    /*  1.05 +       / \    |   /         \   |    | /        |     |   +      ___  _   _| |_ _ __  _   _| |_                 */
    /*       |      /  |\   |  /           \  |    |/         |     |   |     / _ \| | | | __| `_ \| | | | __|                */
    /*       |    /    | \  | /              \|    /          |     |   |    | (_) | |_| | |_| |_) | |_| | |_                 */
    /*       |  /      |  \ |/ X   Y          |\  /|Two       |     |   |     \___/ \__,_|\__| .__/ \__,_|\__|                */
    /*       |         |   \/ 201,0.79        | \/ |Equations |     |   |                    |_|                              */
    /*  0.70 +         |    |                 |    |          |     |   +                                                     */
    /*       |         |    |Y=-.00255*X+1.30 |    |          |     |   |      WANT                                           */
    /*       |         |AREA| for 125 to 175  |AREA|          | AREA|   |      ====                                           */
    /*       |         |    |                 |    |          |     |   |                                                     */
    /*       |         |46.1|                 |59.4|          | 118 |   |      Obs     AREAS                                  */
    /*  0.35 +         |    |                 |    |          |     |   +                                                     */
    /*       |         |    |                 |    |          |     |   |       1      46.052                                 */
    /*       |         |    |                 |    |          |     |   |       2      59.395                                 */
    /*       |         |    |                 |    |          |     |   |       3     118.000                                 */
    /*       |         |    |                 |    |          |     |   |                                                     */
    /*  0.00 +         +----+                 +----+          +-----+   +                                                     */
    /*       |       125   175              465   535       700    800  |                                                     */
    /*       +-+--------+--------+--------+--------+--------+--------+--+                                                     */
    /*         0       135      270      405      540      640      810                                                       */
    /*                                    Y                                                                                   */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */


    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.bardf;
    input X HEIGHT WIDTH;
    cards4;
    150 1.4 50
    500 1.4 70
    750 1.18 100
    ;;;;
    run;quit;

    data sd1.df;
    input x1 y1;
    cards4;
      1 0.84339
    101 1.04591
    201 0.79109
    301 1.39882
    401 1.08238
    501 0.79488
    601 1.12186
    701 1.18
    801 1.18
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* BARS                                                                                                                   */
    /*                                                                                                                        */
    /* SD1.BARDF total obs=3 01APR2024:09:                                                                                    */
    /*                                                                                                                        */
    /* Obs     X     HEIGHT    WIDTH                                                                                          */
    /*                                                                                                                        */
    /*  1     150     1.40       50                                                                                           */
    /*  2     500     1.40       70                                                                                           */
    /*  3     750     1.18      100                                                                                           */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* TWO POINT EQUATION INPUT                                                                                               */
    /*                                                                                                                        */
    /* SD1.DF total obs=9 01APR2024:09:33:29                                                                                  */
    /*                                                                                                                        */
    /* Obs     X1       Y1                                                                                                    */
    /*                                                                                                                        */
    /*  1       1    0.84339                                                                                                  */
    /*  2     101    1.04591                                                                                                  */
    /*  3     201    0.79109                                                                                                  */
    /*  4     301    1.39882                                                                                                  */
    /*  5     401    1.08238                                                                                                  */
    /*  6     501    0.79488                                                                                                  */
    /*  7     601    1.12186                                                                                                  */
    /*  8     701    1.18000                                                                                                  */
    /*  9     801    1.18000                                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.1";
    libname wrk "%sysfunc(pathname(work))";
    proc r;
    submit;
    library(ggplot2);
    library(haven);
    df <- read_sas("d:/sd1/df.sas7bdat");
    bardf <- read_sas("d:/sd1/bardf.sas7bdat");
    df;
    bardf;
    areas<-mapply(function(x, h, w){
        integrate(function(v){pmin(approxfun(df$X1, df$Y1)(v), h)},
                  lower = x - .5 * w,
                  upper = x + .5 * w
        )$value},
        bardf$X, bardf$HEIGHT, bardf$WIDTH);
    areas;
    endsubmit;
    import r=areas data=wrk.areas;
    run;quit;
    ');


    %utl_rbegin;
    parmcards4;
    library(haven);
    df    <- read_sas("d:/sd1/df.sas7bdat");
    bardf <- read_sas("d:/sd1/bardf.sas7bdat");
    df;
    bardf;
    areas<-mapply(function(x, h, w){
        integrate(function(v){pmin(approxfun(df$X1, df$Y1)(v), h)},
                  lower = x - .5 * w,
                  upper = x + .5 * w
        )$value},
        bardf$X, bardf$HEIGHT, bardf$WIDTH);
    areas;
    ;;;;
    %utl_rend;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  AREAS                                                                                                                 */
    /*                                                                                                                        */
    /*  [1]  46.05241  59.39455 117.99968                                                                                     */
    /*                                                                                                                        */
    /*  | A tibble: 9 × 2                                                                                                     */
    /*       X1      Y1                                                                                                       */
    /*    <dbl>   <dbl>                                                                                                       */
    /*  1     1 0.84339                                                                                                       */
    /*  2   101 1.04591                                                                                                       */
    /*  3   201 0.79109                                                                                                       */
    /*  4   301 1.39882                                                                                                       */
    /*  5   401 1.08238                                                                                                       */
    /*  6   501 0.79488                                                                                                       */
    /*  7   601 1.12186                                                                                                       */
    /*  8   701 1.18000                                                                                                       */
    /*  9   801 1.18000                                                                                                       */
    /*  # A tibble: 3 × 3                                                                                                     */
    /*        X HEIGHT WIDTH                                                                                                  */
    /*    <dbl>  <dbl> <dbl>                                                                                                  */
    /*  1   150   1.40    50                                                                                                  */
    /*  2   500   1.40    70                                                                                                  */
    /*  3   750   1.18   100                                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*___                        _                               _
    |___ \    ___ _ __ ___  __ _| |_ ___    __ _ _ __ __ _ _ __ | |__
      __) |  / __| `__/ _ \/ _` | __/ _ \  / _` | `__/ _` | `_ \| `_ \
     / __/  | (__| | |  __/ (_| | ||  __/ | (_| | | | (_| | |_) | | | |
    |_____|  \___|_|  \___|\__,_|\__\___|  \__, |_|  \__,_| .__/|_| |_|
                                           |___/          |_|
    */


    %macro xpn;
       retain x 1  y 0.84339;
       input x1 y1;
       lagx1=lag(x1);
       lagy1=lag(y1);
       if _n_ > 1 then do;
          do x=lagx1+1 to x1;
            inc= (y1-lagy1)/(x1-lagx1);
            y=y+inc;
            output;
          end;
       end;
       else output;
    %mend xpn;

    data lyn(keep=x y rename=(x=xl y=yl));
     %xpn;
    cards4;
      1    0.84339
    101    1.04591
    201    0.79109
    301    1.39882
    401    1.08238
    501    0.79488
    601    1.12186
    701    1.18
    801    1.18
    ;;;;
    run;quit;

    data bar;
      set sd1.bardf ;
      half=width/2;
      do xb=x-half to x+half;
        do yb=0 to height by .01;
           output;
        end;
      end;
    run;quit;

    data barlyn;
      merge bar(in=b) lyn;
      if b;
      keep xb yb xl yl;
    run;quit;

    options ls=64 ps=32;
    proc plot data=barlyn;
      plot yl*xl='.' yb*xb='#' /overlay box;
    run;quit;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
R compute the area of an image which is under a curve AI image processing AI
