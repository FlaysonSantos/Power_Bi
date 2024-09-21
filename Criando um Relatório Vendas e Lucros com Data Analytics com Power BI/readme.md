## Relatório de vendas
Acesse a pasta [Dados](https://github.com/FlaysonSantos/Power_Bi/tree/main/Criando%20um%20Relat%C3%B3rio%20Vendas%20e%20Lucros%20com%20Data%20Analytics%20com%20Power%20BI/Dados) para utilizar o projeto "sales_report_desafio_projeto.pbix" ou vizualizar em pdf "sales_report_desafio_projeto.pdf"
 Gerado no Power BI, com gráficos que mostram dados como:

-   **Vendas por país** (Estados Unidos, Canadá, França, Alemanha, México)
-   **Produtos TOP 3** por vendas (Paseo, VTT, Velo)
-   **Vendas e unidades vendidas por mês**
-   **Lucro e vendas por mês**
-   **Segmentos de clientes** (Governo, Pequenas Empresas, Empresas, Midmarket, Parceiros de Canal)

Essas visualizações ajudam a entender a distribuição das vendas por regiões, períodos e segmentos, além de dar uma visão dos produtos mais vendidos.

## Dados de vendas:

Nosso dados detalhados de vendas, contem as seguintes colunas principais:

-   **Segmento**: (ex.: Governo, Midmarket)
-   **País**: (ex.: Canadá, Alemanha)
-   **Produto**: (ex.: Carretera)
-   **Unidades Vendidas**: Quantidade de unidades vendidas
-   **Preço de Venda**, **Preço de Fabricação**, **Vendas Brutas**, **Descontos**, **Vendas** (descontos aplicados)
-   **COGS** (Custo das Mercadorias Vendidas) e **Lucro**
-   **Data** e informações de Mês e Ano.

## Funçoes DAX  usadas no projeto:

### Descomplicando a Fórmula `AVERAGEX`

> avg sales = AVERAGEX(financials, financials[Sales])

A fórmula `avg sales = AVERAGEX(financials, financials[Sales])` é usada para calcular a **média das vendas** a partir de uma tabela chamada `financials` no Power BI. Vamos quebrar essa fórmula em partes para entender melhor:

-   **`AVERAGEX`**: Essa função é específica do DAX (Data Analysis Expressions) e serve para calcular a média de uma expressão ao longo de uma tabela.
-   **`financials`**: Representa o nome da tabela que contém os dados das vendas.
-   **`financials[Sales]`**: Indica a coluna "Sales" (Vendas) dentro da tabela `financials`. É nessa coluna que os valores das vendas estão armazenados.

### Como a Fórmula Funciona no Power BI

1.  **Itera por cada linha:** A função `AVERAGEX` percorre cada linha da tabela `financials`.
2.  **Obtém o valor da venda:** Para cada linha, ela pega o valor correspondente na coluna "Sales".
3.  **Calcula a média:** Após percorrer todas as linhas, a função calcula a média de todos os valores de vendas que foram coletados.
4.  **Armazena o resultado:** O resultado final, que é a média das vendas, é armazenado na medida `avg sales`.




## Entendendo a Função `MAX` no DAX

> Máximo sold = MAX(financials[Units Sold])

**A fórmula `Máximo sold = MAX(financials[Units Sold])` é utilizada para encontrar a maior quantidade de unidades vendidas em uma tabela chamada `financials`.**

### Descomplicando a Fórmula

-   **`MAX`**: Essa função tem a finalidade de identificar o maior valor dentro de um conjunto de dados.
-   **`financials[Units Sold]`**: Indica a coluna "Units Sold" (Unidades Vendidas) dentro da tabela `financials`. É nessa coluna que estão armazenados os números de unidades vendidas.

### Como a Fórmula Funciona

1.  **Itera por cada linha:** A função `MAX` percorre linha por linha da coluna "Units Sold".
2.  **Compara os valores:** A cada linha, o valor atual é comparado com o maior valor encontrado até aquele momento.
3.  **Armazena o maior valor:** Se o valor atual for maior, ele se torna o novo valor máximo.
4.  **Retorna o resultado:** Ao final, a função retorna o maior valor encontrado em toda a coluna.


## Analisando a Medida `OUTLIER`

> > outlier =  CALCULATE(
> 
> >[total de vendidos],
> 
> >FILTER(
> 
> >VALUES(financials[Product]),
> 
> >COUNTROWS( FILTER(financials, [total de vendidos] >= 150)) >> 0
> 
> >)
> 
> >)

**A medida `OUTLIER` que você apresentou é uma forma inteligente de identificar produtos que se destacam por um alto volume de vendas em relação a outros produtos.**

### Desvendando a Fórmula

Vamos quebrar a fórmula em partes para entender melhor cada etapa:

-   **`CALCULATE([total de vendidos])`:**
    
    -   **Objetivo:** Calcular o total de vendas, mas com um contexto modificado.
    -   **Contexto:** O contexto será modificado pelo filtro aplicado a seguir.
-   **`FILTER(VALUES(financials[Product]), COUNTROWS( FILTER(financials, [total de vendidos] >= 150)) > 0)`:**
    
    -   **Criando um filtro:** Essa parte complexa cria um filtro para os produtos.
    -   **`VALUES(financials[Product])`:** Cria uma lista de todos os produtos únicos na tabela `financials`.
    -   **`COUNTROWS( FILTER(financials, [total de vendidos] >= 150)) > 0`:** Conta quantas linhas na tabela `financials` têm um valor de `total de vendidos` maior ou igual a 150. Se esse número for maior que zero, significa que existem produtos que ultrapassaram esse limite e são considerados outliers.

### Como a Fórmula Funciona na Prática

1.  **Identifica os outliers:** A fórmula filtra a lista de produtos, selecionando apenas aqueles que possuem um volume de vendas igual ou superior a 150 unidades.
2.  **Calcula o total:** Para os produtos filtrados (outliers), a função `CALCULATE` calcula o total de vendas.
3.  **Retorna o resultado:** O resultado final é o total de vendas de todos os produtos considerados outliers.

### Em outras palavras:

A medida `OUTLIER` responde à pergunta: "Qual é o total de vendas dos produtos que venderam mais do que 150 unidades?".

**É importante notar:**

-   **Limiar de 150:** O valor 150 é um limiar arbitrário para definir o que é um outlier. Você pode ajustar esse valor de acordo com a sua análise e os seus dados.
-   **Contexto:** A medida `OUTLIER` é sensível ao contexto. Se você aplicar filtros adicionais ao seu relatório, o resultado da medida será recalculado com base nesses filtros.

### Personalizando a Medida

Você pode personalizar essa medida de diversas maneiras:

-   **Alterar o limiar:** Ajuste o valor 150 para um valor que melhor represente o seu conceito de outlier.
-   **Adicionar mais condições:** Combine com outras funções DAX para criar filtros mais complexos, como outliers por categoria de produto ou por região.
-   **Criar medidas adicionais:** Calcular a quantidade de outliers, a média de vendas dos outliers, etc.

**Em resumo,** a medida `OUTLIER` é uma ferramenta poderosa para identificar produtos que se destacam em termos de vendas e podem exigir uma análise mais aprofundada.



## Entendendo a Medida `TOP3 PRODUCT`

> TOP3 PRODUCT =  CALCULATE(
> 
> [total sales],
> 
> TOPN(
> 
> 3,
> 
> ALL(financials[Product]),
> 
> [total sales]),
> 
> VALUES(financials[Product])
> 
> )

**A medida `TOP3 PRODUCT` tem como objetivo calcular o total de vendas dos 3 produtos que mais venderam.**

### Descomplicando a Fórmula

Vamos analisar a fórmula passo a passo:

-   **`CALCULATE([total sales])`:**
    
    -   **Objetivo:** Calcular o total de vendas, mas em um contexto específico.
    -   **Contexto:** O contexto será definido pelo filtro aplicado a seguir.
-   **`TOPN(3, ALL(financials[Product]), [total sales])`:**
    
    -   **Selecionando os top 3:** Essa parte da fórmula filtra a tabela `financials` para incluir apenas os 3 produtos com as maiores vendas.
    -   `TOPN(3)`: Indica que queremos os 3 primeiros registros.
    -   `ALL(financials[Product])`: Remove qualquer filtro pré-existente na coluna "Produto", garantindo que todos os produtos sejam considerados.
    -   `[total sales]`: Ordena os produtos com base no total de vendas, do maior para o menor.
-   **`VALUES(financials[Product])`:**
    
    -   **Lista de produtos:** Retorna uma lista com os nomes únicos dos produtos da tabela filtrada.

### Como a Fórmula Funciona na Prática

1.  **Considera todos os produtos:** A função `ALL` garante que todos os produtos sejam avaliados, independentemente de outros filtros aplicados no relatório.
2.  **Ordena por vendas:** Os produtos são ordenados de acordo com o total de vendas, do mais vendido para o menos vendido.
3.  **Seleciona os 3 primeiros:** A função `TOPN` seleciona apenas os 3 primeiros produtos da lista ordenada.
4.  **Calcula o total de vendas:** Para cada um dos 3 produtos selecionados, o `CALCULATE` calcula o total de vendas.


## Analisando a Medida `TOP3 PRODUCT total para Country`

> TOP3 PRODUCT total para Country =
> 
> CALCULATE([TOP3 PRODUCT], ALLSELECTED('financials'[Country]))

**A medida `TOP3 PRODUCT total para Country` é uma ferramenta poderosa para entender o desempenho dos produtos em diferentes países.**

### Quebrando a Fórmula

Vamos dissecar a fórmula para entender melhor o que cada parte faz:

-   **`CALCULATE([TOP3 PRODUCT])`:**
    
    -   **Objetivo:** Calcular o total de vendas dos 3 produtos mais vendidos, mas com um contexto modificado.
    -   **Contexto:** O contexto será definido pelo filtro aplicado a seguir.
-   **`ALLSELECTED('financials'[Country])`:**
    
    -   **Removendo filtros de país:** Essa parte remove qualquer filtro aplicado à coluna "País", garantindo que o cálculo seja feito para cada país individualmente.

### Como a Fórmula Funciona na Prática

1.  **Considera cada país:** A função `ALLSELECTED` garante que o cálculo seja feito para cada país presente na sua tabela de dados.
2.  **Identifica os top 3:** Para cada país, a medida `[TOP3 PRODUCT]` (que você definiu anteriormente) é utilizada para identificar os 3 produtos mais vendidos.
3.  **Soma as vendas:** O total de vendas dos 3 produtos mais vendidos de cada país é calculado e apresentado na medida.

### Em outras palavras:

A medida `TOP3 PRODUCT total para Country` responde à pergunta: "Quais são os 3 produtos que mais venderam em cada país e qual foi o total de vendas desses produtos em cada país?".

**Por que essa medida é útil?**

-   **Análise regional:** Permite comparar o desempenho dos produtos em diferentes países.
-   **Identificação de oportunidades:** Ajuda a identificar países com potencial de crescimento para determinados produtos.
-   **Tomada de decisão:** Pode ser utilizada para definir estratégias de marketing e vendas específicas para cada país.

## Análise da Fórmula DAX: `

> total de vendidos = SUMX(financials, financials[Units Sold])`

### Quebrando a Fórmula:

-   **`total de vendidos`:** Este é o nome da medida que estamos criando. É aqui que o resultado final do cálculo será armazenado.
-   **`= SUMX`:** A função `SUMX` é uma das mais poderosas do DAX. Ela serve para iterar sobre cada linha de uma tabela e aplicar uma expressão a cada linha, no final, somando todos os resultados.
-   **`financials`:** Esta é a tabela sobre a qual vamos iterar. Em outras palavras, a função `SUMX` vai "percorrer" cada linha da tabela `financials`.
-   **`financials[Units Sold]`:** Esta parte se refere à coluna específica da tabela `financials` que queremos somar. Neste caso, estamos somando os valores da coluna "Units Sold" (Unidades Vendidas).

### O que a Fórmula Faz?

Em resumo, esta fórmula calcula o **total de unidades vendidas** presentes na tabela `financials`. Ela funciona da seguinte maneira:

1.  **Iteração:** A função `SUMX` começa na primeira linha da tabela `financials`.
2.  **Cálculo:** Para cada linha, ela pega o valor da coluna "Units Sold" daquela linha.
3.  **Soma:** Todos os valores obtidos em cada linha são somados.
4.  **Resultado:** O resultado final, que é a soma de todas as unidades vendidas, é armazenado na medida `total de vendidos`

## Analisando a Fórmula DAX: 

> total sales = SUMX(financials, financials[Sales])

### Quebrando a Fórmula:

-   **`total sales`:** Este é o nome da medida que estamos criando. É aqui que o resultado final do cálculo será armazenado.
-   **`= SUMX`:** A função `SUMX` é uma das mais poderosas do DAX. Ela serve para iterar sobre cada linha de uma tabela e aplicar uma expressão a cada linha, no final, somando todos os resultados.
-   **`financials`:** Esta é a tabela sobre a qual vamos iterar. Em outras palavras, a função `SUMX` vai "percorrer" cada linha da tabela `financials`.
-   **`financials[Sales]`:** Esta parte se refere à coluna específica da tabela `financials` que queremos somar. Neste caso, estamos somando os valores da coluna "Sales" (Vendas).

### O que a Fórmula Faz?

Em resumo, esta fórmula calcula o **total de vendas** presentes na tabela `financials`. Ela funciona da seguinte maneira:

1.  **Iteração:** A função `SUMX` começa na primeira linha da tabela `financials`.
2.  **Cálculo:** Para cada linha, ela pega o valor da coluna "Sales" daquela linha.
3.  **Soma:** Todos os valores obtidos em cada linha são somados.
4.  **Resultado:** O resultado final, que é a soma de todas as vendas, é armazenado na medida `total sales`.
