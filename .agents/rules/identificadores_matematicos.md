# DIRETIVA DE IDENTIFICAÇÃO E INDEXAÇÃO DE ELEMENTOS MATEMÁTICOS

Esta regra estabelece o padrão obrigatório de etiquetagem, catalogação e unicidade para todos os elementos matemáticos (fórmulas, axiomas, teoremas, definições, lemas e proposições) no repositório.

---

## 1. Regra de Identificação Única por Categoria
Todo elemento matemático formal introduzido, citado ou revisado no repositório deve receber um identificador único alfanumérico entre parênteses, estruturado por categoria e índice sequencial incremental:

| Categoria | Prefixo | Formato do Código | Arquivo de Log em `math/` | Exemplo |
| :--- | :---: | :---: | :---: | :---: |
| **Fórmula / Equação** | `F` | `(F<n>)` | `math/f.log` | `(F1)`, `(F2)` |
| **Axioma** | `A` | `(A<n>)` | `math/a.log` | `(A1)`, `(A2)` |
| **Teorema** | `T` | `(T<n>)` | `math/t.log` | `(T1)`, `(T2)` |
| **Definição** | `D` | `(D<n>)` | `math/d.log` | `(D1)`, `(D2)` |
| **Lema** | `L` | `(L<n>)` | `math/l.log` | `(L1)`, `(L2)` |
| **Proposição** | `P` | `(P<n>)` | `math/p.log` | `(P1)`, `(P2)` |

---

## 2. Formatação nos Documentos (Markdown / LaTeX)
O identificador deve ser associado diretamente ao elemento:
1. **Em equações destacadas (display math):**
   - Utilizar `\tag{(F<n>)}` dentro do bloco `$$ ... $$` ou escrever o identificador `(F<n>)` adjacente ao bloco em linha destacada.
   ```latex
   $$
   b_t = \begin{cases} +1, & \text{se } \Delta P_t > 0 \\ -1, & \text{se } \Delta P_t < 0 \\ b_{t-1}, & \text{se } \Delta P_t = 0 \end{cases} \tag{(F1)}
   $$
   ```
2. **Em axiomas, teoremas e definições:**
   - Inserir o código no título ou na abertura do enunciado:
   ```markdown
   > **Axioma (A1) (Não-Antecipação / Adaptabilidade):** Seja $(\mathcal{F}_t)_{t \ge 0}$ uma filtragem...
   ```

---

## 3. Registro e Persistência em `math/`
Para garantir a integridade referencial e o controle sequencial:
1. Todo código gerado **deve ser registrado imediatamente** no respectivo arquivo de log em `math/`:
   - Axiomas: `math/a.log`
   - Fórmulas: `math/f.log`
   - Teoremas: `math/t.log`
   - Demais categorias: `math/<prefixo_minusculo>.log`
2. **Estrutura do Log:** O código é registrado simplesmente colocando o código (ex: `(F1)`), **um abaixo do outro** (uma linha por identificador):
   ```text
   (F1)
   (F2)
   (F3)
   ```
3. **Cálculo do Próximo Código:** 
   - O próximo identificador da categoria é estritamente $N+1$, onde $N$ é o número de entradas já registradas no respectivo arquivo `.log`. Se o arquivo estiver vazio, o índice inicial é `1`.
