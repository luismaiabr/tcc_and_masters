[← Anterior: Cronograma ABE](cronograma_abe_16_semanas.md) | [Índice Geral](../../README.md) | [Próximo: Esboço de Pré-Projeto →](pre_projeto_pesquisa_esboco.md)

---

# A Ponte Estatística-Engenharia: Teoria ABE vs. Sistemas Quantitativos

Este documento detalha como cada conceito matemático estudado para o Exame da ABE e para o MAE / IME-USP é instanciado na prática dentro de uma arquitetura quantitativa como o qDATA.

---

## Tabela de Correspondência Teoria $\leftrightarrow$ Engenharia

| Tópico da ABE (Teoria Estatística) | Aplicação Concreta em Finanças Quantitativas | Implementação no qDATA (Trabalhos Futuros) |
| :--- | :--- | :--- |
| **$\sigma$-Álgebras e Filtragens ($\mathcal{F}_t$)** | Modelagem da informação disponível no mercado até o instante $t$. | **Replay Determinístico:** Garantia de que a engine de backtest não consome ticks com timestamp futuro (*no look-ahead bias*). |
| **Esperança Condicional $\mathbb{E}[X \mid \mathcal{F}_t]$** | Previsão de preços futuros, retorno condicional e precificação de ativos sob expectativas iteradas. | **Modelos de Volatilidade e Retorno:** Avaliação da expectativa condicional de retornos dada a microestrutura do book. |
| **Teorema Central do Limite (TCL)** | Agregação de variáveis aleatórias com restauração de propriedades gaussianas assintóticas. | **Dollar e Imbalance Bars:** Amostragem por volume financeiro ou desequilíbrio que restaura a normalidade dos retornos. |
| **Covariância e Matrizes Positivas Definidas** | Gestão de risco de portfólio, modelo de Markowitz e cálculo de correlações multivariadas. | **Decomposição Espectral / Marchenko-Pastur:** Filtragem de ruído empírico em matrizes de covariância de alta dimensão. |
| **Suficiência e Teorema de Fisher-Neyman** | Compressão de dados sem perda de informação estatística sobre os parâmetros subjacentes. | **Barras e Microestrutura:** Extração de estatísticas suficientes a partir de milhões de ticks de L2. |
| **Cota Inferior de Cramér-Rao (CRLB)** | Limite fundamental da precisão com que parâmetros de mercado podem ser estimados. | **Benchmark de Estimadores:** Avaliação de se estimadores online de volatilidade atingem variância mínima. |
| **Máxima Verossimilhança (MLE)** | Calibração de processos de difusão, saltos e modelos de séries temporais (GARCH, Hawkes). | **Estimação Recursiva em Streaming:** Algoritmos online de calibração de parâmetros sobre o stream gRPC. |
| **Teste da Razão de Verossimilhanças (TRV)** | Teste ótimo de hipóteses simples e compostas sobre parâmetros de mercado. | **Detecção de Quebra de Regime:** Monitoramento de mudanças bruscas de volatilidade ou drift em tempo real. |
| **Teorema de Wilks ($\chi^2$ Assintótico)** | Distribuição nula do log da razão de verossimilhança sob hipóteses compostas. | **Calibração de Limiares em CUSUM:** Definição de níveis de alarme estatisticamente calibrados para parada de estratégias. |

---

## Conexão Estratégica para o Contato com Orientadores do IME-USP
Ao redigir o contato para professores do IME-USP (ex: área de Séries Temporais e Processos Estocásticos), o candidato não deve se apresentar apenas como "um programador que quer fazer mestrado", mas sim como:
> *"Um pesquisador que desenvolveu uma plataforma capaz de processar dados reais da B3 em alta frequência e que busca no MAE o rigor teórico para formalizar propriedades assintóticas e novos estimadores de microestrutura sobre dados amostrados por eventos."*
