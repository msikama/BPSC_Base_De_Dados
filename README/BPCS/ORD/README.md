# 📘Order Management

<details>
<summary>🎖️Definição</summary>

Mostrar o procedimento O aplicativo de Gerenciamento de Pedidos é um componente chave do Infor ERP LX.

1.  Ele é utilizado para inserir e manter vários tipos de pedidos (incluindo cotações e autorizações de devolução de material - RMAs), reconhecer e alocar estoque e imprimir documentos comerciais padrão
2.  O gerenciamento no ORD engloba funções como verificação de disponibilidade de inventário, checagem de crédito de clientes, manutenção de preços especiais, faturamento de remessas diretas (drop shipments) e consolidação de pedidos online
3.  Além disso, o aplicativo possui integração estreita com módulos de Contas a Receber, Inventário, Faturamento e Promoções e Acordos

Principais arquivos mestres e de transação, destacando-se:

-  ECH (Customer Order Header): Arquivo de cabeçalho do pedido do cliente
-  ECL (Customer Order Line Items): Arquivo de detalhes e itens de linha do pedido do cliente
-  RCM (Customer Master file): Arquivo Mestre de Clientes
-  EOC (Customer Order Class): Arquivo de Classe de Pedido do Cliente
-  EOT (Customer Order Type): Arquivo de Tipo de Pedido do Cliente

Programas:

- ORD700D1 / ORD700 (Order Entry): Utilizado como o ponto de entrada principal para criar e manter pedidos de clientes, cotações e RMAs a partir de uma única função
- ORD300D / ORD300D1 (Order Inquiry): Permite consultar e visualizar pedidos em aberto por cliente, pedido de compra do cliente, vendedor, armazém, item ou data de solicitação
- ORD550D (Pick Release): Permite liberar pedidos em aberto, alocar o inventário e imprimir documentos de separação (picking)
- ORD570D1 (Pick Confirm): Utilizado para confirmar a quantidade atual, lote e localização do inventário que foi efetivamente separado/expedido
- ORD720D1 (On-line Allocation): Permite verificar detalhes do inventário e realizar manutenções de alocação de estoque para as linhas de um pedido de cliente de forma online

</details>

<details>
<summary>✍️<B>Consulta Pedido</B></summary>

Consulta Ordem: MENU: ORD / ORD300D1 / Linhas [F14]  

HEADER  
```csharp

SELECT HID
     , HORD
	 , HEDTE
	 , HCUST
	 , HSTAT 
FROM   ECH 
WHERE HORD = 296162    

```

Detalhe
```csharp

SELECT *
FROM   ECL
WHERE LORD = 296162   

```
</details>


<details>
	
<summary>✍️<B>ERRO DE ALOCAÇÃO</B> Alocações fantasmas: Aloc Clnt</summary>
<br>
<br>
Existir Aloc Clnt na tela INV300D, mas não existir o registro no ELA.
Como posso fazer uma atulização pontual para resolver este caso?

Este é um caso clássico de "alocação fantasma" (ghost allocation). Isso geralmente ocorre por falhas de atualização ou quedas do sistema, onde o arquivo de detalhe perdeu a informação, mas os arquivos de saldo mantiveram o valor acumulado.
Como o registro não existe na tabela de detalhes ELA (Allocation to Orders), você não conseguirá resolver o problema pelas telas operacionais padrão (como o programa de alocação online ORD720 ou ORD725D), pois a linha da alocação não aparecerá na tela para que você possa usar a ação 4=Delete.

- Para realizar uma atualização pontual e resolver essa divergência sem precisar rodar o recálculo geral do sistema, a equipe de TI precisará fazer um ajuste direto via banco de dados (usando SQL ou utilitários como o DFU).

- A TI deverá subtrair a quantidade "fantasma" diretamente nos campos de totalização das tabelas de saldo:
Tabela IIM (Item Master): Atualizar o campo ICUSA (que guarda o total de alocações de cliente a nível macro).

- Tabela IWI (Warehouse Inventory): Atualizar o campo WCUSA (que guarda o total alocado do item dentro daquele armazém).

- Tabelas ILI e ILN: Atualizar o campo de quantidade alocada no endereço físico (ILI) e, se o item for controlado por lote, no mestre de lotes (ILN) para manter a integridade.

A Solução Oficial do Sistema Se a atualização direta via banco de dados não for recomendada ou permitida pela política da sua empresa, a única forma sistêmica de limpar essa alocação fantasma é, de fato, utilizando o programa INV971 (Reset on-order and allocated amounts).

O INV971 ignora o que está na tela e reseta os campos de saldo (IONOD, IPRDA e ICUSA no arquivo IIM, e WCUSA no arquivo IWI), recalculando-os do zero com base no que realmente existe nas tabelas de detalhes (linhas de pedidos ECL, ordens de fabricação FSO e FMA, e pedidos de compra HPO).

Lembre-se, porém, das restrições para rodar este programa, como a necessidade de tratar previamente as ordens de devolução (post-ship orders) para não perder a visibilidade do estoque.

</details>
