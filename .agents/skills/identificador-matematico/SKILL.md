---
name: identificador-matematico
description: Dispara automaticamente quando há um elemento matemático (fórmula, equação, expressão matemática, axioma, teorema, definição ou lema) sem identificador único em documentos ou códigos do repositório. Revisa o conteúdo, categoriza o elemento, atribui o código sequencial correspondente no formato (Fn), ((En)), (An), (Tn) e registra o identificador no arquivo correspondente dentro de math/ (f.log, e.log, a.log, t.log, etc.), um abaixo do outro.
---

# Skill: Identificador e Indexador Matemático (`identificador-matematico`)

Esta skill é responsável por detectar, classificar, numerar e registrar formalmente todos os elementos matemáticos do repositório que ainda não possuam identificação única categórica.

---

## 1. Condições de Disparo Automático
A skill deve ser ativada automaticamente sempre que:
1. Um documento ou código recém-criado, editado ou inspecionado contiver fórmulas ou expressões matemáticas (`$$ ... $$`, equações, expressões matemáticas destacadas, axiomas, teoremas, definições) desprovidas de identificador formal `(F<n>)`, `((E<n>))`, `(A<n>)`, `(T<n>)`, etc.
2. O usuário solicitar revisão de fórmulas, expressões, axiomas ou da notação matemática do projeto.
3. Houver inconsistência ou lacuna entre as fórmulas/expressões utilizadas nos documentos e os registros em `math/`.

---

## 2. Categorias e Mapeamento de Arquivos em `math/`

| Elemento | Prefixo | Formato do Identificador | Arquivo de Destino em `math/` |
| :--- | :---: | :---: | :---: |
| Fórmula / Equação | `F` | `(F<n>)` | `math/f.log` |
| Expressão Matemática | `E` | `((E<n>))` | `math/e.log` |
| Axioma | `A` | `(A<n>)` | `math/a.log` |
| Teorema | `T` | `(T<n>)` | `math/t.log` |
| Definição | `D` | `(D<n>)` | `math/d.log` |
| Lema | `L` | `(L<n>)` | `math/l.log` |

---

## 3. Fluxo Operacional de Execução

Ao detectar elementos sem identificador, execute o seguinte procedimento:

### Passo 1: Inspeção do Log em `math/`
1. Acesse o arquivo de log correspondente à categoria do elemento (ex: `math/f.log` para fórmulas, `math/e.log` para expressões, `math/a.log` para axiomas).
2. Se o arquivo não existir, crie-o.
3. Conte o número de linhas não-vazias preenchidas para determinar o índice atual $N$.
   - Para expressões matemáticas (`E`), o identificador utiliza parênteses duplos: `((E<N+1>))`.
   - Para as demais categorias, utiliza parênteses simples: `(<Prefixo><N+1>)`.
   - *Exemplo:* Se `math/e.log` estiver vazio, o primeiro código será `((E1))`. Se contiver `((E1))`, o próximo será `((E2))`.
   - *Exemplo:* Se `math/f.log` contém `(F1)` e `(F2)`, o próximo elemento será `(F3)`.

### Passo 2: Aplicação do Identificador no Arquivo
1. Para fórmulas e equações LaTeX (`$$ ... $$`):
   - Adicionar a tag de numeração `\tag{(F<n>)}` ao final da fórmula.
2. Para expressões matemáticas destacadas ou com identificação dedicada:
   - Adicionar a tag `\tag{((E<n>))}` ao final da expressão no bloco LaTeX ou posicionar o código `((E<n>))` de forma adjacente e destacada.
3. Para axiomas, teoremas e definições:
   - Adicionar o identificador junto ao título do bloco (ex: `> **Axioma (A1):** ...` ou `### Teorema (T1)`).

### Passo 3: Registro em `math/<categoria>.log`
1. Anexe o código gerado ao final do arquivo respectivo dentro de `math/`.
2. Garanta que cada código fique estritamente **um abaixo do outro** (uma linha única por código):
   ```text
   ((E1))
   ((E2))
   ```
3. Não insira comentários, vírgulas ou metadados nos arquivos `.log` — apenas os códigos identificadores, um por linha.

---

## 4. Diretrizes de Rigor e Não-Duplicação
- Nunca reutilize um identificador já registrado em `math/`.
- Diferencie rigorosamente:
  - **Fórmulas/Equações `(Fn)`:** Relações de igualdade, desigualdade ou sistemas completos de equações.
  - **Expressões `((En))`:** Termos matemáticos, operadores, grandezas ou fragmentos funcionais sem operador relacional principal que demandem indexação própria.
- Mantenha a ordenação sequencial estrita ($1, 2, 3, \dots$).
