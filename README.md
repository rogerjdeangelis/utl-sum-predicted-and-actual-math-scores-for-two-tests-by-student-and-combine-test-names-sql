# utl-sum-predicted-and-actual-math-scores-for-two-tests-by-student-and-combine-test-names-sql
Sql r python and sas sum predicted and actual math scores for two tests by student and combine test names 
    %let pgm=utl-sum-predicted-and-actual-math-scores-for-two-tests-by-student-and-combine-test-names-sql;

    Sql r python and sas sum predicted and actual math scores for two tests by student and combine test names

    github
    https://tinyurl.com/ycxu5pfp
    https://stackoverflow.com/questions/78931674/r-adding-maintaining-and-changes-values-when-summing-rows

       Thee Solutions
          1 sas sql
          2 r sql
          3 python sql


    https://github.com/rogerjdeangelis/utl-sum-predicted-and-actual-math-scores-for-two-tests-by-student-and-combine-test-names-sql

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                                    |                                                                   */
    /*             INPUT                                  |         PROCESS & OUTPUT                                          */
    /*                                                    |                                                                   */
    /*                                                    |  Sum predicted & actual math scores                               */
    /*                                                    |  for two tests by student and combine test names                  */
    /*                                                    |                                                                   */
    /*  NAME      MEASURE    EXTRA    PREDICTED    ACTUAL |  NAME       MEASURE     SUMPRED    SUMACT    EXTRA                */
    /*                                                    |                                                                   */
    /*                                                    |                                                                   */
    /*  Ashley    Score_A     No          8           2   |  Ashley    Score_A_B       13         5       No                  */
    /*  Ashley    Score_B     No          5           3   |                                                                   */
    /*                                                    |                                                                   */
    /*  Ben       Score_A     Yes         7           7   |  Ben       Score_A_B       14        10       Yes                 */
    /*  Ben       Score_B     Yes         7           3   |                                                                   */
    /*                                                    |                                                                   */
    /*  Clark     Score_A     Yes         9           6   |                                                                   */
    /*  Clark     Score_B     Yes         6          10   |  Clark     Score_A_B       15        16       Yes                 */
    /*                                                    |                                                                   */
    /*                                                    |                                                                   */
    /*                                                    | SAS R & PYTHON (exacly the same code)                             */
    /*                                                    | =====================================                             */
    /*                                                    |                                                                   */
    /*                                                    |  proc sql;                                                        */
    /*                                                    |    create                                                         */
    /*                                                    |      table want as                                                */
    /*                                                    |    select                                                         */
    /*                                                    |     distinct                                                      */
    /*                                                    |      name                                                         */
    /*                                                    |     ,substr(measure,1,6)||'A_B' as measure                        */
    /*                                                    |     ,sum(predicted) as sumPred                                    */
    /*                                                    |     ,sum(actual)    as sumAct                                     */
    /*                                                    |     ,min(extra)     as extra                                      */
    /*                                                    |    from                                                           */
    /*                                                    |      sd1.have                                                     */
    /*                                                    |    group                                                          */
    /*                                                    |      by name                                                      */
    /*                                                    |  ;quit;                                                           */
    /*                                                    |                                                                   */
    /*                                                    |                                                                   */
    /*                                                    |  R                                                                */
    /*                                                    |  =                                                                */
    /*                                                    |                                                                   */
    /*                                                    |  df |>                                                            */
    /*                                                    |    dplyr::summarise(                                              */
    /*                                                    |      Measure_ID = toString(sub("Score_", "", Measure_ID)),        */
    /*                                                    |      Predicted = sum(Predicted),                                  */
    /*                                                    |      Actual = sum(Actual),                                        */
    /*                                                    |      Extra = unique(Extra),                                       */
    /*                                                    |      .by = Name)                                                  */
    /*                                                    |                                                                   */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    libname sd1 "d:/sd1";
    options validvarname=upcase;
    data sd1.have;
     informat name measure $8. extra $4.;
     input
        name measure predicted actual extra ;
    cards4;
    Ashley Score_A 8 2 No
    Ashley Score_B 5 3 No
     Ben   Score_A 7 7 Yes
     Ben   Score_B 7 3 Yes
     Clark Score_A 9 6 Yes
     Clark Score_B 6 10 Yes
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  SD1.HAVE total obs=6                                                                                                  */
    /*                                                                                                                        */
    /*  Obs    NAME      MEASURE    EXTRA    PREDICTED    ACTUAL                                                              */
    /*                                                                                                                        */
    /*   1     Ashley    Score_A     No          8           2                                                                */
    /*   2     Ashley    Score_B     No          5           3                                                                */
    /*   3     Ben       Score_A     Yes         7           7                                                                */
    /*   4     Ben       Score_B     Yes         7           3                                                                */
    /*   5     Clark     Score_A     Yes         9           6                                                                */
    /*   6     Clark     Score_B     Yes         6          10                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    proc sql;
      create
        table want as
      select
       distinct
        name
       ,substr(measure,1,6)||'A_B' as measure
       ,sum(predicted) as sumPred
       ,sum(actual)    as sumAct
       ,min(extra)     as extra
      from
        sd1.have
      group
        by name
    ;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Obs    NAME       MEASURE     SUMPRED    SUMACT    EXTRA                                                               */
    /*                                                                                                                        */
    /*  1     Ashley    Score_A_B       13         5       No                                                                 */
    /*  2     Ben       Score_A_B       14        10       Yes                                                                */
    /*  3     Clark     Score_A_B       15        16       Yes                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(sqldf)
    library(haven)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    print(have);
    want<-sqldf('
      select
       distinct
        name
       ,substr(measure,1,6)||"A_B" as measure
       ,sum(predicted) as sumPred
       ,sum(actual)    as sumAct
       ,min(extra)     as extra
      from
        have
      group
        by name
      ')
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rwant"
         );
    ;;;;
    %utl_rendx;

    proc print data=sd1.rwant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* ROWNAMES    NAME      MEASURE    SUMPRED    SUMACT    EXTRA                                                            */
    /*                                                                                                                        */
    /*     1       Ashley    Score_A_B     13         5       No                                                              */
    /*     2       Ben       Score_A_B     14        10       Yes                                                             */
    /*     3       Clark     Score_A_B     15        16       Yes                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */
    %utl_pybeginx;
    parmcards4;
    import pyperclip
    import os
    from os import path
    import sys
    import subprocess
    import time
    import pandas as pd
    import pyreadstat as ps
    import numpy as np
    import pandas as pd
    from pandasql import sqldf
    mysql = lambda q: sqldf(q, globals())
    from pandasql import PandaSQL
    pdsql = PandaSQL(persist=True)
    sqlite3conn = next(pdsql.conn.gen).connection.connection
    sqlite3conn.enable_load_extension(True)
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll')
    mysql = lambda q: sqldf(q, globals())
    have, meta = ps.read_sas7bdat("d:/sd1/have.sas7bdat")
    exec(open('c:/temp/fn_tosas9.py').read())
    print(have);
    want = pdsql("""
      select
       distinct
        name
       ,substr(measure,1,6)||"A_B" as measure
       ,sum(predicted) as sumPred
       ,sum(actual)    as sumAct
       ,min(extra)     as extra
      from
        have
      group
        by name
    """)
    print(want)
    fn_tosas9(
       want
       ,dfstr="pywant"
       ,timeest=3
       )
    ;;;;
    %utl_pyendx;

    libname tmp "c:/temp";
    proc print data=tmp.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  PYTHON                                                                                                                */
    /*                                                                                                                        */
    /*       NAME    measure  sumPred  sumAct extra                                                                           */
    /*  0  Ashley  Score_A_B     13.0     5.0    No                                                                           */
    /*  1     Ben  Score_A_B     14.0    10.0   Yes                                                                           */
    /*  2   Clark  Score_A_B     15.0    16.0   Yes                                                                           */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  SAS                                                                                                                   */
    /*                                                                                                                        */
    /*       NAME    measure  sumPred  sumAct extra                                                                           */
    /*  0  Ashley  Score_A_B     13.0     5.0    No                                                                           */
    /*  1     Ben  Score_A_B     14.0    10.0   Yes                                                                           */
    /*  2   Clark  Score_A_B     15.0    16.0   Yes                                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
