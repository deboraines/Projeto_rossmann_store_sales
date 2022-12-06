<h1 align="center">
  Rossmann Store Sales - Projeto de Machine Learning
</h1>

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
