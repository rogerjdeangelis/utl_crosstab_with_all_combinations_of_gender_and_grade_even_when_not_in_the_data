# utl_crosstab_with_all_combinations_of_gender_and_grade_even_when_not_in_the_data.sas
Crosstab with all combinations of gender and grade even when not in the data.   Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics                   artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP                natural language processing machine learning.

    Crosstab with all combinations of gender and grade even when not in the data                                                        
                                                                                                                                        
    see github                                                                                                                          
    https://goo.gl/JUmLPV                                                                                                               
    https://github.com/rogerjdeangelis/utl_crosstab_with_all_combinations_of_gender_and_grade_even_when_not_in_the_data                 
                                                                                                                                        
                                                                                                                                        
    Original topic                                                                                                                      
    Count the instances between two dates with a criteria met                                                                           
                                                                                                                                        
                                                                                                                                        
                                                                                                                                        
     WORK.HAVE total obs=15      |                             RULES                                                                    
                                 |                             Frequencies                                                              
        DOV     SEX      GRADE   |                                                                                                      
                                 |                                                        NOT IN DATA                                   
        AUG    FEMALE      A     |        Female     Female   Female    Male       Male     Male                                        
        AUG    FEMALE      B     | Month  Grade=A    Grade=B  Grade=C   Grade=A    Grade=B  Grade=C                                     
        AUG    FEMALE      C     | AUG       1         1        2          1           1       0                                        
        AUG    FEMALE      C     |                                                                                                      
        AUG    MALE        A     |                                                                                                      
        AUG    MALE        B     |                                                                                                      
                                 |                                                                                                      
        SEP    FEMALE      A     |                                                                                                      
        SEP    MALE        A     |                                                                                                      
        SEP    MALE        B     |                                                                                                      
                                                                                                                                        
        ZZZ    FEMALE      A     |  I added this to get all combinations                                                                
        ZZZ    FEMALE      B     |                                                                                                      
        ZZZ    FEMALE      C     |                                                                                                      
        ZZZ    MALE        A     |                                                                                                      
        ZZZ    MALE        B     |                                                                                                      
        ZZZ    MALE        C     |                                                                                                      
                                                                                                                                        
                                                                                                                                        
    PROCESS                                                                                                                             
                                                                                                                                        
        ods exclude all;                                                                                                                
        ods output observed=want(rename=label=month where=(month not in ('Sum','ZZZ')));                                                
        proc corresp data=have dim=1 observed cross=both;                                                                               
        tables DOV, sex grade;                                                                                                          
        run;quit;                                                                                                                       
        ods select all;                                                                                                                 
                                                                                                                                        
                                                                                                                                        
                                                                                                                                        
    OUTPUT (slight manual cleaup)                                                                                                       
    =============================                                                                                                       
                                                                                                                                        
    Obs    MONTH    FEMALE_A     FEMALE_B     FEMALE_C       MALE__A    MALE_B     MALE_C    SUM                                        
                                                                                                                                        
     1      AUG         1            1            2           1           1           0         6                                       
     2      SEP         1            0            0           1           1           0         3                                       
                                                                                                                                        
    related to                                                                                                                          
    https://goo.gl/oqDu3U                                                                                                               
    https://communities.sas.com/t5/Base-SAS-Programming/Count-the-instances-between-two-dates-with-a-criteria-met/m-p/423361            
                                                                                                                                        
                                                                                                                                        
    *                _              _       _                                                                                           
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                                                    
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                                                   
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                                                   
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                                                   
                                                                                                                                        
    ;                                                                                                                                   
                                                                                                                                        
    data have;                                                                                                                          
       infile cards4 eof=dne;                                                                                                           
       input dov$ sex$ grade$;                                                                                                          
       output;                                                                                                                          
       return;                                                                                                                          
       dne:                                                                                                                             
        do sex="FEMALE","MALE";                                                                                                         
          do grade="A","B","C";                                                                                                         
             dov='ZZZ';                                                                                                                 
             output;                                                                                                                    
          end;                                                                                                                          
        end;                                                                                                                            
    CARDS4;                                                                                                                             
    AUG FEMALE A                                                                                                                        
    AUG FEMALE B                                                                                                                        
    AUG FEMALE C                                                                                                                        
    AUG FEMALE C                                                                                                                        
    AUG MALE A                                                                                                                          
    AUG MALE B                                                                                                                          
    SEP FEMALE A                                                                                                                        
    SEP MALE A                                                                                                                          
    SEP MALE B                                                                                                                          
    ;;;;                                                                                                                                
    RUN;QUIT;                                                                                                                           
                                                                                                                                        
    *          _       _   _                                                                                                            
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                                 
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                               
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                               
                                                                                                                                        
    ;                                                                                                                                   
                                                                                                                                        
    ods exclude all;                                                                                                                    
    ods output observed=want                                                                                                            
      (rename=label=month where=(month not in ('Sum','ZZZ')));;                                                                         
    proc corresp data=have dim=1 observed cross=both;                                                                                   
    tables DOV, sex grade;                                                                                                              
    run;quit;                                                                                                                           
    ods select all;                                                                                                                     
                                                                                                                                        
    proc print data=want(obs=2) width=min;                                                                                              
    run;quit;                                                                                                                           
                                                                                                                                        
                                                                                                                                        
             FEMALE___    FEMALE___    FEMALE___                                                                                        
    MONTH        A            B            C        MALE___A    MALE___B    MALE___C    SUM                                             
                                                                                                                                        
     AUG         1            1            2           1           1           0         6                                              
     SEP         1            0            0           1           1           0         3                                              
                                                                                                                                        
                                                                                                                                        
                                   

