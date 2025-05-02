# Processo Reproduzível para Normalização da Coluna `D3_gender`

Este documento descreve **como reconstruir, de forma 100 % reproduzível**, a sequência de prompts necessária para corrigir e padronizar a coluna `D3_gender` em dois idiomas (PT‑BR e ES) no arquivo `normalization_gender_base.csv`. Ele surgiu porque o _prompt_ original, embora tenha funcionado no contexto da sessão, **não garantiu o mesmo resultado ao ser reutilizado**. Segue a nova metodologia que evita esse problema.

> **Observação:** O processo de correção ortográfica (spelling) originalmente foir realizado seguindo o fluxo de trabalho definido no arquivo [`Prompt_refine.md`](../prompt_refine.md).

---

## 1  Por que o _super‑prompt_ falhou

| Limitação / Risco                                                                                              | Consequência prática                                                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Contexto invisível**: o modelo mistura instruções com raciocínio, mas não executa código Python internamente | O _super‑prompt_ pedia ao modelo para “corrigir” e, ao mesmo tempo, ler arquivos CSV; parte da lógica precisava de Python (pandas) e parte do conhecimento linguístico do LLM. Essa colisão gerou erros de parsing e dicionários incompletos. |
| **Dados reais são sujos**: delimitador variável, erros de codificação                                          | Um comando único não dava espaço para detectar e contornar o `ParserError` antes de prosseguir, propagando falhas invisíveis.                                                                                                                 |
| **Validação humana necessária**: listas de correção podem requerer revisão                                     | Sem checkpoints intermediários, qualquer erro ortográfico passaria despercebido até o final, exigindo retrabalho completo.                                                                                                                    |

> **Conclusão**  →  Dividir em **vários prompts pequenos** permite:
> • diagnosticar problemas cedo;
> • alternar entre _modo‑Python_ (manipulação de dados) e _modo‑LLM_ (correção linguística);
> • obter confirmações parciais antes de comprometer o resultado final.

---

## 2  Premissas que garantem a reprodutibilidade

1. **Encoding fixo** `utf‑8‑sig` e **separador** `;` (evita erros de tokenização).
2. Coluna **`Country`** usada para mapear idioma (Brasil → PT‑BR; Peru/Bolívia → ES).
3. Correções ortográficas **não** devem ser feitas em Python, mas pelo próprio LLM (contexto linguístico global).
4. Todas as etapas produzem saídas verificáveis (tabelas interativas, contagens, previews).
5. O arquivo final deve preservar as colunas originais e adicionar **`Spelling`**.

---

## 3  Sequência de Prompts (6 passos)

> Copie e cole cada bloco, **na ordem**, em uma nova sessão do ChatGPT. Siga as instruções que o modelo devolve em cada etapa antes de passar ao próximo prompt.

### Prompt 1  — Carregar e listar valores únicos

```
Seguem os dados originais (normalization_gender_base.csv). Abra o arquivo com encoding='utf-8-sig' e separador ';'.
• Crie a coluna Language: Brasil → PT-BR; Peru/Bolívia → ES.
• Para cada idioma, liste TODOS os valores únicos da coluna D3_gender e exiba-os em uma tabela interativa.
```

### Prompt 2  — Contagem de termos em espanhol

```
Quais e quantos são os termos únicos em espanhol?
```

### Prompt 3  — Correção completa (ES)

```
Corrija TODOS os termos únicos em espanhol quanto à grafia, acentuação e capitalização. Apresente a tabela original × corrigido e, ao final, a lista dos termos corrigidos.
```

### Prompt 4  — Contagem de termos em português

```
Agora faça o mesmo para o português: identifique todos os termos únicos em PT-BR e informe o total.
```

### Prompt 5  — Correção completa (PT‑BR)

```
Corrija TODOS os termos únicos em português quanto à digitação e acentuação. Mostre a tabela original × corrigido e a lista consolidada de formas corretas.
```

### Prompt 6  — Aplicar dicionário e salvar resultado

```
Usando os dicionários ES + PT-BR, crie no dataset original uma coluna Spelling com o termo corrigido correspondente a cada valor em D3_gender.
Salve o arquivo como normalization_gender_with_spelling.csv (UTF-8) e exiba uma prévia das primeiras linhas. Disponibilize o link para download.
```

---

## 4  Por que essa divisão funciona

1. **Passo 1 (Carga e inspeção)** lida exclusivamente com leitura de dados (Python/pandas), sem misturar correção linguística.
2. **Passos 2 e 4** são checkpoints obrigatórios, provando que as listas estão completas antes de corrigir.
3. **Passos 3 e 5** usam o _core_ linguístico do modelo para padronizar grafia; aqui não há execução Python, apenas lógica textual.
4. **Passo 6** volta ao modo‑Python, aplicando o dicionário consolidado a todo o dataframe e salvando o CSV.

> **Dessa forma, cada prompt usa apenas o “modo” apropriado** — evitamos pedir ao modelo algo que dependa simultaneamente de contexto linguístico avançado _e_ manipulação de dados, tarefa que ele não consegue executar num único bloco.

---

## 5  Reuso e adaptação

- **Outra base de dados?** Mantenha Prompt 1 (ajustando encoding/separador) e siga a sequência – a lógica continua válida.
- **Novo idioma?** Inclua o mapeamento no Prompt 1 e repita Prompts 2 e 3 para o novo grupo linguístico.
- **Mais colunas a corrigir?** Basta expandir a lógica do Passo 6 para incluir novas colunas e dicionários.

---

### ✔ Com este roteiro, conseguimos reproduzir a normalização de `D3_gender` e obter o **mesmo CSV final**, sem depender de detalhes implícitos na sessão original.
