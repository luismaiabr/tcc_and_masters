# DIRETIVA DE GESTÃO DE DÚVIDAS E CRIAÇÃO DE CONTEÚDO EDUCACIONAL

Esta diretiva governa a criação e estruturação de materiais educativos no repositório a partir de dúvidas levantadas por Luis Maia.

---

## 1. Gatilho e Confirmação Prévia Obrigatória
Sempre que o usuário expressar uma dúvida sobre qualquer conceito, teoria estatística, decisão arquitetural, ferramenta ou modelo:
1. **Responda objetivamente à dúvida** na conversa.
2. **Pergunte expressamente ao usuário** se ele deseja que seja gerado o módulo educacional correspondente dentro do diretório `duvidas/`.
   - *Exemplo de confirmação:* "Deseja que eu crie o módulo educacional completo para esta dúvida em `duvidas/<titulo_da_duvida>/`?"
3. **NÃO crie os arquivos antes da confirmação explícita do usuário.**

---

## 2. Estrutura de Pastas e Arquivos
Após a autorização do usuário, crie uma pasta dedicada dentro de `duvidas/` cujo nome seja o título ou slug representativo da dúvida (ex: `duvidas/invariancia_amostragem_dollar_bars/` ou `duvidas/teste_razao_verossimilhanca_wilks/`).

A pasta deve conter **obrigatoriamente três arquivos Markdown**:

### 2.1. `contexto.md`
- **Objetivo:** Registrar a gênese e o escopo da dúvida.
- **Conteúdo Obrigatório:**
  - Descrição da dúvida levantada.
  - Ponto de partida / contexto prático (em que parte do qDATA, da Seção 6.4 do TCC ou do cronograma do IME-USP a dúvida se insere).
  - Motivação: por que compreender esse conceito é crítico para o projeto ou para a aprovação na ABE.

### 2.2. `licao.md`
- **Objetivo:** A lição completa, estruturada e didática (tutorial / lesson).
- **Conteúdo Obrigatório:**
  - Explicação teórica formal, com derivações matemáticas e notação rigorosa quando aplicável.
  - Conexão prática com código ou arquitetura de software (Dupla Lente: Engenharia + Estatística).
  - Exemplos ilustrativos, diagramas conceituais ou trechos em pseudocódigo/Python/Rust.
  - Conclusão com os *takeaways* centrais da lição.

### 2.3. `bibliografia.md`
- **Objetivo:** Mapeamento bibliográfico aprofundado para estudo contínuo.
- **Conteúdo Permitido e Encorajado:**
  - Artigos acadêmicos fundamentais (com autores, ano, título e DOI/link quando aplicável).
  - Artigos não-acadêmicos, *whitepapers* de mercado e posts de blogs de engenharia quantitativa de referência.
  - Recomendações de livros-texto com indicação **preferencial de capítulos e seções específicas** (ex: *Bolfarine & Sandoval, Cap. 4, Seção 4.2* ou *López de Prado, Cap. 2*).
