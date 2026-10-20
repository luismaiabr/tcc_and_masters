# Lição: Fundamentos e Implementação de Dollar Bars

[← Voltar ao Contexto](contexto.md) | [Índice de Dúvidas](../README.md)

---

## 1. O Problema Fundamental da Amostragem Cronológica (Time Bars)

A grande maioria dos sistemas quantitativos de varejo e plataformas de análise técnica amostra séries temporais com base em intervalos arbitrários do relógio astronômico: barras de 1 minuto (M1), 5 minutos (M5), diárias (D1).

Do ponto de vista econométrico e de microestrutura de mercado, **o tempo cronológico é homogêneo, mas a taxa de chegada de informação no mercado é heterogênea e altamente irregular**.

Considere as duas situações no contrato futuro de mini-índice (WIN):
1. **Período de Abertura ou Divulgação de Notícia (ex: Payroll / Copom):** Em 60 segundos, ocorrem 50.000 negócios com movimentação de bilhões de reais. Uma barra M1 condensa uma massa gigantesca de transações em apenas um resumo OHLCV.
2. **Período de Baixa Liquidez (ex: Intervalo de Almoço):** Em 60 segundos, ocorrem 15 negócios dispersos com volume residual. A barra M1 atribui a mesma importância analítica (1 observação) a um intervalo quase desprovido de fluxo informativo.

### Consequências Estatísticas Indesejadas das Time Bars:
- **Heterocedasticidade Amostral Extrema:** A variância dos retornos calculados em barras de tempo fixo oscila violentamente dependendo da hora do dia.
- **Leptocurtose e Não-Normalidade:** Caudas excessivamente pesadas que violam a hipótese de distribuição normal ou i.i.d., invalidando grande parte do ferramental estatístico clássico (testes $t$, modelos autorregressivos padrão, estimações assintóticas).

---

## 2. A Hierarquia das Barras Informacionais

Para resolver esse problema, a literatura quantitativa (notadamente Marcos López de Prado, 2018) propõe estruturar os dados com base no **fluxo de informação**:

1. **Tick Bars:** Amostragem disparada após cada $N$ transações (contagem simples de negócios).
2. **Volume Bars:** Amostragem disparada ao acumular $V$ contratos transacionados ($\sum Q_i \ge V$).
3. **Dollar Bars:** Amostragem disparada ao acumular um montante financeiro total $D$.

### Por que Dollar Bars superam Volume Bars?
Se uma ação custa R$ 20,00 e valoriza até R$ 80,00 ao longo de dois anos, cada lote de 1.000 ações passa a movimentar 4 vezes mais capital. Uma *Volume Bar* fixa de 100.000 ações amostrará 4 vezes mais valor econômico no segundo período, distorcendo comparações históricas. 

As **Dollar Bars** neutralizam essa distorção: cada barra representa exatamente a mesma cota de valor econômico trocado entre compradores e vendedores.

---

## 3. Formalização Matemática das Dollar Bars

Seja uma sequência discreta de negócios ordenados no tempo $i = 1, 2, \dots$, onde cada negócio é caracterizado pelo par:
- $P_i$: Preço unitário de execução do negócio $i$.
- $Q_i$: Quantidade de contratos/ações negociados na transação $i$.

O valor financeiro (notional) movimentado exclusivamente pelo negócio $i$ é dado pelo produto $P_i Q_i$.

A condição de amostragem que determina o encerramento da barra é:

$$\sum_{i=1}^T P_i Q_i \ge D \tag{(F10)}$$

Onde $D$ é o limiar financeiro estipulado e $T$ é o **tempo de parada estocástico (*stopping time*)**:

$$\tau = \inf \left\{ T \ge 1 : \sum_{i=1}^T P_i Q_i \ge D \right\} \tag{(F11)}$$

No instante do tick $T = \tau$:
1. A barra atual é selada com as métricas calculadas sobre os negócios $i \in \{1, \dots, \tau\}$:
   - **Open ($O$):** $P_1$
   - **High ($H$):** $\max_{1 \le i \le \tau} P_i$
   - **Low ($L$):** $\min_{1 \le i \le \tau} P_i$
   - **Close ($C$):** $P_\tau$
   - **Volume de Contratos ($V$):** $\sum_{i=1}^\tau Q_i$
   - **Preço Médio Ponderado por Volume ($VWAP_\tau$):**

   $$VWAP_\tau = \frac{\sum_{i=1}^\tau P_i Q_i}{\sum_{i=1}^\tau Q_i} \tag{(F12)}$$

2. O acumulador financeiro é reiniciado (ou o excedente $\sum_{i=1}^\tau P_i Q_i - D$ é propagado como resíduo inicial para o primeiro tick da barra seguinte).
3. Uma nova barra se inicia imediatamente a partir do negócio $\tau + 1$.

---

## 4. Conexão Teórica: Processos Subordinados e Teorema Central do Limite (IME-USP)

A fundamentação probabilística rigorosa para a superioridade das Dollar Bars repousa na teoria dos **Processos Estocásticos Subordinados** (Clark, 1973):

Seja $P(t)$ o preço do ativo em tempo cronológico contínuo. Considera-se que $P(t) = X(\theta(t))$, onde:
- $X(\tau)$ é um processo estocástico regido por um relógio operacional $\tau$ (o fluxo de volume financeiro).
- $\theta(t)$ é um processo estocástico não-decrescente que mede a quantidade de transações/capital decorridos até o tempo $t$.

Quando a amostragem é realizada diretamente no relógio informacional $\tau$ (intervalos regulares de volume financeiro $D$), o retorno logarítmico entre barras consecutivas:

$$r_\tau = \ln \left( \frac{P_\tau}{P_{\tau-1}} \right) \tag{(F13)}$$

converge assintoticamente para uma variável aleatória normalmente distribuída pelo Teorema Central do Limite (TCL). 

Isso ocorre porque cada incremento de retorno $r_\tau$ passa a ser uma soma de choques elementares com variância homogênea por unidade de informação, eliminando a leptocurtose induzida pelo tempo astronômico.

---

## 5. Implementação de Baixa Latência em Streaming (Engenharia de Software)

Na arquitetura do qDATA, essa lógica não é executada em lote (*batch*) sobre arquivos estáticos, mas sim de forma **reativa em streaming** consumindo o canal `COPY_TICKS_ALL`.

### Algoritmo de Agregação em Tempo Real ($O(1)$ por tick)

```python
from dataclasses import dataclass
from typing import Optional

@dataclass
class Tick:
    timestamp_ns: int
    price: float
    quantity: int

@dataclass
class DollarBar:
    open_time: int
    close_time: int
    open: float
    high: float
    low: float
    close: float
    volume: int
    dollar_volume: float
    ticks_count: int
    vwap: float

class DollarBarAggregator:
    def __init__(self, threshold_dollar: float):
        self.threshold = threshold_dollar
        self.reset_state()

    def reset_state(self):
        self.cum_dollar = 0.0
        self.cum_volume = 0
        self.ticks_count = 0
        self.open = None
        self.high = -float("inf")
        self.low = float("inf")
        self.open_time = None

    def on_tick(self, tick: Tick) -> Optional[DollarBar]:
        """Processa um tick em O(1) de tempo e espaço."""
        tick_dollar = tick.price * tick.quantity

        if self.ticks_count == 0:
            self.open = tick.price
            self.open_time = tick.timestamp_ns

        self.high = max(self.high, tick.price)
        self.low = min(self.low, tick.price)
        self.cum_dollar += tick_dollar
        self.cum_volume += tick.quantity
        self.ticks_count += 1

        # Verificação do limiar estocástico de parada (F10)
        if self.cum_dollar >= self.threshold:
            bar = DollarBar(
                open_time=self.open_time,
                close_time=tick.timestamp_ns,
                open=self.open,
                high=self.high,
                low=self.low,
                close=tick.price,
                volume=self.cum_volume,
                dollar_volume=self.cum_dollar,
                ticks_count=self.ticks_count,
                vwap=self.cum_dollar / self.cum_volume if self.cum_volume > 0 else tick.price
            )
            self.reset_state()
            return bar

        return None
```

### Considerações Críticas de Engenharia de Produção:
1. **Evitar Erros de Ponto Flutuante:** Para cálculo financeiro contínuo em C++ ou Rust, recomenda-se representar o financeiro acumulado como um inteiro em centavos (`int64_t`) para prevenir deriva por arredondamento de float.
2. **Buffer Circular Zero-Allocation:** O emissor deve reutilizar estruturas de memória pré-alocadas (*ring buffers*) para empacotar o payload Protobuf e transmiti-lo via gRPC sem causar pausas de *garbage collection*.
3. **Reconciliação e Tolerância a Falhas:** Em caso de perda de conexão com o `mt5bridge`, o agregador deve ser capaz de reconstruir o estado parcial a partir da persistência em hypertables do TimescaleDB.

---

## 6. Takeaways Centrais

1. **Amostragem orientada a informação** substitui o relógio astronômico pelo relógio econômico.
2. A fórmula $\sum_{i=1}^T P_i Q_i \ge D$ define o momento exato em que um *quantum* homogêneo de liquidez foi absorvido pelo mercado.
3. As **Dollar Bars** estabilizam a variância e restabelecem a normalidade assintótica dos retornos logarítmicos, tornando os modelos quantitativos mais robustos contra regimes de caudas pesadas.
