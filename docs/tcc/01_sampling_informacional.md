[← Anterior: 00. Estado Atual](00_estado_atual_qdata.md) | [Índice Geral](../../README.md) | [Próximo: 02. Livro de Ofertas e Feature Store →](02_reconstrucao_lob_feature_store.md)

---

# Seção 6.4.1: Amostragem Baseada em Informação (Information-Driven Bars)

## 1. Problema Conceitual e Limitações da Barra M1
A amostragem de dados orientada ao relógio cronológico (ex: barras OHLCV de 1 minuto) é o padrão de mercado de varejo, mas impõe severas distorções econométricas:
- **Heterocedasticidade Amostral:** Em períodos de alta volatilidade (ex: abertura de mercado, divulgação do Payroll), uma barra de 1 minuto condensa dezenas de milhares de transações; em períodos calmos, contém escassos negócios.
- **Ruptura de Propriedades Gaussianas:** Os retornos calculados em intervalos de tempo fixos exibem curtose excessiva (caudas pesadas), dependência não-linear e violação do pressuposto i.i.d.

---

## 2. Proposta Técnica: Motor de Agregação Orientado a Eventos
Projeta-se a evolução do núcleo de streaming do qDATA para processar os fluxos `COPY_TICKS_ALL` e construir dinamicamente barras de amostragem informacional:

1. **Tick Bars:** Cada barra é fechada após um número pré-definido fixo de negócios $N$.
2. **Volume Bars:** Cada barra é fechada quando o volume total negociado atinge um limiar $V$.
3. **Dollar Bars:** Amostragem disparada ao atingir um montante financeiro acumulado $\sum_{i=1}^T P_i Q_i \ge D$. Permite neutralizar distorções decorrentes da oscilação do nível de preço do ativo ao longo de meses ou anos.
4. **Imbalance Bars (Tick/Volume Imbalance):**
   - Baseiam-se na assinatura direcional de cada negócio $b_t \in \{-1, +1\}$ via algoritmo de tick (regra clássica de Lee-Ready):
   
   $$b_t = \begin{cases} +1, & \text{se } \Delta P_t > 0 \\ -1, & \text{se } \Delta P_t < 0 \\ b_{t-1}, & \text{se } \Delta P_t = 0 \end{cases}$$

   - Acumulam o desequilíbrio de fluxo $I_T = \sum_{t=1}^T b_t$. Uma barra fecha quando o desequilíbrio acumulado excede a sua esperança condicional:
   
   $$\left| \sum_{t=1}^T b_t \right| \ge \mathbb{E}[T] \cdot \left| 2\mathbb{P}(b_t = 1) - 1 \right|$$

---

## 3. Avaliação pela Dupla Lente

### Lente de Engenharia de Software
- **Desafio:** Implementação de agregador *stateful* em memória com altíssima vazão (centenas de milhares de ticks por segundo no WIN), garantindo tolerância a falhas, reconciliação de estado e baixa latência sem alocações desnecessárias (zero-allocation ring buffers).
- **Protocolo:** Disseminação das barras customizadas para múltiplos clientes via gRPC server-streaming.

### Lente Quantitativa e Estatística (Conexão IME-USP / ABE)
- **Fundamentação:** Restauração das propriedades do **Teorema Central do Limite (TCL)** e da convergência assintótica dos retornos. A amostragem em tempo de fluxo de negócios (*business time* / *information clock*) recupera propriedades i.i.d. e aproxima a distribuição dos retornos da Normal, facilitando estimação por Máxima Verossimilhança (MLE) e modelagem de volatilidade.

### Pitch de Mercado (2 Linhas)
> *"Projetei um motor de amostragem estatística em streaming que processa ticks de alta frequência e sintetiza Dollar e Imbalance Bars em tempo real, restaurando a normalidade assintótica dos retornos para modelos quantitativos."*
