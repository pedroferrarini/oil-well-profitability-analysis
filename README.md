# Análise de Rentabilidade de Poços de Petróleo

## Sobre o projeto

Este projeto tem como objetivo identificar a região mais adequada para o desenvolvimento de poços de petróleo, considerando a previsão de reservas, o retorno financeiro potencial e o risco de prejuízo.

A análise utiliza dados geológicos de três regiões, modelos de Regressão Linear e simulações estatísticas com Bootstrap para avaliar a viabilidade econômica e apoiar decisões orientadas por dados.

Projeto desenvolvido como parte da formação em Data Science da TripleTen.

## Objetivos

- Realizar análise exploratória dos dados de três regiões.
- Treinar modelos de Regressão Linear para prever o volume de reservas.
- Avaliar o desempenho dos modelos utilizando RMSE.
- Calcular o ponto de equilíbrio financeiro da operação.
- Estimar o lucro dos 200 poços mais promissores de cada região.
- Aplicar Bootstrap para estimar a distribuição dos lucros.
- Calcular o risco de prejuízo e recomendar a região mais viável.

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Scikit-learn
- Jupyter Notebook
- Regressão Linear
- StandardScaler
- Bootstrap

## Etapas do projeto

### 1. Análise exploratória dos dados

Foram analisados três conjuntos de dados geológicos, cada um representando uma região.

Cada conjunto possui 100.000 registros e cinco colunas:

| Coluna | Descrição |
|---|---|
| `id` | Identificador do poço |
| `f0` | Característica geológica |
| `f1` | Característica geológica |
| `f2` | Característica geológica |
| `product` | Volume de reservas do poço |

A análise inicial identificou que os conjuntos não apresentam valores ausentes ou linhas duplicadas. A coluna `id` foi mantida como identificador, sem ser utilizada como variável preditora.

As médias de reservas observadas foram:

| Região | Média de reservas |
|---|---:|
| Região 0 | 92,50 |
| Região 1 | 68,83 |
| Região 2 | 95,00 |

Apesar de a Região 2 apresentar a maior média, esse indicador, isoladamente, não determina a melhor alternativa de investimento.

### 2. Treinamento e avaliação dos modelos

Foi desenvolvida uma função para treinar um modelo de Regressão Linear em cada região.

Os dados foram divididos em 75% para treinamento e 25% para validação. As variáveis preditoras foram padronizadas com `StandardScaler`, ajustado apenas sobre os dados de treinamento.

O desempenho foi avaliado utilizando RMSE (*Root Mean Squared Error*), métrica que mede a magnitude dos erros de previsão na mesma unidade da variável-alvo.

| Região | Média prevista | RMSE |
|---|---:|---:|
| Região 0 | 92,59 | 37,58 |
| Região 1 | 68,73 | 0,89 |
| Região 2 | 94,97 | 40,03 |

A Região 1 apresentou o menor RMSE, indicando maior precisão preditiva nesse conjunto de dados.

### 3. Análise financeira

Para avaliar a viabilidade econômica, foram utilizadas as seguintes premissas:

| Parâmetro | Valor |
|---|---:|
| Orçamento total | US$ 100.000.000 |
| Receita por unidade de produto | US$ 4.500 |
| Quantidade de poços selecionados | 200 |
| Volume total necessário para o ponto de equilíbrio | 22.222,22 unidades |
| Volume médio necessário por poço | 111,11 unidades |

As médias observadas nas três regiões ficaram abaixo do volume médio necessário por poço. Por isso, a seleção dos poços com maior potencial de produção é essencial para a viabilidade do projeto.

### 4. Estimativa inicial de lucro

Foram selecionados os 200 poços com maiores previsões de reservas em cada região. O lucro foi calculado com base no volume real de produto dos poços selecionados, na receita por unidade e no orçamento total.

| Região | Lucro estimado |
|---|---:|
| Região 0 | US$ 33,21 milhões |
| Região 1 | US$ 24,15 milhões |
| Região 2 | US$ 27,10 milhões |

Na estimativa inicial, a Região 0 apresentou o maior lucro potencial. Entretanto, essa análise pontual não considera suficientemente a incerteza dos resultados e o risco de prejuízo.

### 5. Simulação Bootstrap e análise de risco

Foi aplicada a técnica Bootstrap com 1.000 iterações, utilizando amostras de 500 registros e selecionando os 200 poços mais promissores em cada simulação.

Essa abordagem permitiu estimar o lucro médio, o intervalo de confiança de 95% e a probabilidade de obter lucro negativo.

| Região | Lucro médio estimado | Intervalo de confiança de 95% | Risco de prejuízo |
|---|---:|---:|---:|
| Região 0 | US$ 3,96 milhões | −US$ 1,11 mi a US$ 9,10 mi | 6,9% |
| Região 1 | US$ 4,56 milhões | US$ 338,21 mil a US$ 8,52 mi | 1,5% |
| Região 2 | US$ 4,04 milhões | −US$ 1,63 mi a US$ 9,50 mi | 7,6% |

O critério estabelecido foi selecionar uma região com risco de prejuízo inferior a 2,5%.

A Região 1 foi a única que atendeu a esse requisito. Além disso, apresentou o maior lucro médio estimado no Bootstrap e um intervalo de confiança de 95% inteiramente positivo.

## Conclusão

Inicialmente, a Região 0 parecia ser a melhor alternativa por apresentar o maior lucro na estimativa pontual dos 200 poços selecionados. No entanto, após a aplicação do Bootstrap, a conclusão mudou.

A **Região 1 foi identificada como a alternativa mais adequada para o investimento**, considerando os critérios financeiros e de risco definidos no projeto.

Os principais resultados foram:

- **Maior lucro médio no Bootstrap:** aproximadamente US$ 4,56 milhões.
- **Menor risco de prejuízo:** 1,5%, abaixo do limite de 2,5%.
- **Intervalo de confiança de 95% positivo:** de aproximadamente US$ 338 mil a US$ 8,52 milhões.
- **Maior precisão preditiva:** RMSE de aproximadamente 0,89.

O projeto demonstra como a combinação de análise exploratória, Machine Learning e simulação estatística pode contribuir para decisões de negócio mais fundamentadas, considerando tanto o retorno financeiro esperado quanto os riscos envolvidos.

## Competências desenvolvidas

- Análise exploratória e preparação de dados.
- Manipulação de dados com Pandas e NumPy.
- Treinamento de modelos de Machine Learning.
- Regressão Linear e avaliação por RMSE.
- Padronização de variáveis preditoras.
- Cálculo de viabilidade econômica e estimativa de lucro.
- Simulação estatística com Bootstrap.
- Análise de risco e interpretação de intervalos de confiança.
- Comunicação de resultados para apoiar decisões de negócio.
