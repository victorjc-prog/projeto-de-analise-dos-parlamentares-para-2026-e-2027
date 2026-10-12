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

## Projeção exploratória para 2026–2027

Foi usado um modelo Ridge padronizado em um painel anual por região, com tendência temporal e valores dos anos anteriores. A previsão é recursiva, nominal e não individual por parlamentar.

| Região | 2026 (R$ milhões) | 2027 (R$ milhões) |
|---|---:|---:|
| Norte | 34,55 | 36,19 |
| Nordeste | 70,24 | 68,29 |
| Centro-Oeste | 22,69 | 25,09 |
| Sudeste | 73,15 | 70,76 |
| Sul | 38,03 | 39,02 |
| **Total** | **238,66** | **239,35** |

Na validação temporal com 2025 como período de teste, o Ridge teve WAPE de **7,62%**. O baseline de repetir o valor de 2024 teve **4,22%**, sendo mais preciso nesse teste. Como há apenas seis anos de histórico e um único ano de validação, os números de 2026–2027 devem ser tratados como cenário exploratório, não como previsão confiável para orçamento. Recomenda-se ampliar o histórico e executar backtests em vários períodos antes de usar o modelo em decisões.

## Reproduzir

1. Mantenha os seis arquivos ZIP na pasta `dados_camara` esperada pelo notebook, ou ajuste `PASTA_DADOS` na primeira célula de código.
2. Abra [o notebook de análise](analise_despesas_2020_2025.ipynb) no VS Code ou Jupyter.
3. Selecione um kernel Python 3.9 ou superior e execute as células em ordem.

O notebook usa a biblioteca padrão do Python e não requer pacotes adicionais. A leitura integral dos arquivos pode levar alguns minutos.
