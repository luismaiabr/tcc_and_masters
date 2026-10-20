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

## 🗂️ Navegação Rápida (Hub Principal)

| Módulo | Documento | Descrição Executiva |
| :--- | :--- | :--- |
| **Contexto Estático** | [00. Estado Atual do qDATA](docs/tcc/00_estado_atual_qdata.md) | O que já está pronto (FastAPI, TimescaleDB, gRPC, Wine/MT5). |
| **TCC 6.4 (Trabalhos Futuros)** | [01. Amostragem Informacional](docs/tcc/01_sampling_informacional.md) | Dollar Bars e Imbalance Bars com restauração via TCL. |
| **TCC 6.4 (Trabalhos Futuros)** | [02. Livro de Ofertas e Feature Store](docs/tcc/02_reconstrucao_lob_feature_store.md) | Cálculo online de OFI, VPIN, Micro-Price e Roll Spread. |
| **TCC 6.4 (Trabalhos Futuros)** | [03. Inferência Estatística em Streaming](docs/tcc/03_inferencia_streaming_regime.md) | TRV/Wilks, Processos de Hawkes e filtragem por Marchenko-Pastur. |
| **TCC 6.4 (Trabalhos Futuros)** | [04. Baixa Latência e Replay Determinístico](docs/tcc/04_arquitetura_distribuida_replay.md) | Pipeline Hot/Cold e garantia de Point-in-Time Correctness. |
| **TCC 6.4 (Trabalhos Futuros)** | [05. Governança e Roteamento Dual-Stream](docs/tcc/05_governanca_regulatoria_dual_stream.md) | Watermark temporal para delay de 15 min (B3) e Zero Trust. |
| **Mestrado (MAE / IME-USP)** | [Cronograma ABE (16 Semanas)](docs/mestrado/cronograma_abe_16_semanas.md) | Roteiro de estudos em Probabilidade Avançada e Inferência. |
| **Mestrado (MAE / IME-USP)** | [Ponte Teoria $\leftrightarrow$ Engenharia](docs/mestrado/ponte_estatistica_engenharia.md) | Mapeamento explícito entre teoremas da prova e código do qDATA. |
| **Mestrado (MAE / IME-USP)** | [Esboço de Pré-Projeto](docs/mestrado/pre_projeto_pesquisa_esboco.md) | Proposta formal para abordagem a professores de Séries Temporais. |
| **Mercado Quant** | [Portfólio & Carreira Quant](docs/carreira/posicionamento_quant_portfolio.md) | Bullet points para CV e roteiro para entrevistas técnicas. |
| **Módulos Educacionais** | [Hub de Dúvidas](duvidas/README.md) | Aprofundamentos didáticos estruturados (contexto, lição, bibliografia). |
| **Referências Canônicas** | [Identidade Original](identidade.md) / [Plano de Estudos ABE](plano_para_mestrado.md) | Diretrizes originais e plano mestre de estudos. |

---

## 📂 Árvore de Diretórios Navegável

Clique diretamente em qualquer arquivo para acessá-lo no GitHub:

```text
tcc_and_masters/
├── .agents/
│   ├── [GEMINI.md](.agents/GEMINI.md)                                # Persona do Arquiteto Sênior Quant e regras gerais
│   └── rules/
│       ├── [quant_architecture.md](.agents/rules/quant_architecture.md) # Regras de arquitetura de baixa latência e streaming
│       ├── [academic_standards.md](.agents/rules/academic_standards.md) # Normas de rigor acadêmico, LaTeX/ABNT e IME-USP
│       └── [gestao_duvidas_educacionais.md](.agents/rules/gestao_duvidas_educacionais.md) # Diretiva de criação de lições sob demanda
│
├── docs/
│   ├── tcc/                                                          # Seção 6.4 do TCC: Trabalhos Futuros da Plataforma qDATA
│   │   ├── [00_estado_atual_qdata.md](docs/tcc/00_estado_atual_qdata.md)         # Marco estático do sistema construído no TCC
│   │   ├── [01_sampling_informacional.md](docs/tcc/01_sampling_informacional.md)     # Dollar Bars e Imbalance Bars (TCL)
│   │   ├── [02_reconstrucao_lob_feature_store.md](docs/tcc/02_reconstrucao_lob_feature_store.md) # Feature Store de Microestrutura (OFI, VPIN)
│   │   ├── [03_inferencia_streaming_regime.md](docs/tcc/03_inferencia_streaming_regime.md)    # TRV/Wilks, Hawkes e Marchenko-Pastur
│   │   ├── [04_arquitetura_distribuida_replay.md](docs/tcc/04_arquitetura_distribuida_replay.md) # Hot/Cold Path e Replay Determinístico
│   │   └── [05_governanca_regulatoria_dual_stream.md](docs/tcc/05_governanca_regulatoria_dual_stream.md) # Dual-Stream Routing (delay B3 15m)
│   │
│   ├── mestrado/                                                     # Rota de Ingresso e Pesquisa (MAE / IME-USP)
│   │   ├── [cronograma_abe_16_semanas.md](docs/mestrado/cronograma_abe_16_semanas.md) # Cronograma de 16 semanas para a ABE
│   │   ├── [ponte_estatistica_engenharia.md](docs/mestrado/ponte_estatistica_engenharia.md) # Correspondência: Teoria ABE <-> qDATA
│   │   └── [pre_projeto_pesquisa_esboco.md](docs/mestrado/pre_projeto_pesquisa_esboco.md)   # Esboço para contato com orientadores
│   │
│   └── carreira/                                                     # Posicionamento no Mercado Financeiro Quantitativo
│       └── [posicionamento_quant_portfolio.md](docs/carreira/posicionamento_quant_portfolio.md) # Bullets para CV e guia para entrevistas
│
├── duvidas/                                                          # Módulos educacionais gerados a partir de dúvidas
│   └── [README.md](duvidas/README.md)                                        # Estrutura e índice dos tópicos didáticos
│
├── [identidade.md](identidade.md)                                            # Registro de identidade original e diretrizes do consultor Tee
├── [plano_para_mestrado.md](plano_para_mestrado.md)                                   # Documento de referência estática do cronograma da ABE
└── [README.md](README.md)                                                # Este índice geral do projeto
```

---

## 🤖 Consultoria Automatizada ([.agents/](.agents/))
O diretório [`.agents/`](.agents/) configura o comportamento do agente **Tee** em qualquer sessão deste repositório, garantindo conformidade com:
- A regra de restrição sobre o escopo atual do TCC.
- A **Dupla Lente Obrigatória** (Engenharia de Software + Rigor Estatístico) em todas as propostas técnicas.
- As regras arquiteturais e acadêmicas especificadas em [`.agents/rules/`](.agents/rules/).