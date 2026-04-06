# 📘Order Management

Mostrar o procedimento O aplicativo de Gerenciamento de Pedidos é um componente chave do Infor ERP LX.

1. Ele é utilizado para inserir e manter vários tipos de pedidos (incluindo cotações e autorizações de devolução de material - RMAs), reconhecer e alocar estoque e imprimir documentos comerciais padrão
2. O gerenciamento no ORD engloba funções como verificação de disponibilidade de inventário, checagem de crédito de clientes, manutenção de preços especiais, faturamento de remessas diretas (drop shipments) e consolidação de pedidos online
3. Além disso, o aplicativo possui integração estreita com módulos de Contas a Receber, Inventário, Faturamento e Promoções e Acordos

Principais arquivos mestres e de transação, destacando-se:

. ECH (Customer Order Header): Arquivo de cabeçalho do pedido do cliente
. ECL (Customer Order Line Items): Arquivo de detalhes e itens de linha do pedido do cliente
. RCM (Customer Master file): Arquivo Mestre de Clientes
. EOC (Customer Order Class): Arquivo de Classe de Pedido do Cliente
. EOT (Customer Order Type): Arquivo de Tipo de Pedido do Cliente

Programas:
. ORD700D1 / ORD700 (Order Entry): Utilizado como o ponto de entrada principal para criar e manter pedidos de clientes, cotações e RMAs a partir de uma única função
. ORD300D / ORD300D1 (Order Inquiry): Permite consultar e visualizar pedidos em aberto por cliente, pedido de compra do cliente, vendedor, armazém, item ou data de solicitação
. ORD550D (Pick Release): Permite liberar pedidos em aberto, alocar o inventário e imprimir documentos de separação (picking)
. ORD570D1 (Pick Confirm): Utilizado para confirmar a quantidade atual, lote e localização do inventário que foi efetivamente separado/expedido
. ORD720D1 (On-line Allocation): Permite verificar detalhes do inventário e realizar manutenções de alocação de estoque para as linhas de um pedido de cliente de forma online


