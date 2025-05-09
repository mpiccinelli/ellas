# Análise de dados da Survey do projeto ELLAS.

Este repositório contém os arquivos e códigos utilizados na análise dos dados da Survey ELLAS.

**Autores:**

- Marlos Vinicius S. Piccinelli

  - Mestrando em Computação Aplicada, PPGCA - UTFPR
  - marlosvinicius.info@gmail.com

- Nádia P. Kozievitch

  - Professora, Doutora, UTFPR
  - nadiap@utfpr.edu.br

- Rita Cristina Galarraga Berardi
  - Professora, Doutora, UTFPR
  - ritaberardi@utfpr.edu.br

## Descrição do Projeto:

O projeto ELLAS (Equality in Leadership for Latin American STEM) visa promover a igualdade de gênero em áreas de Ciência, Tecnologia, Engenharia e Matemática (STEM) na América Latina. Este estudo foca nos dados da Survey realizada a pedido do ELLAS. A partir da análise dos dados, buscamos contribuir para a formulação de estratégias e políticas que promovam a igualdade de gênero e a inclusão de mulheres em áreas de STEM.

**Objetivo do Estudo:**
Analisar os dados da Survey para identificar padrões e tendências relacionados à igualdade de gênero em STEM na América Latina, com foco em lideranças femininas. O presente estudo busca complementar os dados da plataforma ELLAS, com quantificações e análises que possam contribuir para a formulação de políticas públicas e estratégias de inclusão.

**Origem dos Dados:**
Os dados foram coletados por meio de questionários online aplicados no Brasil, Peru e Bolivia com o auxílio de empresas especializadas em pesquisa de mercado e instituições acadêmicas. A pesquisa foi realizada entre 2023 e 2024, com o objetivo de entender o perfil, as experiências e desafios enfrentados por mulheres em STEM na América Latina, e complementar os dados disponibilizados na plataforma de dados abertos mentida peo projeto ELLAS. A pesquisa foi aprovada por comitês de ética e respeitou as diretrizes de consentimento informado e confidencialidade dos participantes. Os dados foram disponibilizados em formato xlsx e CSV, com dicionário de dados e informações sobre a coleta, perfil e objetivos de cada variável.

**Estrutura de Arquivos:**

```
├── ELLAS
│   └── Data
│       └── Original
│           └── dataset.csv
│           └── dictionary.csv
│       └── Normalization
│           └── Ethnic
│               └── harmonization_ethnic_data.csv
│           └── Gender
│               └── normalization_gender_base.csv
│               └── normalization_gender_data.csv
│               └── data_gender_normalized.csv
│               └── prompt.md
│               └── prompt_refine.md
│               └── Reproduction
│                   └── Gemini_mapping.csv
│                   └── GPT_normalization_gender_with_spelling.csv
│                   └── Prompt_reprodution.md
│           └── Professional
│               └── normalization_professional_base.csv
│               └── normalization_professional_with_translated.csv
│               └── data_professional_normalized.csv
│               └── prompt.md
│           └── Course
│               └── normalization_course_base.csv
│               └── normalization_course_with_translated.csv
│               └── data_course_normalized.csv
│               └── prompt.md
│           └── data_cleaned.csv
│           └── data_cleaned_normalized.csv
│       └── Dictionaries
│           └── dictionary_A1_informed_consent.csv
│           └── dictionary_Country.csv
│           └── dictionary_course_area.csv
│           └── dictionary_courses.csv
│           └── dictionary_D1_1_range.csv
│           └── dictionary_D2_sex.csv
│           └── dictionary_D3_gender_classification.csv
│           └── dictionary_D3_gender.csv
│           └── dictionary_D4_ethnic_group_especification.csv
│           └── dictionary_D4_ethnic_group.csv
│           └── dictionary_D5_state.csv
│           └── dictionary_D6_city.csv
│           └── dictionary_D7_marital_status.csv
│           └── dictionary_D11_O_professional_area_other.csv
│           └── dictionary_D11_professional_area.csv
│           └── dictionary_G7_IT_area.csv
│           └── dictionary_likert.csv
│           └── dictionary_Problem_case.csv
│           └── dictionary_si_no.csv
│       └── Consolidated
│           └── data_encoded.csv
│           └── data_decoded.csv
│           └── dictionary_consolidated.csv
│           └── prompt.md
│   └── Ontology
│       └── Ellas3.1.owl
│   └── Images
│       └── AE (Análise Exploratória)
│       └── Course (Normalização)
│       └── Gender (Normalização)
│       └── Professional (Normalização)
│       └── LLM (Prompts)
│   └── Source
│       └── 1 - Limpeza e tratamento.ipynb
│       └── 2 - Análise Exploratória.ipynb
│       └── 3 - Normalização de Gêneros.ipynb
│       └── 3.1 - Mesclagem de dados.ipynb
│       └── 3.2 - Reanálise.ipynb
│       └── 4 - Normalização de Cursos.ipynb
│       └── 4.1 - Mesclagem de dados.ipynb
│       └── 4.2 - Reanálise.ipynb
│       └── 5 - Normalização de Área Profissional.ipynb
│       └── 5.1 - Mesclagem de dados.ipynb
│       └── 5.2 - Reanálise.ipynb
│   └── README.md
└────── LICENSE
```

## Metodologia:

Todos os dados foram processados utilizando Python com as bibliotecas Pandas, Matplotlib e Seaborn. Utilizamos também o Jupyter Notebook para facilitar a visualização e análise dos dados. O código foi organizado em diferentes notebooks, cada um focando em uma parte específica do processo de análise. Os notebooks estão organizados na pasta _Source_ do repositório.
Além disso, utilizamos LLMs (Large Language Models) para auxiliar na normalização dos dados, codificação e decodificação, e na criação dos dicionários.

A análise foi dividida em três etapas principais: Análise exploratória, Limpeza e tratamento dos dados, Visualização e Análise dos dados. A seguir, apresentamos um resumo de cada etapa:

### Análise Exploratória:

Nesta etapa, foram realizadas análises descritivas e estatísticas dos dados, com o objetivo de identificar padrões, tendências e relações entre as variáveis. Foram gerados gráficos e tabelas para facilitar a visualização dos resultados. A visualização dos gráficos nos permitiu identificar problemas de qualidade ds dados, como colunas não normalizadas nas variáveis de etnia, gênero, estado, cidade, curso superior, pós graduação, mestrado, doutorado e pós doutorado e na área de formação. Além disso, foram identificados outros problemas, como a presença de valores ausentes e alguns outliers em campos como quantidade de filhos, idade e tempo de experiência.

### Limpeza e Tratamento dos Dados:

Nesta etapa, os dados foram carregados e verificados quanto à presença de valores ausentes, inconsistências e erros. As variáveis foram identificadas com o auxilio do dicionario fornecido para facilitar a leitura e compreensão. Os dados foram normalizados e padronizados, conforme necessário, para garantir a consistência. Além disso, foram aplicadas técnicas de harmonização étnica, normalização de gênero, cursos e áreas profissionais. As normalizações foram realizadas com o auxílio de LLMs (Large Language Models) e todo o processo foi documentado em um arquivo de prompt, que pode ser encontrado na pasta _Prompt_.
Os dados foram divididos em três partes: dados de gênero, dados de cursos e dados de áreas profissionais. Cada parte foi normalizada separadamente, utilizando os dicionários fornecidos para garantir a consistência e a padronização dos dados. Os dados normalizados foram salvos em arquivos separados para facilitar a análise posterior.
Após a normalização, os dados foram mesclados em um único arquivo, que contém todas as colunas originais, além das colunas normalizadas. O arquivo final foi salvo como `data_cleaned_normalized.csv`, que contém todos os dados tratados e normalizados.
Por fim, os dados foram codificados e decodificados, utilizando os dicionários fornecidos para garantir a consistência e a padronização dos dados e depois foram salvos em um arquivo separado para facilitar a análise posterior. O arquivo codificado foi salvo como `data_encoded.csv`, que contém todos os dados tratados e normalizados, com as colunas codificadas. O arquivo decodificado foi salvo como `data_decoded.csv`, que contém todos os dados tratados e normalizados, com as colunas decodificadas. Um novo arquivo de dicionário foi gerado, chamado `dictionary_consolidated.csv`, que contém todas as colunas do arquivo `data_encoded.csv`, com os nomes das colunas e os dicionários utilizados para a normalização. Esse arquivo pode ser utilizado para facilitar a leitura e compreensão dos dados.
Vale ressaltar que todo o processo de codificação e decodificação também foi realizado com o auxílio de LLMs (Large Language Models), assim como a criação dos dicionários. O processo todo foi supervisionado e esta documentado em um arquivo de prompt, que pode ser encontrado na pasta _Consolidated_.

### Visualização e Análise dos Dados:

## Resultados:

## Conclusões:

## Contribuições:

## Agradecimentos:

## Referências:

- Maciel, C., Guzman, I., Berardi, R., Caballero, B. B., Rodriguez, N., Frigo, L., Salgado, L., Jimenez, E., Bim, S. A. and Tapia, P. C. _Open Data Platform to Promote Gender Equality Policies in STEM_, **In Proceedings of the Western Decision Sciences Institute (WDSI)**. April 2023. Portland Oregon, EUA. Disponível em: <https://wdsinet.org/Annual_Meetings/2023_Proceedings/papers/198..pdf>. Acessado em: 24 abr. 2025.

- Berardi, R., Auceli, P., Maciel, C., Davila, G., Guzman, I., & Mendes, L. ELLAS: Uma plataforma de dados abertos com foco em lideranças femininas em STEM no contexto da América Latina. **In Anais do XVII Women in Information Technology**, (pp. 124-135). Porto Alegre: SBC. doi:10.5753/wit.2023.230764. Disponível em: <https://sol.sbc.org.br/index.php/wit/article/view/25016>. Acessado em: 24 abr. 2025.

- UNESCO. _School-related violence and bullying on the basis of Sexual Orientation and Gender Identity or Expression (SOGIE): a global review of current evidence to inform policy, practice and research_. **UNESCO**, 2018. Disponível em: <https://unesdoc.unesco.org/ark:/48223/pf0000366434>. Acessado em: 24 abr. 2025.

- UNESCO. _Safe, Seen and Included: Inclusion and diversity within educational settings_. **UNESCO**, 2016. Disponível em: <https://unesdoc.unesco.org/ark:/48223/pf0000385417>. Acessado em: 24 abr. 2025.

- OHCHR. _UN Free & Equal: a global campaign to promote equal rights for LGBTI people_. **Office of the United Nations High Commissioner for Human Rights**, 2018. Disponível em: <https://www.ohchr.org/en/sexual-orientation-and-gender-identity/un-free-equal-global-campaign-promote-equal-rights-lgbti-people>. Acessado em: 24 abr. 2025.

- UNESCO. _Bringing it Out in the Open: Monitoring school violence based on sexual orientation, gender identity or gender expression in national and international surveys_. **UNESCO**, 2019. Disponível em: <https://unesdoc.unesco.org/ark:/48223/pf0000367493>. Acessado em: 24 abr. 2025.
