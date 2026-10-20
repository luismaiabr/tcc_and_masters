# REGRAS DE ARQUITETURA QUANTITATIVA (LOW-LATENCY & STREAMING)

Ao planejar ou projetar arquiteturas para a evolução do qDATA e projetos futuros de engenharia quantitativa, obedeça aos seguintes padrões:

## 1. Amostragem Orientada a Informação (Information-Driven Sampling)
- Evitar fixação cega em barras baseadas em tempo (Time Bars M1).
- Priorizar motores de agregação em memória sobre streams de ticks (`COPY_TICKS_ALL`, `COPY_TICKS_INFO`):
  - **Tick Bars:** Amostragem por frequência fixa de transações.
  - **Volume Bars:** Agregação por volume negociado.
  - **Dollar Bars:** Agregação por volume financeiro ($P \times Q$).
  - **Imbalance Bars:** Acúmulo de desequilíbrio de ticks ou volume para capturar fluxo informado.
- Fundamentação: Recuperação de propriedades gaussianas e restauração assintótica via Teorema Central do Limite (TCL).

## 2. Reconstrução de Livro de Ofertas e Feature Store em Tempo Real
- Consumo de eventos de livro Nível 1 e Nível 2.
- Cálculo de métricas de microestrutura:
  - **Order Flow Imbalance (OFI)**
  - **Volume-Synchronized Probability of Informed Trading (VPIN)**
  - **Micro-price** ponderado pelo book
  - **Roll Spread** (medida implícita de custos de transação)

## 3. Inferência Estocástica e Mudança de Regime em Streaming
- Conexão nativa do stream gRPC com algoritmos sequenciais:
  - **Testes da Razão de Verossimilhança (TRV / Wilks)** sequenciais, CUSUM ou Page-Hinkley para quebras estruturais.
  - Estimação recursiva de Máxima Verossimilhança (MLE) para processos pontuais de Hawkes (auto-excitantes) e modelos GARCH / Volatilidade Estocástica.
  - Matrizes de covariância limpas via Teoria de Matrizes Aleatórias (Lei de Marchenko-Pastur e Decomposição Espectral).

## 4. Engenharia de Alta Confiabilidade
- **Hot Path vs. Cold Path:**
  - *Hot Path:* Caminho em memória de baixa latência (Zero-Copy, Ring Buffers, Arrow Flight ou gRPC interno).
  - *Cold Path:* Caminho de persistência e auditoria analítica (TimescaleDB Hypertables com Continuous Aggregates e compressão colunar).
- **Market Replay Determinístico:** Reprodução ponto-a-ponto com garantia de *Point-in-Time Correctness* para eliminar *look-ahead bias*.
- **Watermark-based Dual-Stream Routing:** Módulo de roteamento regulatório que entrega ticks em tempo real via malha Zero-Trust (Tailscale) para instâncias autorizadas e aplica delay determinístico de 15 minutos em nível de buffer para consumidores educacionais e conformidade B3.
