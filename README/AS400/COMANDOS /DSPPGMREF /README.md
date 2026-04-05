✍️<B>Copy sources</B>

<br><p>Copiar o programa para ver os arquivos/programas usados</p>

DSPPGMREF PGM(SFCT06*) OUTPUT(*OUTFILE) OUTFILE(MSIKAMA/MS_PGMREF) 
 
```csharp

SELECT DISTINCT                                             
       WHPNAM, WHLIB, WHTEXT                                               
     , WHFNAM, WHLNAM, TABLE_TEXT                                           
     , WHOBJT                                               
FROM   MSIKAMA/MS_PGMREF                                    
       INNER JOIN MSIKAMA/PF_PROD                           
         ON(TABLE_NAME = SUBSTR(WHFNAM,1,3))                
WHERE  WHOBJT IN('F', 'L')                                  
AND    WHFNAM NOT LIKE 'ZPA%' AND WHFNAM NOT LIKE 'ZXU%'                               
AND    WHFNAM NOT LIKE 'ZMA%' AND WHFNAM NOT LIKE 'ZXO%'   
AND    WHFNAM NOT LIKE 'ZMM%' AND WHFNAM NOT LIKE 'ZMO%' 
AND    WHFNAM NOT LIKE 'ZMAVA2%' AND WHFNAM NOT LIKE 'Z_ZX8L02%'                               
ORDER BY WHFNAM  

```



[🔙](../../../../README.md)
