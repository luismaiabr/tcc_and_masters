---
name: gestao-duvidas
description: NUNCA dispare esta skill automaticamente. Ative APENAS quando o usuário invocar expressamente o comando da skill (ex: `gestao-duvidas`, `/gestao-duvidas`) ou solicitar expressamente a criação/consolidação de um módulo educativo permanente no diretório `duvidas/`. Se o usuário apenas pedir uma explicação ou tirar dúvidas sem usar o comando, explique diretamente no chat sem acionar esta skill.
---

# Skill: Gestão de Dúvidas e Módulos Educacionais (`gestao-duvidas`)

Esta skill orienta o processo de estruturação e registro de módulos didáticos permanentes dentro do diretório `duvidas/`, acionada **exclusivamente sob comando explícito do usuário**.

---

## 1. Condições de Disparo (Acionamento Exclusivo por Comando)
- **REGRA FUNDAMENTAL:** Esta skill **NUNCA dispara de forma automática**.
- Se o usuário pedir explicações conceituais, análises ou tirar dúvidas sem usar o comando expressamente:
  - **Responda direta, profunda e pragmaticamente no chat.**
  - **NÃO ative esta skill** e **NÃO interrompa o fluxo** perguntando compulsoriamente sobre criação de módulos no repositório.
- A skill deve ser ativada **UNICAMENTE** quando:
  1. O usuário invocar expressamente o comando da skill (ex: `gestao-duvidas`, `/gestao-duvidas`, "use a skill gestao-duvidas").
  2. O usuário solicitar expressamente: "crie o módulo educacional para esta dúvida", "salve essa explicação em duvidas/", ou instrução análoga explícita.

---

## 2. Fluxo Operacional (Disparado pelo Comando)

### Fase 1: Identificação do Tema e Estruturação
Como a skill foi expressamente acionada pelo usuário:
1. Recupere o contexto da dúvida debatida ou do tópico solicitado.
2. Defina um slug conciso e representativo em `snake_case` (ex: `duvidas/amostragem_dollar_bars/`, `duvidas/filtro_kalman_streaming/`).
3. Confirme rapidamente os parâmetros com o usuário caso haja ambiguidade no slug ou no escopo.

### Fase 2: Geração do Módulo Educacional
Após o acionamento do comando pelo usuário:
1. Defina um slug conciso e representativo em `snake_case` (ex: `duvidas/amostragem_dollar_bars/`, `duvidas/filtro_kalman_streaming/`).
2. Crie a pasta do módulo contendo os três arquivos canônicos:

#### A. `contexto.md`
- **Gênese da Dúvida:** Pergunta original formulada pelo usuário e pontos nodais levantados.
- **Inserção no qDATA/TCC:** Em qual seção do TCC (ex: 6.4.1 Amostragem, 6.4.2 LOB, etc.) ou componente do qDATA o assunto se apoia.
- **Relevância Acadêmica / ABE:** Conexão direta com tópicos do exame da ABE (Probabilidade, Inferência, Álgebra Linear) e mestrado no IME-USP.

#### B. `licao.md`
- **Fundamentação Conceitual:** Explicação didática completa e estruturada.
- **Rigor Matemático:** Derivações passo a passo, fórmulas identificadas com tags `\tag{(F<n>)}`, `\tag{((E<n>))}`, `(A<n>)`, etc.
  - *Regra Cruzada:* Acione a skill `identificador-matematico` para registrar formalmente todo novo elemento em `math/<tipo>.log`.
- **Perspectiva de Engenharia de Software:** Aplicação prática, complexidade assintótica $O(\cdot)$, concorrência, tratamento de latência e código de referência (Python, C++ ou Rust).
- **Takeaways Centrais:** Síntese em tópicos objetivos dos pontos de retenção da aula.

#### C. `bibliografia.md`
- **Livros e Obras de Referência:** Mapeamento com indicação precisa de **capítulos, seções e páginas** (ex: *López de Prado, Cap. 2, Seções 2.3.1 e 2.3.2*).
- **Artigos Seminais:** Papers acadêmicos com autores, ano, título, periódico e DOI/link.
- **Recursos da Indústria:** Posts técnicos de blogs e whitepapers de prop trading e market makers respeitados.

#### D. Atualização do Índice
- Atualize [duvidas/README.md](file:///c:/Users/Luis%20Maia/Documents/TCC2/tcc_and_masters/duvidas/README.md) inserindo o novo módulo na seção "Módulos Disponíveis" com link direto para a lição, contexto e bibliografia.

---

## 3. Diretrizes de Qualidade e Integridade
- **Rigor sem Superficialidade:** Evite resumos rasos; a lição deve funcionar como material de consulta definitiva para o mestrado e para entrevistas técnicas quantitativas.
- **Navegação Cruzada:** Todos os arquivos gerados devem conter links de navegação para o contexto, lição, bibliografia e para o índice geral de dúvidas.
