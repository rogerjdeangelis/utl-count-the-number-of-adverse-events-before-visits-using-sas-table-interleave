# utl-count-the-number-of-adverse-events-before-visits-using-sas-table-interleave
Count the number of adverse events before visits using sas table interleave;
    %let pgm=utl-count-the-number-of-adverse-events-before-visits-using-sas-table-interleave;

    %stop_submission;

    Count the number of adverse events before visits using sas table interleave;
    
    github
    https://tinyurl.com/4r8vjs68
    https://github.com/rogerjdeangelis/utl-count-the-number-of-adverse-events-before-visits-using-sas-table-interleave

    sas communities
    https://tinyurl.com/2myam2x6
    https://communities.sas.com/t5/SAS-Programming/count-events-in-one-dataset-between-two-visits-in-another/m-p/767332#M243271

    ChrisNZ
    https://communities.sas.com/t5/user/viewprofilepage/user-id/16961

    /*************************************************************************************************************************/
    /* INPUT                    | PROCESS  (ADVERSE EVENTS ON OR BEFORE VISIT)         | OUTPUT                              */
    /* =====                    | =======                                              | ======                              */
    /* data adverse_events;     | ID                                                   | ID    VISIT    N                    */
    /*  input date $10.;        | ==                                                   |                                     */
    /* cards;                   |                                                      | 1       1      2                    */
    /* 2020-09-01               | 1 count adverse events <= visit 2020-09-03           | 1       2      3                    */
    /* 2020-09-03               |                                                      | 1       3      4                    */
    /* 2020-09-08               | avverse_events count                                 |                                     */
    /* 2020-09-10               |                                                      |                                     */
    /* 2020-09-17               |  2020-09-01                                          |                                     */
    /* 2020-09-20               |  2020-09-03     2  Two before visit                  |                                     */
    /* 2020-09-23               |                                                      |                                     */
    /* 2020-09-26               |                                                      |                                     */
    /* 2020-09-29               | 2 count adverse events > 2020-09-03 & <= 2020-09-17  |                                     */
    /* 2020-10-02               |                                                      |                                     */
    /* ;;;;                     | avverse_events count                                 |                                     */
    /* run;quit;                |                                                      |                                     */
    /*                          |   2020-09-08                                         |                                     */
    /* data visits;             |   2020-09-10                                         |                                     */
    /*  input id date $10.;     |   2020-09-17    3                                    |                                     */
    /* cards4;                  |                                                      |                                     */
    /* 1 2020-09-03             | 3 count adverse events > 2020-09-017 <= 2020-10-0    |                                     */
    /* 2 2020-09-17             |                                                      |                                     */
    /* 3 2020-10-01             | avverse_events count                                 |                                     */
    /* ;;;;                     |                                                      |                                     */
    /* run;quit;                |   2020-09-20                                         |                                     */
    /*                          |   2020-09-23                                         |                                     */
    /*                          |   2020-09-26                                         |                                     */
    /*                          |   2020-09-29    4                                    |                                     */
    /*                          |                                                      |                                     */
    /*                          | Result                                               |                                     */
    /*                          |                                                      |                                     */
    /*                          |   ID   COUNT                                         |                                     */
    /*                          |                                                      |                                     */
    /*                          |    1     2                                           |                                     */
    /*                          |    2     3                                           |                                     */
    /*                          |    3     4                                           |                                     */
    /*                          |                                                      |                                     */
    /*                          | NOTE: BY DATE below puts the                         |                                     */
    /*                          |       dates in the correct sort order                |                                     */
    /*                          |                                                      |                                     */
    /*                          | data WANT;                                           |                                     */
    /*                          |   set EVENTS(in=E)                                   |                                     */
    /*                          |       VISITS(in=V);                                  |                                     */
    /*                          |   by DATE;                                           |                                     */
    /*                          | run;quit;                                            |                                     */
    /*                          |                                                      |                                     */
    /*                          |    DATE     ID                                       |                                     */
    /*                          |                                                      |                                     */
    /*                          | 2020-09-01   .                                       |                                     */
    /*                          | 2020-09-03   .                                       |                                     */
    /*                          | 2020-09-03   1 visit from vists table                |                                     */
    /*                          | 2020-09-08   .                                       |                                     */
    /*                          | 2020-09-10   .                                       |                                     */
    /*                          | 2020-09-17   .                                       |                                     */
    /*                          | 2020-09-17   2 visit from vists table                |                                     */
    /*                          | 2020-09-20   .                                       |                                     */
    /*                          | 2020-09-23   .                                       |                                     */
    /*                          | 2020-09-26   .                                       |                                     */
    /*                          | 2020-09-29   .                                       |                                     */
    /*                          | 2020-10-01   3                                       |                                     */
    /*                          | 2020-10-02   .                                       |                                     */
    /*                          |                                                      |                                     */
    /*                          | Now all we have to do is sum the missings            |                                     */
    /*                          | and output when id is populated                      |                                     */
    /*                          |                                                      |                                     */
    /*                          | data want;                                           |                                     */
    /*                          |   set adverse_events(in=e)                           |                                     */
    /*                          |               visits(in=v);                          |                                     */
    /*                          |   by date;                                           |                                     */
    /*                          |   retain _v;                                         |                                     */
    /*                          |   if id then do;                                     |                                     */
    /*                          |     output;                                          |                                     */
    /*                          |     _v=id;                                           |                                     */
    /*                          |     n=0;                                             |                                     */
    /*                          |   end;                                               |                                     */
    /*                          |   else n+1;                                          |                                     */
    /*                          |   keep id date n;                                    |                                     */
    /*                          | run;                                                 |                                     */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_U

    */











