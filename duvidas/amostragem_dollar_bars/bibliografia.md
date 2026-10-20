# Bibliografia: Amostragem Informacional e Dollar Bars

[← Voltar à Lição](licao.md) | [Índice de Dúvidas](../README.md)

---

## 1. Obras Fundamentais de Finanças Quantitativas e Machine Learning

* **LÓPEZ DE PRADO, Marcos.** *Advances in Financial Machine Learning*. Hoboken: John Wiley & Sons, 2018.
  - **Capítulo 2: Financial Data Structures**
    - *Seção 2.3.1:* Standard Bars (Time, Tick, Volume, Dollar Bars) — dedicação especial às páginas 25–31, onde o autor demonstra por que Dollar Bars recuperam propriedades estatísticas superiores.
    - *Seção 2.3.2:* Information-Driven Bars (Tick/Volume Imbalance e Runs Bars).
  - **Capítulo 3: Labeling** — impacto da amostragem correta na rotulagem pelo método *Triple Barrier*.

* **LÓPEZ DE PRADO, Marcos.** *Machine Learning for Asset Managers*. Cambridge University Press, 2020.
  - **Capítulo 2: Denoising and Detrending** — propriedades espectrais e ruído em matrizes de covariância sob diferentes regimes de amostragem.

---

## 2. Artigos Acadêmicos Seminais (Processos Estocásticos e Subordinação)

* **CLARK, Peter K.** "A Subordinated Stochastic Process Model with Finite Variance for Speculative Prices". *Econometrica*, v. 41, n. 1, p. 135–155, 1973.
  - *Importância:* Artigo pioneiro que estabeleceu a teoria dos processos subordinados em finanças, demonstrando formalmente que os preços dos ativos evoluem segundo um relógio informacional e não cronológico.

* **ANE, Thierry; GEMAN, Hélyette.** "Order Flow, Transaction Clock, and Normality of Asset Returns". *The Journal of Finance*, v. 55, n. 5, p. 2259–2284, 2000.
  - *Importância:* Prova empírica de que a transição para um relógio baseado no número de transações e volume financeiro recupera a normalidade dos retornos diários e intradiários.

* **EASLEY, David; LÓPEZ DE PRADO, Marcos M.; O'HARA, Maureen.** "Flow Toxicity and Liquidity in a High-Frequency World". *The Review of Financial Studies*, v. 25, n. 5, p. 1457–1493, 2012.
  - *Importância:* Base teórica para métricas de microestrutura (VPIN) que dependem de barras de volume e financeiro com amostragem informacional.

---

## 3. Microestrutura de Mercado e Séries Temporais (IME-USP / ABE)

* **HASBROUCK, Joel.** *Empirical Market Microstructure: The Institutions, the Economics, and the Econometrics of Securities Trading*. Oxford: Oxford University Press, 2007.
  - **Capítulo 3:** *Trading Mechanisms and Trade Reporting* — fluxo de ticks e microestrutura de livros de ofertas.
  - **Capítulo 4:** *Order Flow and the Bid-Ask Spread* — impacto do fluxo de ordens na formação dos retornos.

* **TSAY, Ruey S.** *Analysis of Financial Time Series*. 3. ed. Hoboken: John Wiley & Sons, 2010.
  - **Capítulo 5:** *High-Frequency Data Analysis and Market Microstructure* — modelagem de intervalos de tempo não-estacionários e processos pontuais.

---

## 4. Recursos Técnicos e Engenharia Quantitativa de Mercado

* **HUDSON & THAMES.** *Research on Financial Data Structures: Why Time Bars are Inferior*. Quantitative Research Insights, 2020. Disponível em: `https://hudsonthames.org/`
* **MLFINLAB Documentation.** *Standard Data Structures (Dollar Bars Module)*.
