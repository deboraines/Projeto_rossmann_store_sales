<h1 align="center">
  Rossmann Store Sales - Projeto de Machine Learning
</h1>

<h1 align="center">
  <img alt="rossmann" title="#logo" src="./images/forecast_sales.jpg" w=512 heigth="400" width="600"/>
</h1>

## 1. Problema de negócio
  A previsão de vendas para as próximas 6 semanas nas lojas Rossmann fornecerá uma estimativa da receita esperada para o período com base em vários fatores, como dados históricos de vendas, tendências de mercado, sazonalidade, promoções, concorrência e condições econômicas. 
  
  Essa previsão ajudará as lojas Rossmann a planejar e alocar recursos de maneira eficaz, otimizar os níveis de estoque e ajustar preços e estratégias promocionais para maximizar vendas e lucros.

### 1.1 Contexto de Negócio
   A previsão refere-se às lojas Rossmann, que operam com mais de 3000 drogarias. Atualmente, os gerentes de loja da Rossmann têm a tarefa de  prever suas vendas diárias com até seis semanas de antecedência. As vendas da loja são influenciadas por muitos fatores, incluindo promoções, concorrência, feriados escolares e estaduais, sazonalidade e localidade, Com milhares de gerentes individuais prevendo vendas com base em suas circunstâncias únicas, a precisão de resultados pode variar bastante. 
  
  O objetivo da previsão é fornecer às lojas Rossmann informações valiosas sobre o volume de vendas e a receita esperada das próximas 6 semanas, baseado nos dados de vendas das 6 semanas anteriores, o que pode ajudá-los a ajustar suas estratégias e tomar decisões com base nas informações mais recentes. Isso pode ser especialmente importante para uma empresa de varejo como a Rossmann, que pode ser afetada por vários fatores, como concorrência, comportamento do consumidor e condições econômicas.
  
 ### 1.2 Objetivos
Os objetivos da previsão de vendas das lojas Rossmann são:
- Planejamento: A previsão pode ajudar as lojas Rossmann a planejar seu estoque, pessoal e outros recursos de forma mais eficaz, fornecendo-lhes informações sobre o volume de vendas e a receita esperada.
- Orçamento: A previsão pode ajudar as lojas Rossmann a desenvolver um orçamento mais preciso, fornecendo-lhes uma melhor compreensão de suas receitas e despesas esperadas.
- Marketing: A previsão pode ajudar as lojas Rossmann a desenvolver estratégias de marketing mais eficazes, identificando tendências e padrões de comportamento do consumidor, bem como antecipando o impacto de promoções ou eventos futuros.
- Avaliação de desempenho: A previsão pode ajudar as lojas Rossmann a avaliar seu desempenho, comparando seu volume de vendas e receita reais com os valores previstos. Isso pode ajudá-los a identificar áreas de melhoria e fazer ajustes conforme necessário.
- Decisões de negócios: A previsão pode ajudar as lojas Rossmann a tomar decisões de negócios, fornecendo-lhes uma melhor compreensão do mercado e do comportamento do consumidor. Isso pode incluir decisões relacionadas a preços, seleção de produtos e expansão ou contração de operações.
  
No geral, o objetivo da previsão de vendas da loja Rossmann para as próximas 6 semanas é fornecer ao negócio uma compreensão mais clara do desempenho de vendas esperado e ajudar a orientar a tomada de decisões para obter melhores resultados.


### 2.1 Ferramentas
  - Python 3.8
  - Jupyter Notebook
  

## 3. Dados
Os dados para esse projeto foram coletados na plataforma do Kaggle: https://www.kaggle.com/competitions/rossmann-store-sales/data


### 3.1 Atributos de origem

|    Atributos    |                         Definição                            |
| :-------------: | :----------------------------------------------------------: |
|       Id        |          ID que representa uma duplicata (Store, Date)       |
|      Store      |                       Número da loja                         |
|      Sales      |           Quantidade de vendas em um determinado dia         |
|    Customers    |           Quantidade de cliente em um determinado dia        |
|      Open       |           Indicador para saber se a loja estava aberta       |
|  StateHoliday   |                Indica um feriado estadual                    |
|  SchoolHoliday  | Indica se a (Loja, Data) foi afetada pelo fechamento das escolas públicas |
|    StoreType    |   Diferencia entre 4 modelos de loja diferentes: a, b, c, d  |
|    Assortment   |               Descreve um nível de sortimento                       |
| CompetitionDistance | Distância em metros até a loja concorrente mais próxima  |
| CompetitionOpenSince[Month/Year] | Ano e mês aproximados que o concorrente mais próximo foi aberto |
|      Promo      | Indica se uma loja está realizando uma promoção naquele dia  |
|      Promo2     |   É uma promoção contínua e consecutiva para algumas lojas   |
| Promo2Since[Year/Week] | Descreve o ano e a semana do calendário em que a loja começou a participar do Promo2 |
|  PromoInterval  | Descreve os intervalos consecutivos em que o Promo2 é iniciada, nomeando os meses em que a promoção é reiniciada. Por exemplo. "Fevereiro, maio, agosto, novembro" significa que cada rodada começa em fevereiro, maio, agosto, novembro de qualquer ano para essa loja.|


### 3.2 Detalhamento atributos de origem

- Open:
    - 0 = Fechado 
    - 1 = Aberto
- StateHoliday: Normalmente todas as lojas, com poucas exceções, fecham nos feriados estaduais. Observe que todas as escolas fecham nos feriados e fins de semana.
    - a = Feriado
    - b = Feriado da Páscoa
    - c = Natal
    - 0 = Nenhum 
- Assortment: 
    - a = Básico
    - b = Extra
    - c = Estendido
- Promo2:
    - 0 = Loja não está participando
    - 1 = Loja está participando 

## 4. Premissas
- Dados faltantes: 
  - Chequei a quantidade de valores ausentes para todos os campos e fiz os tratamentos para substituir os valores ausentes por valores condizentes para aquele campo. 
    - O primeiro campo que tratei os valores ausentes foi o "competition_distance" , eu decidi preencher os valores ausentes desse campo com um valor baseado no valor máximo de "competition_distance", porque se o valor é ausente, é porque ele não tem um competidor próximos da loja, ou é uma loja muito distante para ser um competidor. Se colocarmos uma distância muito maior que a distância máxima que têm nos dados, é a mesma coisa que dizer que não existe um competidor próximo. 
    - O segundo e terceiro campo que tratei os valores ausentes foi o "competition_open_since_month" e "competition_open_since_year", eu decidi preencher os valores ausentes desses campos com o mês e ano da coluna date. Porque se o valor é ausente, é porque ele não tem um competidor próximo da loja, ou a loja tem um competidor próximo mas não sabe a data que a loja mais próxima foi aberta, ou porque a loja abriu depois e esqueceram de anotar a data.
    - O quarto e quinto campo que tratei os valores ausentes foi o "promo2_since_week" e  "promo2_since_year", eu decidi preencher os valores ausentes desses campos com a data da coluna date e ano da coluna date. Porque se o valor é ausente, significa que a loja não aceitou participar da promoção.
    - O sexto campo que tratei os valores ausentes foi o "promo_interval", eu decidi preencher os valores ausentes desse campo com zero, pois facilita no processamento do modelo de machine learning.
- Criação de novas colunas:
  - A primeira coluna que criei foi de "month_map", que pega a data que é ano, mês e dia e transforma em mês, depois aplica uma lista chamada "month_map", que contém uma lista de números de 1 a 12 e substitui esses números por seus respectivos meses abreviados.
  - A segunda coluna que criei, foi a "is_promo", que pega a "promo_interval" e faz uma divisão baseado na vírgula, para poder quebrar o array que está separado por vírgula em uma lista, depois disso ele checa se a nova coluna "month_map" está dentro dessa lista, se sim, retorna 1, senão, retorna 0. Se a "promo_interval" for igual a 0, retorna 0.
  - A terceira coluna que criei, foi a "year", que extrai o ano da coluna "date".
  - A quarta coluna que criei, foi a "month", que extrai o mês da coluna "date".
  - A quinta coluna que criei, foi a "day", que extrai o dia da coluna "date".
  - A sexta coluna que criei, foi a "week_of_year", que extrai a semana do ano da coluna "date".
  - A sétima coluna que criei, foi a "year_week", que extrai a o ano e semana da coluna "date".
  - A oitava coluna que criei, foi a "competition_since" que agrupa a "competition_open_since_year" com a "competition_open_since_month" e coloca o dia 1, tornando assim uma data. 
  - A nona coluna que criei, foi a "competition_time_month" que pega a coluna date e subtrai com a coluna "competition_since" e divide por 30, para mostrar a quantos meses que a loja está na competição.
  - A décima coluna que criei, foi a "promo_since" que agrupa a "promo2_since_year" com a "promo2_since_week", depois transforma em data.
  - A décima primeira coluna que criei, foi a "promo_time_week" que pega a coluna date e subtrai com a coluna "promo_since" e divide por 7, para mostrar a quantas semanas que a loja está na promoção 2.
- Alteração de tipos de dados:
  - Alterei o tipo dos dados das colunas "competition_open_since_month", "competition_open_since_year", "promo2_since_week" e "promo2_since_year" de float para inteiro.
  - Alterei as descrições da coluna "state_holiday" para "public_holiday" se "a", "easter_holiday" se "b", "christmas" se "c", se não "regular_day"


## 5. Dez Principais Insights
- **H1:** Lojas com maior sortimentos deveriam vender mais.
      
    ✅ **Verdadeira:** 
    - Na média, lojas com MAIOR SORTIMENTO vendem MAIS.
      
- **H2:** Lojas com competidores mais próximos deveriam vender menos.
      
    ❌ **Falsa:** 
    - Lojas com competidores mais próximos entre 0 a 2000 metros, vendem acima da média de vendas que é 6955.

- **H3:** Lojas com competidores à mais tempo deveriam vender mais.
    
    ❌ **Falsa:** 
    - Lojas com competidores à mais tempo vendem menos que a média de vendas que é de 6955.
      
- **H4:** Lojas com promoções ativas por mais tempo deveriam vender mais.
    
    ✅ **Verdadeira:** 
    - Lojas com promoções ativas por mais tempo vendem mais, depois de um certo período de promoção. Muitas lojas ficaram acima da média de vendas de 6955.
      
- **H5:** Lojas com mais promoções consecutivas deveriam vender mais.
    
    ❌ **Falsa:** 
    - Lojas com mais promoções consecutivas vendem menos do que lojas que participam apenas da promoção tradicional (1ª promoção).
      
- **H6:** Lojas abertas durante o feriado de Natal deveriam vender mais.
    
    ❌ **Falsa:** 
    - Lojas abertas durante o feriado de Natal na média vendem mais que os feriados públicos e dias normais, mas vedem menos que o feriado da Páscoa. Somente em 2014 que as lojas venderam mais no feriado de Natal.

- **H7:** Lojas deveriam vender mais ao longo dos anos.
    
    ❌ **Falsa:** 
    - Lojas vendem menos ao longo dos anos.
      
- **H8:** Lojas deveriam vender mais no segundo semestre do ano.
    
    ❌ **Falsa:** 
    - Lojas vendem menos no segundo semestre do ano.
      
- **H9:** Lojas deveriam vender mais depois do dia 10 de cada mês.
   
    ✅ **Verdadeira:** 
    - Lojas vendem mais depois do dia 10 de cada mes. Pelo fato de ter mais dias no mês, 20 dias contra 10. As vendas são maiores antes do dia 10 quando olhamos para as médias de vendas pelos grupos: "Antes do dia 10" & "Depois do dia 10".
      
- **H10:** Lojas deveriam vender mais depois do dia 10 de cada mês.
    
    ✅ **Verdadeira:** 
    - Lojas vendem menos nos finais de semana.
      
## 6. Criação do Modelo de Machine Learning
- Comparei a performance entre os principais modelos pelos 3 tipos de erros, MAE, MAPE e RMSE.
- Optei pelo modelo Random Forest Regressor que apresentou o menor erro RMSE.
- Rodei o modelo final com os melhores valores que o Random Forest escolheu e com menor erro MAE.
- Calculei a performance somando as predições de cada loja, peguei o erro MAE e MAPE para cada loja. 
  - Calculei o melhor e pior cenário de vendas subtraindo e somando o erro MAE. Abaixo a tradução do resultado do cálculo de melhor e pior cenário de vendas para as lojas: 
    - A loja 1 nas próximas 6 semanas vai vender 161 mil e pode ter um erro de 276 e esse erro de 276 corresponde a 6% das vendas reais em média que essa loja faz.
    - A loja 2 nas próximas 6 semanas vai vender 175 mil e pode ter um erro de 338 e esse erro de 338 corresponde a 7% das vendas reais em média que essa loja faz.
    - A loja 3 nas próximas 6 semanas vai vender 261 mil e pode ter um erro de 580 e esse erro de 580 corresponde a 8% das vendas reais em média que essa loja faz.
  
## 7. Resultados Finais 
- Calculei o total da performance e obtive o seguinte resultado:
  - A soma de predições para as próximas 6 semanas em todas as lojas é de 285 milhões, onde no pior cenário vai fazer 284 milhões e no melhor cenário vai fazer 285 milhões.
