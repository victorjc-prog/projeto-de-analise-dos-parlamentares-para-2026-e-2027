[README_GitHub.md](https://github.com/user-attachments/files/33359132/README_GitHub.md)

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
- **Previsão:** regressão Ridge regularizada por parlamentar, com efeito individual e tendência anual, ajustada aos gastos de 2020–2025. As previsões abaixo cobrem somente os quatro maiores de cada região.

## Principais resultados

O total líquido incluído na análise de 2020–2025 foi **R$ 1.333.828.027,97**. O gasto anual aumentou de **R$ 172,9 milhões em 2020** para **R$ 249,4 milhões em 2024** e recuou **4,0% em 2025**, permanecendo 38,4% acima de 2020. Os dados anuais incluem registros nos 12 meses.

Líderes por região no acumulado de seis anos:

| Região | Parlamentar | UF | Gasto líquido |
|---|---|---:|---:|
| Centro-Oeste | Beto Pereira | MS | R$ 3.104.848,23 |
| Nordeste | João Maia | RN | R$ 3.317.209,88 |
| Norte | Acácio Favacho | AP | R$ 3.192.714,55 |
| Sudeste | Capitão Augusto | SP | R$ 2.906.317,25 |
| Sul | Pompeo de Mattos | RS | R$ 3.315.952,92 |

### Leitura inicial dos quatro maiores por região

Os vinte parlamentares do ranking tiveram registros nos seis anos analisados, reduzindo o efeito de diferenças no tempo observado. A distância entre o primeiro e o quarto colocado ajuda a comparar a concentração dentro de cada grupo:

| Região | Maior acumulado | Quarto colocado | Diferença entre eles | Leitura |
|---|---:|---:|---:|---|
| Centro-Oeste | Beto Pereira, MS | José Medeiros, MT | R$ 319.553,65 (10,3% do líder) | Maior dispersão relativa; os três primeiros são de MS. |
| Nordeste | João Maia, RN | Wellington Roberto, PB | R$ 154.222,93 (4,6% do líder) | Ranking relativamente concentrado; os dois primeiros são do RN. |
| Norte | Acácio Favacho, AP | Olival Marques, PA | R$ 18.195,39 (0,6% do líder) | Menor dispersão; os quatro valores são muito próximos. |
| Sudeste | Capitão Augusto, SP | Da Vitoria, ES | R$ 103.020,38 (3,5% do líder) | Valores próximos; os dois primeiros são de SP. |
| Sul | Pompeo de Mattos, RS | Bibo Nunes, RS | R$ 320.982,28 (9,7% do líder) | Maior diferença absoluta; os quatro primeiros são do RS. |

João Maia (Nordeste) e Pompeo de Mattos (Sul) são os dois maiores valores regionais e diferem por apenas **R$ 1.256,96** no acumulado de seis anos. A concentração por UF descreve somente a composição deste ranking, não o gasto total de cada estado nem evidência de irregularidade.

### Previsões individuais para os 20 parlamentares

Valores anuais estimados para cada um dos quatro maiores gastos de cada região. São previsões nominais, sem correção pela inflação.

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
