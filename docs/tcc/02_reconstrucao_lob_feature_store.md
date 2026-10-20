[← Anterior: 01. Amostragem Informacional](01_sampling_informacional.md) | [Índice Geral](../../README.md) | [Próximo: 03. Inferência Estatística em Streaming →](03_inferencia_streaming_regime.md)

---

# Seção 6.4.2: Reconstrução do Livro de Ofertas e Feature Store de Microestrutura

## 1. Do Dado Bruto às Características de Microestrutura
Além de armazenar cotações brutas, a evolução do qDATA propõe uma camada de processamento de eventos do Livro de Ofertas (*Limit Order Book* - LOB) de Nível 1 e Nível 2 (`COPY_TICKS_INFO`), operando como uma **Feature Store Quantitativa em Tempo Real**.

---

## 2. Métricas Computadas em Streaming

### 2.1. Order Flow Imbalance (OFI)
Mede o desequilíbrio líquido do fluxo de ordens nos melhores níveis de compra (*bid*) e venda (*ask*):
$$OFI_t = \mathbb{I}_{\{P^b_t \ge P^b_{t-1}\}} q^b_t - \mathbb{I}_{\{P^b_t \le P^b_{t-1}\}} q^b_{t-1} - \left( \mathbb{I}_{\{P^a_t \le P^a_{t-1}\}} q^a_t - \mathbb{I}_{\{P^a_t \ge P^a_{t-1}\}} q^a_{t-1} \right)$$
Onde $q^b, q^a$ são quantidades e $P^b, P^a$ são preços do melhor bid e ask. O OFI tem forte poder preditivo sobre variações de preço no curto prazo.

### 2.2. VPIN (Volume-Synchronized Probability of Informed Trading)
Cálculo da probabilidade de negociação informada em janelas baseadas em volume (*volume buckets*):
$$VPIN = \frac{\sum_{\tau=1}^N |V_\tau^B - V_\tau^S|}{N \cdot V}$$
Onde $V$ é o tamanho do balde de volume e $V_\tau^B, V_\tau^S$ são os volumes compradores e vendedores estimados dentro do balde $\tau$.

### 2.3. Micro-Price Ponderado
Substitui o mid-price aritmético por uma métrica que reflete a pressão de liquidez nas pontas:
$$P_t^{\text{micro}} = \frac{q_t^b P_t^a + q_t^a P_t^b}{q_t^b + q_t^a}$$

### 2.4. Roll Spread (Medida Implícita de Custos)
Estimador do bid-ask spread efetivo derivado da covariância serial dos retornos observados:
$$S = 2 \sqrt{-\operatorname{Cov}(\Delta P_t, \Delta P_{t-1})}$$

---

## 3. Avaliação pela Dupla Lente

### Lente de Engenharia de Software
- **Desafio:** Reconstruir o estado local do book de ofertas com consistência estrita (*sequence numbers*), tratando mensagens fora de ordem e calculando métricas em tempo constante $O(1)$ por atualização de tick/nível.
- **Armazenamento:** Persistência em buffers circulares de memória compartilhada para consumo com latência sub-milissegundo via gRPC/IPC.

### Lente Quantitativa e Estatística (Conexão IME-USP / ABE)
- **Fundamentação:** Uso de covariâncias seriais, momentos conjuntos de vetores aleatórios bidimensionais $(P_t, Q_t)$ e estimação não-paramétrica de probabilidade de fluxo informado. Permite estudar modelos de impacto de mercado e predição condicional $\mathbb{E}[\Delta P_{t+\Delta t} \mid \text{LOB}_t]$.

### Pitch de Mercado (2 Linhas)
> *"Desenvolvi uma Feature Store de microestrutura que consome dados de book L2 e extrai em streaming métricas preditivas de fluxo de ordens (OFI, VPIN e Micro-price) com latência sub-milissegundo."*
