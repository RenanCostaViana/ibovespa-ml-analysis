# 📈 Ibovespa ML Analysis — Market Data Analytics

Análise do mercado financeiro brasileiro utilizando Machine Learning
Projeto de análise exploratória e experimentação preditiva com dados históricos do Ibovespa

---

## 🧠 Visão Geral

Este projeto analisa dados históricos do índice Ibovespa, aplicando **análise de dados**, **testes de estacionariedade** e **Machine Learning** para explorar padrões, avaliar diferentes transformações da série temporal e entender os limites de modelos preditivos em um contexto notoriamente ruidoso, como o mercado financeiro.

O foco do projeto é **analítico e educacional**, buscando compreender o comportamento dos dados e avaliar criticamente o uso de modelos de ML — incluindo onde as métricas de avaliação podem enganar.

> ⚠️ Este projeto **não constitui recomendação de investimento** e não tem como objetivo prever ou sugerir operações de compra ou venda.

---

## 🎯 Objetivos do Projeto

- Explorar dados históricos do Ibovespa e compreender sua estrutura
- Realizar análise exploratória (EDA) de preços, retornos e variações
- Testar formalmente a estacionariedade da série sob diferentes transformações (nível, médias móveis, log-detrend, diferenciação)
- Aplicar e comparar modelos de séries temporais (Naive, SeasonalNaive, SeasonalWindowAverage, AutoARIMA e Prophet)
- Avaliar criticamente o desempenho e as limitações dos modelos e das métricas de erro
- Documentar o processo de forma clara, crítica e responsável

---

## 📊 Etapas da Análise

1. **Aquisição e entendimento dos dados**
   - Série histórica diária do índice (via `yfinance`)
   - Organização temporal e tratamento inicial

2. **Análise Exploratória (EDA)**
   - Comportamento de preços e volume
   - Decomposição sazonal e funções de autocorrelação (ACF/PACF)

3. **Testes de Estacionariedade (ADF)**
   - Comparação de quatro representações da série: nível puro, médias móveis (detrend), log-detrend e diferenciação
   - Cada transformação é testada formalmente com o teste de Dickey-Fuller aumentado (ADF)

4. **Modelagem**
   - Comparação de modelos estatísticos (Naive, SeasonalNaive, SeasonalWindowAverage, AutoARIMA) e do Prophet
   - Avaliação de erro (WMAPE) e de acurácia direcional (acerto da alta ou baixa de cada dia em relação ao dia anterior)
   - **Desenho do teste:** os modelos são treinados até o início do período de teste e preveem os ~30 pregões finais **de uma só vez** (horizonte de vários passos), sem serem reajustados com os fechamentos reais ao longo do período. A direção prevista para cada dia compara a previsão daquele dia com a previsão do dia anterior (ou com o último fechamento real, no primeiro dia).
   - Esse desenho é mais exigente do que uma previsão estritamente de um dia à frente (*walk-forward*), em que o modelo conheceria o fechamento real da véspera antes de cada previsão — os resultados de acurácia devem ser lidos sob essa ótica.

5. **Interpretação Crítica dos Resultados**
   - Discussão sobre ruído, não estacionariedade e limites preditivos
   - Análise sobre onde a métrica de erro escolhida pode distorcer a leitura dos resultados

---

## 🛠️ Tecnologias Utilizadas

- **Python**
- **Pandas / NumPy**
- **yfinance** (obtenção dos dados)
- **Statsmodels** (decomposição sazonal, ACF/PACF, teste ADF)
- **StatsForecast** (Naive, SeasonalNaive, SeasonalWindowAverage, AutoARIMA)
- **Prophet**
- **Matplotlib / Seaborn / Plotly**
- **Jupyter Notebook**

---

## 🧠 Principais Aprendizados

- **Dados financeiros são altamente ruidosos e não estacionários**: a série em nível não passa no teste de estacionariedade (ADF), e só se torna estacionária após transformação (médias móveis, log-detrend ou diferenciação).
- **Métricas tradicionais nem sempre refletem valor preditivo real** — este projeto encontrou um exemplo concreto disso: o WMAPE das versões transformadas da série chega a ser dezenas de vezes maior que o da série em nível, não porque os modelos piorem nessa proporção, mas porque o WMAPE se torna instável quando os valores oscilam perto de zero (como acontece em séries detrendizadas). Comparar erro relativo entre representações de escalas tão diferentes pode levar a conclusões erradas se não for feito com cuidado.
- **Acurácia direcional (acertar alta ou baixa) ficou, na maioria dos testes, próxima de 50%** — em linha com o que se espera de um mercado eficiente de curto prazo, onde o preço já incorpora a informação disponível.
- **O uso de ML em mercado financeiro exige cautela e senso crítico**: um resultado numérico "bom" isoladamente não garante capacidade preditiva real.
- **Análise responsável é mais importante do que promessas de previsão.**

---

## ⚠️ Limitações

- O modelo não considera fatores externos (macroeconomia, notícias, eventos)
- Resultados são sensíveis ao período analisado
- A avaliação usa um único horizonte de ~30 pregões previstos de uma vez; uma validação *walk-forward* (previsão dia a dia, reajustando o modelo) daria uma leitura mais fiel da previsão de curtíssimo prazo
- Com apenas ~30 observações no teste, diferenças de poucos pontos percentuais de acurácia estão dentro da margem de erro
- O projeto não foi desenvolvido para uso operacional ou decisões reais
- Machine Learning é tratado como **ferramenta de análise**, não como solução definitiva

---

## 🚀 Como Executar

1. Clone o repositório:

```
git clone https://github.com/RenanCostaViana/ibovespa-ml-analysis.git
```

2. Instale as dependências:

```
pip install -r requirements.txt
```

3. Abra o notebook principal:

```
jupyter notebook ibovespa_ml_analysis.ipynb
```

4. Execute as células na ordem indicada

---

## 💬 Considerações Finais

Este projeto foi desenvolvido para demonstrar a aplicação consciente de técnicas de Data Analytics e Machine Learning em um domínio complexo, aliando conhecimento financeiro, capacidade analítica e interpretação crítica dos dados — incluindo o cuidado de questionar as próprias métricas de avaliação, não só os modelos.

## 📬 Contato

LinkedIn: <https://linkedin.com/in/renancostaviana>
E-mail: <renan.cv@outlook.com.br>

*✨ Projeto desenvolvido com foco em análise de dados aplicada ao mercado financeiro.*
