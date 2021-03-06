# utl_sort_and_copy_schema1_tables_to_schema2
Creating a sorted copy of all tables(sas datasets) in a schema(SAS library)

    ```  Creating a sorted copy of all tables(sas datasets) in a schema(SAS library).                                                                                 ```
    ```                                                                                                                                                               ```
    ```     I am using libname 'work' as the out library and libname 'tmp' as input library                                                                           ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE - (minus error checking)                                                                                                                     ```
    ```     ======================================                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```       COMPILE TIME (if _n_=0 DOSUBL)                                                                                                                          ```
    ```             * get meta data - table names in source schema;                                                                                                   ```
    ```             select quote(memname) into :mems separated by "," from sashelp.vtable where libname="TMP"                                                         ```
    ```                                                                                                                                                               ```
    ```       MAINLINE                                                                                                                                                ```
    ```         do mem=&mems;                                                                                                                                         ```
    ```             call symputx('mem',mem);                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```       DOSUBL Subroutine                                                                                                                                       ```
    ```           proc sort data=tmp.&mem out=work(drop=age) noequals;                                                                                                ```
    ```              by name;                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```       MAINLINE                                                                                                                                                ```
    ```           Error check and stop if ERROR                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/RtmgpZ                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/How-to-iteratively-process-datasets-for-one-procedure/m-p/404919                                         ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```   Two SAS datsets in library 'TMP'                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```   TMP.CLASS total obs=19                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```     NAME       SEX    AGE    HEIGHT    WEIGHT                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     Alfred      M      14     69.0      112.5                                                                                                                 ```
    ```     Alice       F      13     56.5       84.0                                                                                                                 ```
    ```     Barbara     F      13     65.3       98.0                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```   TMP.CLASSFIT total obs=19                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```     NAME       SEX    AGE    HEIGHT    WEIGHT    PREDICT    LOWERMEAN    UPPERMEAN     LOWER      UPPER                                                       ```
    ```                                                                                                                                                               ```
    ```     Joyce       F      11     51.3       50.5     56.993      43.804       70.182      29.883     84.103                                                      ```
    ```     Louise      F      12     56.3       77.0     76.488      67.960       85.017      51.315    101.662                                                      ```
    ```     Alice       F      13     56.5       84.0     77.268      68.907       85.630      52.150    102.386                                                      ```
    ```     James       M      12     57.3       83.0     80.388      72.667       88.108      55.476    105.299                                                      ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  WANT (3 datasets in work (has logging dataset))                                                                                                              ```
    ```  ========================                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```   Three datasets in the work library sorted on name  log.sas7bdat, class.sas7bdat and classfit.sas7bdat                                                       ```
    ```                                                                                                                                                               ```
    ```   WORK.LOG total obs=2                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```    MEM         RC     STATUS                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    CLASS        0    Completed                                                                                                                                ```
    ```    CLASSFIT     0    Completed                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```   WORK.CLASSFIT total obs=19                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    NAME       SEX    HEIGHT    WEIGHT    PREDICT    LOWERMEAN    UPPERMEAN     LOWER      UPPER                                                               ```
    ```                                                                                                                                                               ```
    ```    Alfred      M      69.0      112.5    126.006     116.942      135.071     100.646    151.367                                                              ```
    ```    Alice       F      56.5       84.0     77.268      68.907       85.630      52.150    102.386                                                              ```
    ```    Barbara     F      65.3       98.0    111.580     105.260      117.899      87.066    136.094                                                              ```
    ```                                                                                                                                                               ```
    ```   WORK.CLASSFIT total obs=19                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```     NAME       SEX    AGE    HEIGHT    WEIGHT                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     Alfred      M      14     69.0      112.5                                                                                                                 ```
    ```     Alice       F      13     56.5       84.0                                                                                                                 ```
    ```     Barbara     F      13     65.3       98.0                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  libname tmp "d:/tmp";                                                                                                                                        ```
    ```  proc copy in=sashelp out=tmp;                                                                                                                                ```
    ```    select class classfit;                                                                                                                                     ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %symdel mem mems / nowarn; * just in case;                                                                                                                   ```
    ```  data log;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```     * get meta data;                                                                                                                                          ```
    ```     if _n_=0 then do;                                                                                                                                         ```
    ```        %let rc=%sysfunc(dosubl('                                                                                                                              ```
    ```           proc sql ;                                                                                                                                          ```
    ```             select quote(memname) into :mems separated by "," from sashelp.vtable where libname="TMP"                                                         ```
    ```           ;quit;                                                                                                                                              ```
    ```        '));                                                                                                                                                   ```
    ```     end;                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```     do mem=&mems;                                                                                                                                             ```
    ```        call symputx('mem',mem);                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```        rc=dosubl('                                                                                                                                            ```
    ```           proc sort data=tmp.&mem out=work.&mem(drop=age) noequals;                                                                                           ```
    ```              by name;                                                                                                                                         ```
    ```           run;quit;                                                                                                                                           ```
    ```           %let ErrortextData= &syserrortext;                                                                                                                  ```
    ```           %let ErrorcodeData= &syserr;                                                                                                                        ```
    ```        ');                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```         ErrorTextLib  =  symget('ErrorTextLib');                                                                                                              ```
    ```         ErrorTextData =  symget('ErrorTextData');                                                                                                             ```
    ```         ErrorCodeLib  =  symget('ErrorCodeLib');                                                                                                              ```
    ```         ErrorCodeData =  symget('ErrorCodeData');                                                                                                             ```
    ```                                                                                                                                                               ```
    ```         if    rc ne 0                                                                                                                                         ```
    ```            or ErrorCodeLib  ne " "                                                                                                                            ```
    ```            or ErrorCodeData ne "0" Then do;                                                                                                                   ```
    ```             Status        =  "Failed      ";                                                                                                                  ```
    ```             output;                                                                                                                                           ```
    ```             stop;                                                                                                                                             ```
    ```         end;                                                                                                                                                  ```
    ```         else do;                                                                                                                                              ```
    ```            Status="Completed";                                                                                                                                ```
    ```         end;                                                                                                                                                  ```
    ```         output;                                                                                                                                               ```
    ```     end;                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    stop;                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```

