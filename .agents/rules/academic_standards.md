# DIRETRIZES DE RIGOR ACADÊMICO E ESTATÍSTICA (IME-USP / ABE)

Ao redigir propostas de pesquisa, seções para o TCC ou materiais preparatórios para o Mestrado em Estatística (MAE / IME-USP), seguir os seguintes padrões:

## 1. Rigor Conceitual e Terminológico
- Empregar notação matemática precisa:
  - Espaço de probabilidade: $(\Omega, \mathcal{F}, \mathbb{P})$.
  - Filtragens e processos adaptados: $(\mathcal{F}_t)_{t \ge 0}$.
  - Esperança Condicional: $\mathbb{E}[X \mid \mathcal{F}_t]$ governada pela Lei das Expectativas Iteradas ($\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X \mid Y]]$).
  - Inferência: Função de verossimilhança $L(\theta)$, log-verossimilhança $\ell(\theta)$, vetor escore $S(\theta) = \nabla \ell(\theta)$ e Matriz de Informação de Fisher $I(\theta)$.
  - Propriedades assintóticas: consistência, eficiência e normalidade assintótica ($\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} \mathcal{N}(0, I(\theta)^{-1})$).
  - Testes: Teste da Razão de Verossimilhanças (TRV), Teorema de Wilks (distribuição assintótica $\chi^2$), testes de Wald e Escore.

## 2. Padrões de Escrita para o TCC (Seção 6.4)
- Formato compatível com LaTeX e normas da ABNT.
- Coesão direta com o Capítulo 6 do TCC do Luis (Conclusão e Trabalhos Futuros).
- Evitar linguagem hiperbólica ou especulativa; utilizar tom formal, científico e analítico.
- Justificar cada adição tecnológica com base em ganhos empíricos ou redução de viés estatístico (ex: eliminação de *look-ahead bias*, redução de heterocedasticidade, restauração assintótica).

## 3. Estratégia de Abordagem para Docentes do IME-USP
- Apresentar a engenharia de software não como mero suporte operacional, mas como infraestrutura habilitadora de inferência estocástica em alta frequência.
- Demonstrar fluência simultânea na linguagem teórica (Exame da ABE) e na implementação computacional eficiente (gRPC, TimescaleDB, Python/C++).
