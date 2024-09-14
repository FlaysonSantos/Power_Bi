# Modelando um Dashboard de E-commerce com Power BI - [Flayson Santos](https://github.com/FlaysonSantos/)
# Modelo de Dados - Análise de Vendas

Este documento descreve o modelo de dados utilizado para análise de vendas, produtos, descontos e métricas financeiras. O modelo é composto por uma tabela central de fatos, **F_Vendas**, e várias tabelas dimensionais que permitem uma análise detalhada e agregada dos dados.

## Tabela Central

**A F_Vendas** é a nossa tabela de fatos, que contém os dados principais das transações realizadas. Ela armazena informações cruciais, como o total de vendas, o país em que ocorreram, a data, o produto vendido, o lucro e o preço de venda. Essa tabela é a base sobre a qual todas as outras estão conectadas, servindo como ponto central para as análises que realizamos.

## Tabelas de Detalhamento

- **D_Produtos_Detalhes**: Esta tabela adiciona camadas importantes de informações sobre os produtos vendidos, como faixa de desconto aplicada, preço de fabricação, preço de venda e número de unidades vendidas. Permite detalhar as vendas ao nível de produto e compreender o impacto dos descontos e preços sobre os resultados.

- **D_Descontos**: Conectada à **F_Vendas** através do `ID_Produto`, esta tabela fornece detalhes sobre as faixas de desconto, permitindo uma visão clara de como os descontos impactam as vendas e o lucro.

## Análise de Produtos

- **D_Produtos**: Fornece uma visão consolidada dos produtos com dados como a média de valor de venda, valor máximo e mínimo, entre outros dados agregados. Ideal para comparações entre produtos e avaliação de desempenho em termos de vendas e receita.

## Detalhes Financeiros

- **D_Detalhes**: Oferece uma análise aprofundada das vendas, com métricas financeiras como Custo das Mercadorias Vendidas (COGS), lucro, unidades vendidas e desempenho por segmento e país. Tabela essencial para análises financeiras robustas.

- **financials_origem**: Fornece uma visão financeira abrangente com dados como vendas brutas, custos de fabricação e outros elementos que ajudam a avaliar a rentabilidade geral.

## Conclusão

Este modelo de dados foi projetado para fornecer uma visão abrangente e detalhada das vendas. A partir dele, é possível correlacionar variáveis como descontos, custos de fabricação e desempenho de produtos para gerar insights estratégicos e tomar decisões mais informadas. Ao conectar todas essas tabelas, obtemos uma análise poderosa e completa sobre o desempenho de vendas e produtos.

---

## Descrição das Tabelas

### 1. **F_Vendas (Tabela de Fatos)**
   - **Função**: Armazena os dados principais das transações de vendas.
   - **Campos**:
     - `Sales`: Total de vendas realizadas.
     - `Country`: País onde a venda ocorreu.
     - `Date`: Data da transação.
     - `Discount Band`: Faixa de desconto aplicada.
     - `ID_Produto`: Identificador do produto vendido.
     - `Month Name`: Nome do mês em que a venda foi realizada.
     - `Product`: Nome do produto.
     - `Profit`: Lucro obtido com a venda.
     - `Sale Price`: Preço de venda do produto.

### 2. **D_Produtos_Detalhes (Tabela Dimensional)**
   - **Função**: Fornece detalhes sobre os produtos vendidos.
   - **Campos**:
     - `Discount Band`: Faixa de desconto disponível.
     - `Índice`: Identificador do produto.
     - `Manufacturing Price`: Preço de fabricação do produto.
     - `Sale Price`: Preço de venda.
     - `Units Sold`: Quantidade de unidades vendidas.

### 3. **D_Descontos (Tabela Dimensional)**
   - **Função**: Contém informações sobre os descontos aplicados.
   - **Campos**:
     - `Discount Band`: Faixa de desconto aplicada.
     - `Discounts`: Valor do desconto.
     - `ID_produto`: Identificador do produto relacionado.

### 4. **D_Produtos (Tabela Dimensional)**
   - **Função**: Fornece dados agregados sobre produtos e suas vendas.
   - **Campos**:
     - `Contagem`: Número total de produtos.
     - `Índice`: Identificador do produto.
     - `Média da manufatura`: Preço médio de fabricação.
     - `Média do valor de vendas`: Preço médio de venda.
     - `Mediana do valor de vendas`: Mediana dos valores de venda.
     - `Product`: Nome do produto.
     - `Valor máximo de venda`: Maior valor de venda registrado.
     - `Valor mínimo de venda`: Menor valor de venda registrado.

### 5. **D_Detalhes (Tabela Dimensional)**
   - **Função**: Fornece detalhes adicionais sobre vendas e métricas financeiras.
   - **Campos**:
     - `Sales`: Total de vendas.
     - `COGS (Cost of Goods Sold)`: Custo das mercadorias vendidas.
     - `Country`: País onde a venda ocorreu.
     - `Data`: Data da venda.
     - `Discount Band`: Faixa de desconto aplicada.
     - `Discounts`: Valor dos descontos aplicados.
     - `Gross Sales`: Vendas brutas.
     - `Manufacturing Price`: Preço de fabricação.
     - `Month Name`: Nome do mês em que a venda foi realizada.
     - `Month Number`: Número do mês (1-12).
     - `Product`: Nome do produto vendido.
     - `Profit`: Lucro obtido.
     - `Sale Price`: Preço de venda.
     - `Segment`: Segmento de mercado.
     - `Units Sold`: Unidades vendidas.
     - `Year`: Ano da venda.

### 6. **financials_origem (Tabela Dimensional)**
   - **Função**: Apresenta informações financeiras relacionadas às vendas.
   - **Campos**:
     - `Sales`: Total de vendas.
     - `COGS (Cost of Goods Sold)`: Custo das mercadorias vendidas.
     - `Country`: País onde a venda ocorreu.
     - `Date`: Data da transação.
     - `Discount Band`: Faixa de desconto.
     - `Discounts`: Valor dos descontos.
     - `Gross Sales`: Vendas brutas.
     - `Manufacturing Price`: Preço de fabricação.
     - `Month Name`: Nome do mês da venda.

Essas tabelas funcionam em conjunto para fornecer uma visão abrangente de vendas, produtos, descontos e métricas financeiras.

