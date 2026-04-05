<details>
<summary>✍️<B>Tabelas</B></summary>

Lista de Programas 
```csharp
   SELECT * FROM BAT
   SELECT * FROM DSP  
```

Lock do programa *D
```csharp
   SELECT *
   FROM  dsp
   WHERE DSLCK = 'Y'
   and   DSNAME like 'OFEB53O%' 

```

Action
```csharp
SELECT ACETYP,                            
       ACNAME,                            
       ACSCNM,                            
       ACGRID,                            
       ACNO,                              
       ACTGTY,                            
       ACTAR,                             
       ACTXT                              
FROM   ACTL02                             
WHERE ACNAME = 'OFEB53O'                  
AND   ACTGTY <> ';'                       
AND ( ACTAR LIKE '%RINHPO%' OR            
      ACTXT LIKE '%RINHPO%')              
ORDER BY ACSCNM, ACGRID, ACNO    
```

Fild Definition
```csharp
SELECT *
FROM DFDL01          
WHERE DDNAME = 'OFEB53O'      
AND   DDFILD LIKE '%X3NROC%'   
```

Data Model usado por Tela
```csharp
SELECT * 
FROM   DSAL01 
WHERE  DNNAME = 'OFEB53O'  
```

Posição do Campo na Tela
```csharp
SELECT   DANAME                         
     ,   DASCNM                         
     ,   DAFILD                         
     ,   DAROW                          
     ,   DACOL                          
FROM     DFA                            
WHERE    DANAME = 'OFEB53O'             
AND      DAFILD NOT LIKE '%*%'          
AND      DASCNM LIKE '%%'               
ORDER BY DANAME, DASCNM, DAROW, DACOL   
```

Data Area Definition
```csharp
SELECT * 
FROM   UDEL01 
WHERE UENAME = 'OFEB53O'   
```

Data Area Definition
```csharp
SELECT *
FROM   PUL
WHERE  PUNAME = 'FER03B' 
```

BachPrograma - Parametros
```csharp

SELECT *
FROM PRML02
WHERE PRNAME = 'FAC19B'

```



</details>
