[README_GitHub.md](https://github.com/user-attachments/files/33358200/README_GitHub.md)
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
- **Previsão:** regressão Ridge padronizada em painel anual regional, usando tendência temporal e valores dos anos anteriores. A estimativa é nominal, recursiva e não é individual por parlamentar.

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

Projeção exploratória do modelo Ridge:

| Região | 2026 (R$ milhões) | 2027 (R$ milhões) |
|---|---:|---:|
| Norte | 34,55 | 36,19 |
| Nordeste | 70,24 | 68,29 |
| Centro-Oeste | 22,69 | 25,09 |
| Sudeste | 73,15 | 70,76 |
| Sul | 38,03 | 39,02 |
| **Total** | **238,66** | **239,35** |

No teste temporal com 2025 como período de validação, o Ridge teve WAPE de **7,62%**; o baseline de repetir o gasto de 2024 teve **4,22%**. Assim, a projeção de ML deve ser tratada como cenário exploratório, não como previsão confiável para orçamento. O histórico é curto e não há ajuste pela inflação.

A triagem estatística apontou, entre outros casos, um lançamento de **R$ 184.428,00** na categoria de divulgação parlamentar em 2024. O valor requer verificação da documentação e do contexto antes de qualquer conclusão.
