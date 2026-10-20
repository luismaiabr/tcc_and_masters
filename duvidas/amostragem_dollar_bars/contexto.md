# Contexto: Amostragem Informacional via Dollar Bars

[← Voltar ao Índice de Dúvidas](../README.md)

---

## 1. Gênese da Dúvida
Durante a leitura e revisão da [Seção 6.4.1 (Amostragem Baseada em Informação)](../../docs/tcc/01_sampling_informacional.md), foi solicitada a explicação aprofundada da expressão matemática que governa a geração de **Dollar Bars**:

$$\sum_{i=1}^T P_i Q_i \ge D \tag{(F10)}$$

A dúvida versa sobre a decomposição analítica dos termos, a lógica de parada estocástica e a justificativa pela qual a amostragem financeira supera as abordagens tradicionais cronológicas e de volume de contratos.

---

## 2. Inserção no Projeto qDATA e no TCC
No estado atual do qDATA (Seção 6.1 e 6.2 do TCC), o *feeder* `mt5bridge` ingere candles canônicos M1 (minuto a minuto) gerados pelo MetaTrader 5. 

Na **Seção 6.4 ("Trabalhos Futuros")**, projeta-se a substituição do relógio cronológico por um **motor de agregação orientado a eventos** operando sobre o fluxo contínuo `COPY_TICKS_ALL`. O entendimento das Dollar Bars é a pedra fundamental dessa evolução arquitetural, pois define o mecanismo primário de geração de barras sintéticas homogêneas em termos de volume financeiro transacionado.

---

## 3. Relevância para o Mestrado em Estatística (IME-USP / Exame da ABE)
A compreensão das Dollar Bars conecta-se diretamente com:
- **Processos Estocásticos Subordinados:** Mudança do relógio cronológico contínuo $t$ para um relógio operacional $\tau(t)$ dependente da chegada de informação de mercado (teoria de subordinação estocástica de Clark, 1973).
- **Teorema Central do Limite (TCL) e Propriedades Assintóticas:** Restauração da normalidade assintótica dos retornos logarítmicos e atenuação de curtose excessiva (leptocurtose), permitindo que modelos lineares, testes de hipóteses e estimações por Máxima Verossimilhança (MLE) operem sob premissas válidas.
