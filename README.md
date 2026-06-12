# Previsão de Demanda para Dimensionamento de Capacidade Operacional

Trabalho de Conclusão de Curso (Engenharia de Produção — UVV, 2026) que integra **previsão de demanda** e **análise de capacidade produtiva** em uma rede de empresas prestadoras de serviços, usando modelos estatísticos e de machine learning em Python.

## Objetivo

Analisar a relação entre capacidade produtiva e previsão de demanda, propondo um modelo de apoio ao planejamento e à alocação de recursos humanos. A ideia central é responder, com granularidade por empresa e por mês: **quanta equipe é necessária, onde e quando.**

## Contexto

O estudo simula uma rede de **80 empresas** do setor de reparação e instalação de vidros automotivos, com **5 produtos** (para-brisa, vigia, laterais, farol, retrovisor), totalizando **730.400 registros** diários entre 2021 e 2025. Os dados são simulados com parâmetros controlados (sazonalidade intra-anual, crescimento de 5% a.a. e variabilidade estocástica de Poisson) para validar o pipeline analítico em ambiente reprodutível antes de uma eventual aplicação a dados reais.

## O que foi feito

1. **Construção e simulação da base de dados** — volume de atendimentos, tempo médio por produto e quadro de colaboradores por empresa.
2. **Limpeza e EDA** — remoção de outliers de tempo pelo método do boxplot (IQR) e análise exploratória das componentes da série (tendência, sazonalidade anual e semanal).
3. **Modelagem de séries temporais** — desenvolvimento e comparação de três modelos de previsão para 2026.
4. **Análise de capacidade** — cálculo da taxa de utilização (demanda ÷ capacidade, base de 480 min/colaborador/dia) e classificação operacional por empresa.
5. **Integração dos resultados** — identificação de empresas críticas e ociosas e do reforço de quadro necessário.

## Modelos comparados

| Modelo | R² (validação 2025) | Observação |
|---|---|---|
| **Prophet** | **0,9966** | Melhor equilíbrio; múltiplas sazonalidades + feriados — **modelo de referência** |
| Random Forest | 0,9955 | Boa validação; regride à média em horizontes longos |
| ARIMA/SARIMA | −27,21 | Não modela bem múltiplas sazonalidades (R² negativo) |

Métricas de avaliação utilizadas: **MAE, RMSE, MAPE e R²**.

## Principais resultados (projeção 2026)

- Taxa de utilização média projetada de **100,6%**, contra **87,0%** da média histórica.
- **56 das 80 empresas** operando em situação crítica (utilização > 90%).
- Picos de sobrecarga concentrados em **janeiro e dezembro**; folga em julho/agosto.
- Coexistência de empresas sobrecarregadas e ociosas no mesmo portfólio — uma **ineficiência sistêmica de alocação** passível de correção por realocação ou compartilhamento de equipes.

## Tecnologias

`Python` · `Pandas` · `NumPy` · `Statsmodels` · `Prophet` · `Scikit-learn` · `Matplotlib` · `Seaborn`

## Conclusão

A integração entre previsão de demanda e análise de capacidade produtiva, implementada com granularidade por empresa e produto, mostrou-se uma ferramenta robusta de apoio à decisão. Como limitação, destaca-se o uso de dados simulados; como trabalho futuro, recomenda-se a aplicação a bases reais para validação empírica.

---

**Autor:** Leonardo Rodrigues dos Santos
**Orientador:** Prof. Emerson Scheidegger
**Universidade Vila Velha — Engenharia de Produção — 2026**
