[README_GitHub.md](https://github.com/user-attachments/files/33361134/README_GitHub.md)
# Análise de despesas parlamentares (2020–2025)

Projeto de análise dos gastos registrados pela Câmara dos Deputados, com consolidação por parlamentar e região, análise de tendências, triagem estatística de lançamentos atípicos e projeção exploratória para 2026–2027.

## Dados

O notebook usa os arquivos compactados `Ano-2020.csv.zip` até `Ano-2025.csv.zip`, com os respectivos CSVs anuais no interior de cada ZIP. Por padrão, espera encontrá-los em:

```text
C:\Users\Vitor\Downloads\projeto de análise dos parlamentares para 2026 e 2027\dados_camara
```

Se os arquivos estiverem em outro local, altere `PASTA_DADOS` na primeira célula de código do notebook.

## Como executar

1. Tenha Python 3.9 ou superior e a extensão Jupyter do VS Code instalados.
2. Abra [`analise_despesas_2020_2025.ipynb`](analise_despesas_2020_2025.ipynb) no VS Code.
3. Selecione um kernel Python no botão **Selecionar Kernel**. O notebook usa apenas módulos da biblioteca padrão; não exige instalação de pacotes Python adicionais.
4. Execute as células em ordem com **Run All**. A primeira célula de código lê e agrega os arquivos; as seguintes exibem rankings, tendências, previsão e lançamentos candidatos a revisão.

A leitura de todos os arquivos pode levar alguns minutos, dependendo do computador. Os arquivos ZIP originais não são alterados.

## Método

- **Gasto:** soma de `vlrLiquido`, após glosas. Glosas e restituições são exibidas separadamente e não são subtraídas novamente.
- **Região e ranking:** a UF do parlamentar é mapeada para uma das cinco regiões; os quatro maiores gastos acumulados são selecionados por região usando o identificador do deputado e a UF.
- **Anomalias:** triagem por categoria e ano, sinalizando valores acima de `Q3 + 3 × IQR`. São candidatos para conferência documental, não evidência de irregularidade.
- **Previsão:** regressão Ridge regularizada por parlamentar, com efeito individual e tendência anual, ajustada aos gastos de 2020–2025. A coorte prevista é formada pelos quatro maiores acumulados no período em cada região.

## Principais resultados

O total líquido incluído na análise de 2020–2025 foi **R$ 1.333.828.027,97**. O gasto anual aumentou de **R$ 172,9 milhões em 2020** para **R$ 249,4 milhões em 2024** e recuou **4,0% em 2025**, permanecendo 38,4% acima de 2020. Os dados anuais incluem registros nos 12 meses.

### Quatro maiores gastos por região em cada ano

Ranking anual de `vlrLiquido` por ID de parlamentar e UF. Os nomes e as posições podem mudar de um ano para outro; os valores não são acumulados entre anos.

| Ano | Região | 1º | 2º | 3º | 4º |
|---:|---|---|---|---|---|
| 2020 | Norte | Jhonatan de Jesus (RR), R$ 551.380,32 | Jesus Sérgio (AC), R$ 543.409,93 | Marcelo Ramos (AM), R$ 538.354,87 | Jéssica Sales (AC), R$ 527.506,10 |
| 2020 | Nordeste | João Maia (RN), R$ 526.271,01 | Wellington Roberto (PB), R$ 526.106,91 | João Marcelo Souza (MA), R$ 514.712,63 | José Guimarães (CE), R$ 508.971,91 |
| 2020 | Centro-Oeste | Carlos Bezerra (MT), R$ 460.577,76 | Dagoberto Nogueira (MS), R$ 445.759,95 | Beto Pereira (MS), R$ 444.887,80 | José Nelto (GO), R$ 427.339,90 |
| 2020 | Sudeste | Herculano Passos (SP), R$ 454.958,10 | Vinicius Carvalho (SP), R$ 453.641,39 | Dra. Soraya Manato (ES), R$ 445.263,70 | Paulo Teixeira (SP), R$ 444.612,49 |
| 2020 | Sul | Nereu Crispim (RS), R$ 491.631,58 | Luisa Canziani (PR), R$ 469.075,94 | Roman (PR), R$ 466.912,08 | Gleisi Hoffmann (PR), R$ 466.801,61 |
| 2021 | Norte | Edio Lopes (RR), R$ 541.431,66 | Joenia Wapichana (RR), R$ 539.838,78 | Perpétua Almeida (AC), R$ 534.692,55 | Jéssica Sales (AC), R$ 533.942,71 |
| 2021 | Nordeste | Eduardo Bismarck (CE), R$ 566.706,26 | Carla Dickson (RN), R$ 524.552,72 | Efraim Filho (PB), R$ 517.791,91 | Wellington Roberto (PB), R$ 515.562,52 |
| 2021 | Centro-Oeste | Beto Pereira (MS), R$ 501.448,15 | Dr. Luiz Ovando (MS), R$ 488.892,59 | Loester Trutis (MS), R$ 480.922,27 | Dagoberto Nogueira (MS), R$ 479.800,48 |
| 2021 | Sudeste | Alexandre Leite (SP), R$ 475.193,76 | Lauriete (ES), R$ 460.550,39 | Neucimar Fraga (ES), R$ 457.898,78 | Herculano Passos (SP), R$ 456.297,04 |
| 2021 | Sul | Giovani Cherini (RS), R$ 514.155,55 | Afonso Motta (RS), R$ 511.337,31 | Osmar Terra (RS), R$ 487.103,10 | Nereu Crispim (RS), R$ 486.220,40 |
| 2022 | Norte | Joenia Wapichana (RR), R$ 563.759,50 | Jesus Sérgio (AC), R$ 548.923,13 | Edio Lopes (RR), R$ 544.950,69 | Ottaci Nascimento (RR), R$ 542.126,25 |
| 2022 | Nordeste | José Airton Félix Cirilo (CE), R$ 526.215,85 | Marreca Filho (MA), R$ 523.635,85 | Júnior Mano (CE), R$ 521.462,33 | Heitor Freire (CE), R$ 520.790,63 |
| 2022 | Centro-Oeste | Dagoberto Nogueira (MS), R$ 491.460,64 | Loester Trutis (MS), R$ 487.065,25 | Vander Loubet (MS), R$ 483.003,72 | Professora Rosa Neide (MT), R$ 477.353,88 |
| 2022 | Sudeste | Gilberto Nascimento (SP), R$ 465.041,75 | Capitão Augusto (SP), R$ 460.752,48 | Orlando Silva (SP), R$ 460.393,69 | Coronel Tadeu (SP), R$ 456.073,06 |
| 2022 | Sul | Covatti Filho (RS), R$ 508.792,99 | Bibo Nunes (RS), R$ 505.572,14 | Pedro Westphalen (RS), R$ 504.881,77 | Afonso Motta (RS), R$ 504.220,38 |
| 2023 | Norte | Vinicius Gurgel (AP), R$ 597.229,43 | Acácio Favacho (AP), R$ 591.128,85 | Coronel Ulysses (AC), R$ 589.361,60 | Zé Haroldo Cathedral (RR), R$ 587.320,04 |
| 2023 | Nordeste | General Girão (RN), R$ 619.991,85 | André Ferreira (PE), R$ 612.213,04 | Luizianne Lins (CE), R$ 587.806,32 | João Maia (RN), R$ 587.224,12 |
| 2023 | Centro-Oeste | Beto Pereira (MS), R$ 608.522,56 | Vander Loubet (MS), R$ 563.078,95 | José Medeiros (MT), R$ 550.447,14 | Dr. Luiz Ovando (MS), R$ 520.559,10 |
| 2023 | Sudeste | Capitão Augusto (SP), R$ 547.056,95 | Cezinha de Madureira (SP), R$ 545.231,54 | Tabata Amaral (SP), R$ 529.418,71 | Amaro Neto (ES), R$ 524.405,69 |
| 2023 | Sul | Pompeo de Mattos (RS), R$ 653.696,75 | Pedro Westphalen (RS), R$ 594.957,63 | Bibo Nunes (RS), R$ 580.505,60 | Giovani Cherini (RS), R$ 575.539,57 |
| 2024 | Norte | Zé Haroldo Cathedral (RR), R$ 633.590,14 | Gabriel Mota (RR), R$ 622.715,36 | Albuquerque (RR), R$ 618.284,19 | Defensor Stélio Dener (RR), R$ 614.005,49 |
| 2024 | Nordeste | Lucas Ramos (PE), R$ 623.231,72 | André Ferreira (PE), R$ 615.959,83 | General Girão (RN), R$ 604.342,88 | João Maia (RN), R$ 604.006,03 |
| 2024 | Centro-Oeste | Geraldo Resende (MS), R$ 574.083,10 | Dagoberto Nogueira (MS), R$ 563.249,67 | Rodolfo Nogueira (MS), R$ 555.517,15 | Coronel Fernanda (MT), R$ 552.063,67 |
| 2024 | Sudeste | Gilberto Nascimento (SP), R$ 552.751,37 | Cezinha de Madureira (SP), R$ 549.494,22 | Ricardo Salles (SP), R$ 543.435,14 | Jonas Donizette (SP), R$ 538.659,93 |
| 2024 | Sul | Pompeo de Mattos (RS), R$ 667.819,06 | Daiana Santos (RS), R$ 582.386,91 | Afonso Motta (RS), R$ 580.969,20 | Pedro Westphalen (RS), R$ 577.848,12 |
| 2025 | Norte | Gabriel Mota (RR), R$ 621.578,60 | Eduardo Velloso (AC), R$ 608.822,06 | Albuquerque (RR), R$ 607.323,43 | Cristiane Lopes (RO), R$ 602.717,30 |
| 2025 | Nordeste | General Girão (RN), R$ 583.965,76 | João Maia (RN), R$ 578.399,79 | Ruy Carneiro (PB), R$ 577.959,06 | Natália Bonavides (RN), R$ 573.830,35 |
| 2025 | Centro-Oeste | Rodolfo Nogueira (MS), R$ 570.068,96 | Geraldo Resende (MS), R$ 562.066,17 | Rodrigo da Zaeli (MT), R$ 547.852,28 | Dagoberto Nogueira (MS), R$ 541.796,46 |
| 2025 | Sudeste | Paulo Folletto (ES), R$ 540.891,83 | Bebeto (RJ), R$ 517.812,00 | Carlos Zarattini (SP), R$ 517.717,63 | Renata Abreu (SP), R$ 516.802,65 |
| 2025 | Sul | Pompeo de Mattos (RS), R$ 591.318,51 | Heitor Schuch (RS), R$ 590.729,20 | Franciane Bayer (RS), R$ 558.795,95 | Bibo Nunes (RS), R$ 557.790,37 |

Este quadro é anual, não acumulado. A previsão 2026–2027 apresentada abaixo usa outro critério de seleção: os 20 maiores gastos acumulados de 2020–2025.

### Comportamento e tendências

- O gasto nominal total avançou 21,0% em 2021, desacelerou em 2022 (+4,5%) e 2024 (+2,0%), voltou a crescer em 2023 (+11,9%) e caiu 4,0% em 2025. Mesmo após a queda, 2025 ficou 38,4% acima de 2020.
- Entre 2020 e 2025, Centro-Oeste teve o maior crescimento regional relativo (+59,8%) e Sul veio em seguida (+58,5%). Em 2025, porém, representaram apenas 8,0% e 15,3% do total analisado; Sudeste (32,3%) e Nordeste (30,9%) concentraram a maior parcela. Crescimento relativo não é o mesmo que participação no gasto total.
- A liderança anual muda mais no Norte: houve seis líderes diferentes. No Sul, Pompeo de Mattos liderou em 2023, 2024 e 2025; no Nordeste, General Girão foi líder em 2023 e 2025. Beto Pereira liderou o Centro-Oeste em 2021 e 2023; Gilberto Nascimento liderou o Sudeste em 2022 e 2024.
- Nas 24 posições de top 4 acumuladas nos seis anos, MS ocupou 18 no Centro-Oeste, RS ocupou 21 no Sul, SP ocupou 18 no Sudeste, RR ocupou 13 no Norte e RN ocupou 9 no Nordeste. Essas contagens descrevem somente quem aparece no ranking anual, não a participação dessas UFs no gasto regional total.

### Previsões individuais para os 20 parlamentares

Valores anuais estimados para os quatro maiores gastos acumulados de 2020–2025 em cada região. Essa coorte de 20 parlamentares é diferente dos top 4 anuais da tabela anterior. São previsões nominais, sem correção pela inflação.

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

Subtotal estimado apenas para os quatro parlamentares selecionados em cada região:

| Região | 2026 | 2027 |
|---|---:|---:|
| Norte | R$ 2.251.380,80 | R$ 2.297.774,83 |
| Nordeste | R$ 2.269.519,86 | R$ 2.315.913,89 |
| Centro-Oeste | R$ 2.168.095,93 | R$ 2.214.489,96 |
| Sudeste | R$ 2.127.327,47 | R$ 2.173.721,51 |
| Sul | R$ 2.227.586,68 | R$ 2.273.980,71 |
| **Total dos 20** | **R$ 11.043.910,73** | **R$ 11.275.880,90** |

Os subtotais regionais e o total dos parlamentares são arredondados independentemente; pode haver diferença de R$ 0,01 ao somar as linhas exibidas.

Nos backtests de origem móvel, em 2024 o Ridge teve WAPE de **5,12%**, contra **4,38%** do baseline de repetir o gasto do ano anterior; em 2025, o Ridge teve **5,28%**, contra **6,11%** do baseline. Combinados, os erros foram praticamente iguais: **5,20% para Ridge e 5,22% para o baseline**. A amostra tem apenas seis observações anuais por parlamentar; as projeções são exploratórias, não previsão garantida de orçamento. Os subtotais não representam a despesa total das regiões nem de toda a Câmara.

A triagem estatística apontou, entre outros casos, um lançamento de **R$ 184.428,00** na categoria de divulgação parlamentar em 2024. O valor requer verificação da documentação e do contexto antes de qualquer conclusão.
