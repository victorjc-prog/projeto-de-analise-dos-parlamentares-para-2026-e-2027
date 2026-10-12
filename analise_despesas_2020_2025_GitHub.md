# Análise de despesas parlamentares, 2020–2025

## Objetivo

Consolidar os gastos registrados pela Câmara dos Deputados entre 2020 e 2025, identificar os quatro maiores gastos acumulados por região, observar padrões de comportamento, sinalizar lançamentos estatisticamente atípicos e produzir um cenário exploratório para 2026 e 2027.

A análise reproduzível está no [notebook Jupyter](analise_despesas_2020_2025.ipynb).

## Fonte e escopo

Foram utilizados os arquivos `Ano-2020.csv.zip` a `Ano-2025.csv.zip`, na pasta `dados_camara`. Cada arquivo contém lançamentos mensais de despesas. Os dados disponíveis cobrem os 12 meses de cada ano.

O gasto considerado é `vlrLiquido`, já após glosas. Glosas e restituições são reportadas separadamente e não são descontadas uma segunda vez. Registros sem parlamentar identificado ou sem UF brasileira válida foram excluídos dos rankings e dos totais regionais. Os valores são nominais, sem ajuste pela inflação.

## Principais resultados

O total líquido incluído na análise foi **R$ 1.333.828.027,97**. O total anual passou de **R$ 172,9 milhões em 2020** para **R$ 249,4 milhões em 2024**; em 2025 recuou **4,0%** em relação ao ano anterior, permanecendo **38,4% acima de 2020**.

Nordeste e Sudeste concentraram os maiores totais regionais em 2025, com aproximadamente 30,9% e 32,3% do valor analisado, respectivamente. Em crescimento acumulado entre 2020 e 2025, Centro-Oeste e Sul avançaram cerca de 59% e 58%.

## Quatro maiores por região

Soma de `vlrLiquido` por identificador de deputado e UF no período completo. O partido indicado é o do último registro observado.

| Região | Parlamentar | UF | Partido | Gasto líquido 2020–2025 |
|---|---|---:|---|---:|
| Centro-Oeste | Beto Pereira | MS | REPUBLICANOS | R$ 3.104.848,23 |
| Centro-Oeste | Dagoberto Nogueira | MS | PP | R$ 3.037.551,46 |
| Centro-Oeste | Vander Loubet | MS | PT | R$ 2.913.347,08 |
| Centro-Oeste | José Medeiros | MT | PL | R$ 2.785.294,58 |
| Nordeste | João Maia | RN | PP | R$ 3.317.209,88 |
| Nordeste | General Girão | RN | PL | R$ 3.270.844,20 |
| Nordeste | Flávio Nogueira | PI | PT | R$ 3.180.307,51 |
| Nordeste | Wellington Roberto | PB | PSD | R$ 3.162.986,95 |
| Norte | Acácio Favacho | AP | MDB | R$ 3.192.714,55 |
| Norte | Delegado Éder Mauro | PA | PL | R$ 3.186.016,40 |
| Norte | Sidney Leite | AM | PSD | R$ 3.183.103,56 |
| Norte | Olival Marques | PA | PODE | R$ 3.174.519,16 |
| Sudeste | Capitão Augusto | SP | PL | R$ 2.906.317,25 |
| Sudeste | Cezinha de Madureira | SP | PL | R$ 2.885.841,09 |
| Sudeste | Odair Cunha | MG | PT | R$ 2.807.325,21 |
| Sudeste | Da Vitoria | ES | PP | R$ 2.803.296,87 |
| Sul | Pompeo de Mattos | RS | PDT | R$ 3.315.952,92 |
| Sul | Giovani Cherini | RS | PL | R$ 3.117.112,38 |
| Sul | Afonso Motta | RS | PDT | R$ 3.052.530,96 |
| Sul | Bibo Nunes | RS | PL | R$ 2.994.970,64 |

### Leitura inicial do ranking

Os vinte parlamentares listados tiveram registros nos seis anos analisados, então a comparação acumulada não se explica apenas por diferenças no número de anos com dados. A distância entre o primeiro e o quarto colocado varia bastante entre regiões:

| Região | Maior acumulado | Quarto colocado | Diferença entre eles | Leitura |
|---|---:|---:|---:|---|
| Centro-Oeste | Beto Pereira, MS | José Medeiros, MT | R$ 319.553,65 (10,3% do líder) | Maior dispersão relativa; os três primeiros são de MS. |
| Nordeste | João Maia, RN | Wellington Roberto, PB | R$ 154.222,93 (4,6% do líder) | Ranking relativamente concentrado; os dois primeiros são do RN. |
| Norte | Acácio Favacho, AP | Olival Marques, PA | R$ 18.195,39 (0,6% do líder) | Menor dispersão; os quatro valores são muito próximos. |
| Sudeste | Capitão Augusto, SP | Da Vitoria, ES | R$ 103.020,38 (3,5% do líder) | Valores próximos; os dois primeiros são de SP. |
| Sul | Pompeo de Mattos, RS | Bibo Nunes, RS | R$ 320.982,28 (9,7% do líder) | Maior diferença absoluta; os quatro primeiros são do RS. |

João Maia (Nordeste) e Pompeo de Mattos (Sul) são os dois maiores valores regionais e diferem por apenas **R$ 1.256,96** no acumulado de seis anos. A concentração por UF descreve apenas a composição deste ranking de maiores gastos; não significa, por si só, que a mesma UF lidere o gasto total da região ou que exista irregularidade.

## Anomalias para revisão

A triagem foi feita dentro de cada categoria e ano, sinalizando valores acima de `Q3 + 3 × IQR`. Entre os maiores casos identificados:

| Ano | Parlamentar | UF | Categoria | Lançamento |
|---:|---|---:|---|---:|
| 2024 | Duda Ramos | RR | Divulgação da atividade parlamentar | R$ 184.428,00 |
| 2022 | Expedito Netto | RO | Divulgação da atividade parlamentar | R$ 168.000,00 |
| 2022 | Alex Manente | SP | Divulgação da atividade parlamentar | R$ 166.600,00 |
| 2023 | Gustinho Ribeiro | SE | Divulgação da atividade parlamentar | R$ 164.900,00 |

O limite de triagem para o primeiro caso foi R$ 27.880,00. Esses valores são **alertas estatísticos**, não evidência de irregularidade; precisam ser avaliados junto aos documentos, fornecedores e períodos cobertos. O método gera milhares de candidatos por ano e serve para priorizar conferências.

## Previsão individual para 2026–2027

Foi ajustado um modelo Ridge regularizado por parlamentar, com efeito individual e tendência anual, usando os gastos líquidos anuais de 2020 a 2025. A tabela mostra previsões individuais para os quatro maiores acumulados de cada região. Valores nominais, sem correção pela inflação.

| Região | Parlamentar | UF | 2026 | 2027 |
|---|---|---:|---:|---:|
| Norte | Acácio Favacho | AP | R$ 563.647,63 | R$ 575.246,14 |
| Norte | Delegado Éder Mauro | PA | R$ 563.024,55 | R$ 574.623,05 |
| Norte | Sidney Leite | AM | R$ 562.753,58 | R$ 574.352,09 |
| Norte | Olival Marques | PA | R$ 561.955,04 | R$ 573.553,54 |
| Nordeste | João Maia | RN | R$ 575.228,59 | R$ 586.827,10 |
| Nordeste | General Girão | RN | R$ 570.915,50 | R$ 582.514,01 |
| Nordeste | Flávio Nogueira | PI | R$ 562.493,49 | R$ 574.092,00 |
| Nordeste | Wellington Roberto | PB | R$ 560.882,27 | R$ 572.480,78 |
| Centro-Oeste | Beto Pereira | MS | R$ 555.474,02 | R$ 567.072,53 |
| Centro-Oeste | Dagoberto Nogueira | MS | R$ 549.213,85 | R$ 560.812,36 |
| Centro-Oeste | Vander Loubet | MS | R$ 537.659,96 | R$ 549.258,47 |
| Centro-Oeste | José Medeiros | MT | R$ 525.748,10 | R$ 537.346,61 |
| Sudeste | Capitão Augusto | SP | R$ 537.006,02 | R$ 548.604,53 |
| Sudeste | Cezinha de Madureira | SP | R$ 535.101,26 | R$ 546.699,77 |
| Sudeste | Odair Cunha | MG | R$ 527.797,46 | R$ 539.395,97 |
| Sudeste | Da Vitoria | ES | R$ 527.422,73 | R$ 539.021,24 |
| Sul | Pompeo de Mattos | RS | R$ 575.111,66 | R$ 586.710,17 |
| Sul | Giovani Cherini | RS | R$ 556.614,87 | R$ 568.213,38 |
| Sul | Afonso Motta | RS | R$ 550.607,30 | R$ 562.205,80 |
| Sul | Bibo Nunes | RS | R$ 545.252,85 | R$ 556.851,36 |

Subtotal estimado apenas para o top 4 de cada região:

| Região | 2026 | 2027 |
|---|---:|---:|
| Norte | R$ 2.251.380,80 | R$ 2.297.774,83 |
| Nordeste | R$ 2.269.519,86 | R$ 2.315.913,89 |
| Centro-Oeste | R$ 2.168.095,93 | R$ 2.214.489,96 |
| Sudeste | R$ 2.127.327,47 | R$ 2.173.721,51 |
| Sul | R$ 2.227.586,68 | R$ 2.273.980,71 |
| **Total dos 20 parlamentares** | **R$ 11.043.910,73** | **R$ 11.275.880,90** |

Os subtotais regionais e o total dos parlamentares são arredondados independentemente; pode haver diferença de R$ 0,01 ao somar as linhas exibidas.

### Validação e limitações

Backtests de origem móvel: 2024 teve WAPE de **5,12%** para Ridge e **4,38%** para o baseline de repetir o gasto do ano anterior; 2025 teve **5,28%** para Ridge e **6,11%** para o baseline. Combinando os dois anos, o Ridge marcou **5,20%** e o baseline **5,22%**. O desempenho é praticamente empatado, sem evidência de vantagem robusta do ML.

O histórico tem somente seis observações anuais por parlamentar. As previsões são cenários exploratórios, não valores garantidos para orçamento. Os subtotais cobrem apenas estes vinte parlamentares, não toda a despesa das regiões ou da Câmara.

## Reproduzir

1. Mantenha os seis arquivos ZIP na pasta `dados_camara` esperada pelo notebook, ou ajuste `PASTA_DADOS` na primeira célula de código.
2. Abra [o notebook de análise](analise_despesas_2020_2025.ipynb) no VS Code ou Jupyter.
3. Selecione um kernel Python 3.9 ou superior e execute as células em ordem.

O notebook usa a biblioteca padrão do Python e não requer pacotes adicionais. A leitura integral dos arquivos pode levar alguns minutos.
