# Seção 6.4.3: Motor de Inferência Estatística e Mudança de Regime em Streaming

## 1. Do Monitoramento Reativo à Inferência Sequencial
A infraestrutura do qDATA pode integrar modelos de inferência estatística executados diretamente sobre o barramento de streaming gRPC, identificando transições de regime de mercado em tempo real.

---

## 2. Modelos e Mecanismos Propostos

### 2.1. Detecção Sequencial de Quebras Estruturais (TRV e CUSUM)
- **Teste da Razão de Verossimilhanças Sequencial (SPRT / TRV):** Avaliação contínua de hipóteses sobre parâmetros de volatilidade ou drift:
  $$\Lambda_t = \sum_{i=1}^t \ln \frac{f(x_i \mid \theta_1)}{f(x_i \mid \theta_0)}$$
- **Teorema de Wilks e CUSUM:** Detecção de desvios significativos na média ou variância através de estatísticas acumuladas com convergência assintótica governada por distribuições qui-quadrado ($\chi^2$).

### 2.2. Estimação Recursiva por Máxima Verossimilhança (MLE)
- **Processos de Hawkes (Auto-excitantes):** Modelagem de chegadas de ordens e agrupamento de volatilidade (*volatility clustering*):
  $$\lambda(t) = \mu + \sum_{t_i < t} \alpha e^{-\beta(t - t_i)}$$
  Estimação recursiva dos parâmetros $(\mu, \alpha, \beta)$ via algoritmos online de gradiente sobre a superfície de log-verossimilhança.
- **Volatilidade Condicional Recursiva:** Atualização contínua de modelos da família GARCH baseados na informação passada filtrada: $\sigma_t^2 = \mathbb{E}[r_t^2 \mid \mathcal{F}_{t-1}]$.

### 2.3. Limpeza de Ruído em Matrizes de Covariância (Teoria de Matrizes Aleatórias)
- Em carteiras multivariadas com $N$ ativos e $T$ observações onde $N/T \to c \in (0,1)$, a matriz de covariância empírica contém autovalores puramente espúrios governados pela **Lei de Marchenko-Pastur**:
  $$\lambda_{\pm} = \sigma^2 (1 \pm \sqrt{c})^2$$
- Aplicação de decomposição espectral no qDATA para filtrar autovalores dentro da densidade nula e reconstruir uma matriz de covariância estável para modelos de alocação de risco.

---

## 3. Avaliação pela Dupla Lente

### Lente de Engenharia de Software
- **Desafio:** Implementação de algoritmos numéricos vetorizados e otimização de gradiente em streaming, mantendo consumo estável de CPU e memória sem interromper a vazão do barramento de dados gRPC.

### Lente Quantitativa e Estatística (Conexão IME-USP / ABE)
- **Fundamentação:** Aplicação direta de Álgebra Linear avançada (decomposição espectral), Teoria de Verossimilhança (MLE, Matriz de Informação de Fisher, Lema de Neyman-Pearson e TRV) e propriedades assintóticas dos estimadores.

### Pitch de Mercado (2 Linhas)
> *"Projetei um motor estatístico online integrado ao barramento de streaming que aplica Testes de Razão de Verossimilhança e Teoria de Matrizes Aleatórias para detecção de quebra de regime e filtragem de ruído de covariância em tempo real."*
