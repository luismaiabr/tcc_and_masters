# Posicionamento de Mercado & Portfólio Quant

Este documento define a estratégia de apresentação do perfil profissional e do projeto qDATA para processos seletivos de elite em fundos quantitativos, assets sistemáticas e bancos de investimento (ex: Itaú Quant, BTG Pactual, Giant Steps, BW Gestão, Quantitas, etc.).

---

## 1. O Perfil Híbrido de Alto Valor
O mercado financeiro quantitativo busca profissionais capazes de cruzar duas fronteiras raras:
1. **Engenharia de Software de Baixa Latência:** Domínio de protocolos binários (gRPC/Protobuf), concorrência, otimização de memória e arquiteturas distribuídas.
2. **Rigor Matemático e Estatístico:** Conhecimento de probabilidade avançada, inferência assintótica, teoria da informação e séries temporais.

---

## 2. Bullet Points Prontos para o Currículo (CV)

### Opção 1 — Foco em Engenharia Quantitativa / Low-Latency (Quant Dev)
- *Projetou e implementou a plataforma qDATA, uma infraestrutura de Market Data em contêineres Linux para captura e distribuição de dados de alta frequência da B3, alcançando redução de 50% na latência e o dobro de vazão via gRPC server-streaming.*
- *Desenvolveu pipeline híbrido com desacoplamento Hot/Cold Path e motor de agregação em memória para cálculo em streaming de Dollar Bars e métricas de microestrutura (OFI, VPIN, Micro-price).*
- *Estruturou arquitetura Zero Trust (Tailscale) com roteamento dual-stream baseado em marcas d'água temporais, atendendo integralmente às diretrizes regulatórias de Market Data com delay de 15 minutos.*

### Opção 2 — Foco em Pesquisa Quantitativa / Modelagem (Quant Researcher)
- *Formulou motor de amostragem por desequilíbrio de fluxo de ordens (Imbalance Bars), recuperando a normalidade assintótica de retornos via Teorema Central do Limite e eliminando distorções de heterocedasticidade amostral.*
- *Implementou rotinas de detecção sequencial de quebras de regime baseadas no Teste da Razão de Verossimilhança e Teorema de Wilks, acopladas diretamente a streams de cotações em tempo real.*
- *Desenvolveu motor de replay de mercado determinístico point-in-time, garantindo fidelidade estrita à filtragem de informação temporal e eliminando viés de antecipação (look-ahead bias) em backtests.*

---

## 3. Guia de Respostas para Entrevistas Técnicas

### Pergunta: "Por que você usou gRPC em vez de WebSockets ou REST?"
> *"REST foi mantido como interface secundária para consultas pontuais de baixo overhead. No entanto, para streaming contínuo de milhares de ticks por segundo, o gRPC sob HTTP/2 com Protocol Buffers binários eliminou a serialização redundante de texto (JSON) e permitiu multiplexação sobre uma única conexão TCP. Nos benchmarks empíricos do meu TCC com mais de 16 mil barras de dados reais da B3, o gRPC cortou a latência média pela metade e dobrou a vazão em relação ao HTTPS tradicional."*

### Pergunta: "Qual é o problema de usar barras de 1 minuto em estratégias quantitativas?"
> *"Barras de tempo fixo violam a premissa de distribuição gaussiana e introduzem heterocedasticidade amostral severa: durante notícias de alto impacto, 1 minuto contém excesso de informação que é espremido em uma única barra, enquanto em períodos calmos gera barras com volume insignificante e ruído artificial. No planejamento da evolução do qDATA, introduzimos Dollar Bars e Imbalance Bars, que amostram o mercado na velocidade do fluxo informacional, recuperando propriedades do Teorema Central do Limite."*

### Pergunta: "Como você evita look-ahead bias nos seus testes?"
> *"Estruturamos um motor de replay de mercado determinístico que respeita a filtragem temporal matemática: eventos só são emitidos e disponibilizados para o pipeline no timestamp de bolsa correspondente, sem depender do relógio local ou de índices ordenados por inserção no banco de dados. Isso assegura Point-in-Time Correctness em nível de simulação."*
