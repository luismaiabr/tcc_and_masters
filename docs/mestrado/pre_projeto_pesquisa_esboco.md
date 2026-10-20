[← Anterior: Ponte Teoria ↔ Engenharia](ponte_estatistica_engenharia.md) | [Índice Geral](../../README.md) | [Próximo: Portfólio & Carreira Quant →](../carreira/posicionamento_quant_portfolio.md)

---

# Esboço de Pré-Projeto de Mestrado (MAE / IME-USP)

**Título Provisório:**  
*Inferência Estocástica Sequencial e Modelagem de Microestrutura de Mercado em Alta Frequência sob Amostragem Orientada a Informação*

**Área de Concentração:**  
Estatística / Séries Temporais e Processos Estocásticos (MAE — Instituto de Matemática e Estatística da USP).

---

## 1. Contextualização e Problema de Pesquisa
A análise estatística de séries temporais de alta frequência nos mercados financeiros enfrenta desafios de heterocedasticidade, excesso de curtose e quebras estruturais frequentes. O método tradicional de discretização por tempo de relógio (ex: barras de 1 minuto) gera ruído em momentos de baixa atividade e perda de informação em picos de volatilidade.

Este projeto propõe investigar propriedades assintóticas de estimadores sob **amostragem orientada a informação** (Dollar Bars e Imbalance Bars), combinando modelos pontuais (Processos de Hawkes) com testes sequenciais de razão de verossimilhanças para detecção online de mudança de regime no mercado acionário e futuro brasileiro (B3).

---

## 2. Objetivos

### Objetivo Geral
Desenvolver e validar rigorosamente métodos estatísticos de inferência assintótica e algoritmos sequenciais de detecção de quebra de regime aplicados a dados de alta frequência amostrados no domínio da informação.

### Objetivos Específicos
1. Formalizar a distribuição assintótica dos retornos obtidos sob esquemas de parada orientados por volume financeiro e desequilíbrio de ordens.
2. Derivar as propriedades de consistência e eficiência assintótica de estimadores de Máxima Verossimilhança recursivos para parâmetros de processos auto-excitantes (Hawkes).
3. Avaliar empiricamente o poder de testes de quebra de regime baseados no Teorema de Wilks e CUSUM sobre a estrutura de microestrutura da B3.
4. Utilizar a infraestrutura de dados de mercado qDATA como bancada experimental reproduzível.

---

## 3. Metodologia Proposta
1. **Modelagem Matemática:** Derivação teórica sob a ótica de tempos de parada (*stopping times*), esperança condicional em filtragens estocásticas e teoremas limites.
2. **Estimação e Testes:** Implementação de estimadores de máxima verossimilhança e testes assintóticos (Wald, Escore e TRV).
3. **Validação Empírica:** Aplicação sobre o histórico consolidado de ticks de negócios e de livro de ofertas de contratos futuros (Mini-Índice WIN e Mini-Dólar WDO).

---

## 4. Referências Selecionadas
- BOLFARINE, H.; SANDOVAL, M. C. *Introdução à Inferência Estatística*. SBM, 2010.
- JAMES, B. R. *Probabilidade: Um Curso em Nível Intermediário*. IMPA, 2004.
- LÓPEZ DE PRADO, M. *Advances in Financial Machine Learning*. Wiley, 2018.
- CARTEA, Á.; JAIMUNGAL, S.; PENALVA, J. *Algorithmic and High-Frequency Trading*. Cambridge University Press, 2015.
- BACRY, E.; DELATTRE, S.; HOFFMANN, M.; MUZY, J. F. *Some properties of the Mutually Exciting Hawkes Processes with applications to financial data*. Stochastic Processes and their Applications, 2013.
