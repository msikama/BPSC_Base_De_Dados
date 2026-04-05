# 📘AS400                                                      

## 🛠️Comando

<details>
<summary>✍️<B>MENU</B> strsda </summary>
<br><p>STRSDA</p>
  
```csharp

                            Screen Design Aid (SDA)   
                                                      
 Select one of the following:                         
                                                      
      1. Design screens                               
      2. Design menus                                 
      3. Test display files                           
                                                     
                                                                                
 Selection or command                                                           
 ===>                                                                           
```
```csharp
                                 Design Menus
                                                                    
 Type choices, press Enter.                                         
                                                                    
   Source file . . . . . . . .   QDDSSRC      Name, F4 for list     
                                                                    
     Library . . . . . . . . .   ASBGLXMNU    Name, *LIBL, *CURLIB  
                                                                    
   Menu  . . . . . . . . . . .   MNUFLAP      Name, F4 for list     
                                                                    
                                                                           
```

</details>


<details>
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
</details>


<details>
<summary>✍️<B>Copy sources</B></summary>
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

</details>

## 🛠️RPGLE-400

<details>
<summary>✍️<B>Compilação</B> erro de ovr</summary>
<br><p>Qualquer Mensagem</p>

Exemplo do Bento para compilar o RPGLE, criou um CLP:
  
```csharp

        *************** Beginning of data ************************************************************
0011.00              PGM                                                                     230906   
0012.00                                                                                      210914   
0053.00              OVRDBF     FILE(EAIL02X) TOFILE(*LIBL/EAIL02) SHARE(*NO)                230906   
0055.00              OVRDBF     FILE(OFEUPD2X) TOFILE(*LIBL/OFEUPD2) SHARE(*NO)              230906   
0057.00              OVRDBF     FILE(OFEUPH2X) TOFILE(*LIBL/OFEUPH2) SHARE(*NO)              230906   
0059.00                                                                                      210914   
0063.00              RPGLE      PGM(MJE01BR) OBJLIBR(QTEMP) MODLIB(QTEMP) +                  230906   
0063.01                           SRCLIBR(ASBGLXS) BORI(I)                                   230906   
0081.00                                                                                      210914   
0082.00              ENDPGM                                                                  210914   
        ****************** End of data ***************************************************************

```
</details>


[🔙](../../../README.md)
