<summary>✍️<B>Lista de Todos os Phisical Files</B> SQL400 </summary>
<br><p>SQL/400</p>
  
```csharp
  SELECT SUBSTR(TABLE_NAME, 1, 20) TABLE_NAME                    
       , SUBSTR(TABLE_TEXT, 1, 30) TABLE_TEXT                    
       , SUBSTR(TABLE_TYPE, 1, 1)  TABLE_TYPE                    
       , TABLE_SCHEMA                                            
  FROM QSYS2.SYSTABLES                                           
  WHERE TABLE_TYPE  = 'P'                                        
  AND   TABLE_SCHEMA NOT LIKE 'QRY%'                             
  AND   TABLE_SCHEMA NOT LIKE '%SQLPRO50%'                       
  AND   TABLE_SCHEMA NOT LIKE '%ANTONIO%'                        
  AND   TABLE_SCHEMA NOT LIKE '%BACK%'                           
  AND   TABLE_SCHEMA NOT LIKE '%DBU11%'                          
  AND   TABLE_SCHEMA NOT LIKE '#%'                               
  AND   TABLE_TEXT   NOT LIKE '%SKMR%'                           
  AND   TABLE_TEXT   NOT LIKE '%Prev.cliente na data%'           
  AND   TABLE_TEXT   NOT LIKE '%B. Dados Rastr.%'                
  ORDER BY TABLE_SCHEMA, TABLE_NAME                              
```
Com base na Library List

```csharp

SELECT SUBSTR(TABLE_NAME, 1, 20) TABLE_NAME                         
     , CAST(TABLE_TEXT   AS CHAR(50) CCSID 37) TABLE_TEXT           
     , CAST(TABLE_TYPE   AS CHAR(1) CCSID 37)  TABLE_TYPE           
     , CAST(TABLE_SCHEMA AS CHAR(50) CCSID 37)  TABLE_SCHEMA        
FROM   QSYS2.SYSTABLES                                              
WHERE  TABLE_TYPE  = 'P'                                            
AND    TABLE_SCHEMA IN(                                             
       'ERPLXUSRF', 'ERPLXPOR', 'ERPLXEC', 'ASBGLXOHOM',            
       'ASBGLXF', 'ASBGLXO',  'SSABLXF', 'SSABLXSF',                
       'V834WBPKO', 'SSABLXPTF', 'SSABLXSO', 'SSABLXO',             
       'X83ALL', 'ERP8305PTG', 'ERPLXPTF', 'ERPLXO',                
       'ERPLXPAPTF', 'ERPLXPARF', 'ERPLXPARO', 'ERPLXF',            
       'SSAGTLIC83', 'QGPL', 'QTEMP')                               
ORDER BY TABLE_SCHEMA, TABLE_NAME  ) with data                                                   

```

Estrutura das tabelas com base na Library List

```csharp
SELECT DISTINCT                                                  
       CAST(A.TABLE_NAME AS CHAR(20) CCSID 37) TABLE_NAME,       
       CAST(A.TABLE_SCHEMA AS CHAR(15) CCSID 37) TABLE_SCHEMA,   
       CAST(B.TABLE_TEXT AS CHAR(50) CCSID 37) TABLE_TEXTA,      
       CAST(A.COLUMN_NAME AS CHAR(15) CCSID 37) COLUMN_NAME,     
       CAST(A.DATA_TYPE AS CHAR(15) CCSID 37) DATA_TYPE,         
       LENGTH,                                                      
       NUMERIC_SCALE,                                               
       CAST(COLUMN_TEXT AS CHAR(100) CCSID 37) COLUMN_TEXT,         
       CAST(ORDINAL_POSITION AS DEC(15)) ORDINAL_POSITION           
FROM   QSYS2.SYSCOLUMNS A                                          
       LEFT JOIN MSIKAMA/PF_PROD B ON(A.TABLE_NAME = B.TABLE_NAME) 
WHERE  A.TABLE_SCHEMA IN(                                        
       'ERPLXUSRF', 'ERPLXPOR', 'ERPLXEC', 'ASBGLXOHOM',         
       'ASBGLXF', 'ASBGLXO',  'SSABLXF', 'SSABLXSF',             
       'V834WBPKO', 'SSABLXPTF', 'SSABLXSO', 'SSABLXO',          
       'X83ALL', 'ERP8305PTG', 'ERPLXPTF', 'ERPLXO',             
       'ERPLXPAPTF', 'ERPLXPARF', 'ERPLXPARO', 'ERPLXF',   
       'SSAGTLIC83', 'QGPL', 'QTEMP')    
```
