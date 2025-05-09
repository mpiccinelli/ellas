## 1. Carregamento dos arquivos iniciais

No início do processo, carregamos dois arquivos fundamentais:

- **`data_cleaned_normalized.csv`**: contém todos os registros da pesquisa, já limpos e normalizados (por gênero, etnia, cursos e áreas profissionais).
- **`dictionary.csv`**: é o “manual” de todas as variáveis do dataset, informando o nome da coluna, o tipo de resposta (dicotômica, Likert, texto livre etc.) e, quando aplicável, a coluna **Possible_Answers** com os códigos e seus significados.

---

## 2. Identificação e agrupamento das colunas codificadas

Primeiro, usamos o `dictionary.csv` para saber exatamente quais colunas estavam codificadas e qual o tipo de cada resposta:

1. **Tipos “dicotômicos”** (ex.: sim/não)
2. **Escalas Likert** (1 a 7, de “discordo fortemente” a “concordo fortemente”)
3. **Variáveis que já tinham dicionário individual** (como `Country`, `A1_informed_consent` etc.)
4. **Colunas de texto livre** (que não precisaram de decodificação)

Dividimos as variáveis em grupos, para aplicar dicionários específicos ou genéricos conforme o tipo.

---

## 3. Geração dos dicionários de mapeamento

Para cada grupo de colunas, criamos um arquivo CSV contendo duas colunas:

- **id**: o código numérico original
- **description**: o texto correspondente

**3.1. Dicionários específicos**  
Esses arquivos tratam colunas que já vinham com dicionários próprios no `dictionary.csv`:

```
Dictionaries/
├── dictionary_A1_informed_consent.csv
├── dictionary_Country.csv
├── dictionary_D1_1_range.csv
├── dictionary_D2_sex.csv
├── dictionary_D5_state.csv
├── dictionary_D6_county.csv
├── dictionary_D7_marital_status.csv
├── dictionary_D11_professional_area.csv
├── dictionary_G7_IT_area.csv
├── dictionary_Problem_case.csv
```

**3.2. Dicionários genéricos**  
Algumas colunas compartilham o mesmo formato de resposta, então usamos um único dicionário para todas elas:

```
Dictionaries/
├── dictionary_si_no.csv        # todas as perguntas dicotômicas
├── dictionary_likert.csv       # todas as escalas Likert
└── dictionary_course_area.csv  # unifica as 4 colunas de área de curso
```

**3.3. Dicionários oriúndos da normalização**  
Esses dicionários foram criados durante o processo da normalização do dataset, e são utilizados para decodificar as colunas de texto livre:

```
Dictionaries/
├── dictionary_courses.csv # cursos
├── dictionary_D3_gender.csv # gênero
├── dictionary_D3_gender_classification.csv # classificação de gênero
├── dictionary_D4_ethnic_group.csv # etnia
├── dictionary_D4_ethnic_group_especification.csv # especificação de etnia
└── dictionary_D11_O_professional_area_other.csv # área profissional
```

---

## 4. Codificação completa do dataset

Com todos os dicionários prontos, exportamos o **`data_encoded.csv`**, onde cada coluna codificada foi substituída pelo seu **id** numérico. Essa versão é ideal para análises estatísticas e modelagem, pois usa apenas números.

---

## 5. Decodificação de volta para texto

Para que um usuário leigo consiga interpretar facilmente o resultado, aplicamos **todos** os dicionários (tanto os específicos quanto os genéricos) no arquivo codificado, revertendo cada código ao seu texto descritivo.

1. Utilizamos `dictionary_si_no.csv` e `dictionary_likert.csv` para as colunas genéricas.
2. Reaplicamos os dicionários específicos (por exemplo, `dictionary_D11_professional_area.csv` e `dictionary_course_area.csv`).
3. Para as colunas de texto livre, não houve necessidade de decodificação, pois já estavam em texto.

---

## 6. Exportação do dataset decodificado

Ao final, geramos o arquivo **`data_decoded.csv`**, que contém todas as variáveis com respostas em texto, facilitando a leitura e interpretação dos dados.
O arquivo é uma versão mais amigável do dataset, ideal para usuários que não estão familiarizados com os códigos numéricos.

### Considerações finais

- **Rastreabilidade**: cada passo (criação de dicionários, codificação e decodificação) está documentado em prompts e scripts, garantindo que qualquer etapa possa ser reproduzida.
- **Clareza para o usuário**: o arquivo final decodificado pode ser aberto em Excel ou outro visualizador, mostrando apenas texto, sem necessidade de consultar códigos numéricos.
- **Conferência de dados**: ao longo do processo, foram feitas verificações para garantir que não houve perda de informações durante a codificação e decodificação.
- **Flexibilidade**: o sistema de dicionários permite fácil atualização e adição de novas colunas ou categorias, tornando o processo escalável.