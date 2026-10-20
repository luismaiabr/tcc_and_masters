# Planejamento Estratégico: TCC qDATA & Mestrado em Estatística (MAE / IME-USP)

Repositório central de planejamento acadêmico, estruturação de propostas de evolução tecnológica (Seção 6.4 do TCC — "Trabalhos Futuros") e preparação para a transição ao **Mestrado em Estatística no IME-USP** via Exame da ABE, com foco em Engenharia Quantitativa e Microestrutura de Mercado.

---

## 🧭 Princípio Fundamental (Regra de Ouro)
> **O escopo já implementado no TCC (a plataforma qDATA em seu estado atual) permanece CONGELADO e INALTERADO.**
> Todas as análises, arquiteturas e propostas desenvolvidas neste repositório dedicam-se exclusivamente a:
> 1. Redação e fundamentação da **Seção 6.4 ("Trabalhos Futuros")** do TCC.
> 2. Estruturação do **pré-projeto de pesquisa para o MAE / IME-USP**.
> 3. Construção de um **portfólio de engenharia de dados e finanças quantitativas de elite**.

---

## 📂 Mapa Modular do Repositório

```
tcc_and_masters/
├── .agents/                                # Configuração e inteligência do assistente (Tee)
│   ├── GEMINI.md                           # Persona do Arquiteto Sênior Quant e regras gerais
│   └── rules/                              # Diretrizes especializadas
│       ├── quant_architecture.md           # Regras de arquitetura de baixa latência e streaming
│       └── academic_standards.md           # Normas de rigor acadêmico, LaTeX/ABNT e IME-USP
│
├── docs/
│   ├── tcc/                                # Seção 6.4 do TCC: Trabalhos Futuros da Plataforma qDATA
│   │   ├── 00_estado_atual_qdata.md        # Marco estático do sistema construído no TCC
│   │   ├── 01_sampling_informacional.md    # Information-Driven Bars (Tick, Volume, Dollar, Imbalance)
│   │   ├── 02_reconstrucao_lob_feature_store.md # Reconstrução de Livro L2 e Feature Store (OFI, VPIN)
│   │   ├── 03_inferencia_streaming_regime.md # Inferência online, TRV/Wilks, Hawkes e Marchenko-Pastur
│   │   ├── 04_arquitetura_distribuida_replay.md # Hot/Cold Path e Replay Determinístico Point-in-Time
│   │   └── 05_governanca_regulatoria_dual_stream.md # Dual-stream routing e delay regulatório B3 (15 min)
│   │
│   ├── mestrado/                           # Rota de Ingresso e Pesquisa (MAE / IME-USP)
│   │   ├── cronograma_abe_16_semanas.md    # Cronograma operacional de 16 semanas para o Exame da ABE
│   │   ├── ponte_estatistica_engenharia.md # Correspondência direta entre teoria ABE e código do qDATA
│   │   └── pre_projeto_pesquisa_esboco.md  # Esboço do pré-projeto para abordagem a orientadores
│   │
│   └── carreira/                           # Posicionamento no Mercado Financeiro Quantitativo
│       └── posicionamento_quant_portfolio.md # Bullets para CV e guia para entrevistas de Quant Dev/Research
│
├── identidade.md                           # Registro de identidade original e diretrizes do consultor Tee
├── plano_para_mestrado.md                  # Documento de referência estática do cronograma da ABE
└── README.md                               # Este índice geral do projeto
```

---

## 🔗 Acesso Rápido aos Documentos

### 1. Evolução do TCC (Trabalhos Futuros — Seção 6.4)
- [00. Estado Atual do qDATA](file:///docs/tcc/00_estado_atual_qdata.md): O que já está concluído (FastAPI, TimescaleDB, gRPC, Wine/MT5).
- [01. Amostragem Informacional](file:///docs/tcc/01_sampling_informacional.md): Substituição da barra M1 por Dollar e Imbalance Bars.
- [02. Livro de Ofertas e Feature Store](file:///docs/tcc/02_reconstrucao_lob_feature_store.md): Cálculo em tempo real de OFI, VPIN, Micro-Price e Roll Spread.
- [03. Inferência Estatística em Streaming](file:///docs/tcc/03_inferencia_streaming_regime.md): Detecção de quebras com TRV, processos de Hawkes e matrizes limpas por Marchenko-Pastur.
- [04. Baixa Latência e Replay Determinístico](file:///docs/tcc/04_arquitetura_distribuida_replay.md): Desacoplamento Hot/Cold Path e garantia de Point-in-Time Correctness.
- [05. Governança e Roteamento Dual-Stream](file:///docs/tcc/05_governanca_regulatoria_dual_stream.md): Watermark temporal para delay de 15 minutos (B3) e Zero Trust.

### 2. Mestrado em Estatística (MAE / IME-USP)
- [Cronograma ABE (16 Semanas)](file:///docs/mestrado/cronograma_abe_16_semanas.md): Planejamento detalhado em Probabilidade Avançada e Inferência Estatística.
- [Ponte Teoria $\leftrightarrow$ Engenharia](file:///docs/mestrado/ponte_estatistica_engenharia.md): Como cada teorema da prova se aplica no desenvolvimento de sistemas quantitativos.
- [Esboço de Pré-Projeto](file:///docs/mestrado/pre_projeto_pesquisa_esboco.md): Proposta de pesquisa formal para contato com orientadores de Séries Temporais.

### 3. Posicionamento Profissional
- [Portfólio & Carreira Quant](file:///docs/carreira/posicionamento_quant_portfolio.md): Bullet points prontos para currículo e respostas para entrevistas técnicas de Quant Developer e Quant Researcher.

---

## 🤖 Consultoria Automatizada (.agents)
O diretório [`.agents/`](file:///./.agents/) configura o comportamento do agente **Tee** em qualquer sessão deste repositório, garantindo conformidade com:
- A regra de restrição sobre o escopo atual do TCC.
- A **Dupla Lente Obrigatória** (Engenharia de Software + Rigor Estatístico) em todas as propostas técnicas.
- As regras arquiteturais e acadêmicas especificadas em [`.agents/rules/`](file:///./.agents/rules/).