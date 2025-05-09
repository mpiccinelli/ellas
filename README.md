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
│       └── 6 - Análise Exploratória - Pós normalização.ipynb
│   └── README.md
└────── LICENSE
```

## Metodologia:

Todos os dados foram processados utilizando Python com as bibliotecas Pandas, Matplotlib e Seaborn. Utilizamos também o Jupyter Notebook para facilitar a visualização e análise dos dados. O código foi organizado em diferentes notebooks, cada um focando em uma parte específica do processo de análise. Os notebooks estão organizados na pasta _Source_ do repositório.
Além disso, utilizamos LLMs (Large Language Models) para auxiliar na normalização dos dados, codificação e decodificação, e na criação dos dicionários.

A análise foi dividida em três etapas principais: Análise exploratória, Limpeza e tratamento dos dados, Visualização e Análise dos dados. A seguir, apresentamos um resumo de cada etapa:

### Análise Exploratória:

Nesta etapa, foram realizadas análises descritivas e estatísticas dos dados, com o objetivo de identificar padrões, tendências e relações entre as variáveis. Foram gerados gráficos e tabelas para facilitar a visualização dos resultados. A visualização dos gráficos nos permitiu identificar problemas de qualidade ds dados, como colunas não normalizadas nas variáveis de etnia, gênero, estado, cidade, curso superior, pós graduação, mestrado, doutorado e pós doutorado e na área de formação. Além disso, foram identificados outros problemas, como a presença de valores ausentes e alguns outliers em campos como quantidade de filhos, idade e tempo de experiência.

#### Principais problemas identificados X Possíveis soluções:

##### Gênero:

- A variável de gênero apresentava mais de 150 categorias diferentes, o que geralmente acontece quando se tem um campo de texto livre. Além da quantidade excessiva de categorias, a variável também apresentava erros de digitação e formatação, como letras maiúsculas e minúsculas, espaços em branco e caracteres especiais e diferenças de idiomas.
- A proposta apresentada para solucionar o problema foi a normalização da variável de gênero, utilizando um dicionário de normalização. O dicionário foi criado com o auxílio de LLMs (Large Language Models) e usou como base as definições de gênero e orientação sexual da UNESCO. Ainda assim, houve a necessidade de criar uma nova coluna para descrever melhor a resposta do participante, visto que nem todos os termos estavam relacionados a identidade de gênero, alguns eram relacionados a orientação sexual, como "heterossexual", "homossexual", "bissexual", e outros a expressões de gênero, como "queer". Para essa classificação criamos a coluna `D3_gender_classification`, que classifica as respostas em três categorias: identidade de gênero, orientação sexual e expressão de gênero. Essa classificação também é orientada pela UNESCO.

##### Etnia:

- A variável de etnia apresentava mais de 50 categorias diferentes. Além da quantidade excessiva de categorias, a variável também apresentava erros de digitação e formatação, como letras maiúsculas e minúsculas, espaços em branco e caracteres especiais e diferenças de idiomas.
- A proposta apresentada para solucionar o problema foi a normalização da variável de etnia, utilizando um dicionário de normalização. Como a UNESCO não apresenta uma definição clara de etnia, utilizamos como base a classificação do IBGE (Instituto Brasileiro de Geografia e Estatística). Além de categorizar as etnias, criamos uma coluna auxiliar `D4_ethnic_group_especification` para trazer as especificações de cada etnia.

#### Cidades e Estados:

- As variáveis de cidade e estado, juntas, apresentavam mais de 400 categorias diferentes. Além da quantidade excessiva de categorias, as variáveis estavam distribuídas em colunas diferentes, o que dificultava a análise.
- A proposta apresentada para solucionar o problema foi o empilhamento das variáveis de cidade e estado em apenas duas colunas `D5_state` e `D6_city`.

##### Cursos:

- As variáveis de cursos apresentavam, juntas, mais de 1000 categorias diferentes. Além da quantidade excessiva de categorias, as variáveis também apresentavam erros de digitação e formatação, como letras maiúsculas e minúsculas, espaços em branco e caracteres especiais e diferenças de idiomas.
- A proposta apresentada para solucionar o problema foi a normalização da variável de cursos, utilizando um dicionário de normalização. O dicionário foi criado com o auxílio de LLMs (Large Language Models).

##### Áreas Profissionais:

- A variável de área profissional apresentava mais de 100 categorias diferentes. Além da quantidade excessiva de categorias, a variável também apresentava erros de digitação e formatação, como letras maiúsculas e minúsculas, espaços em branco e caracteres especiais e diferenças de idiomas.
- A proposta apresentada para solucionar o problema foi a normalização da variável de área profissional, utilizando um dicionário de normalização. O dicionário foi criado com o auxílio de LLMs (Large Language Models).

### Limpeza, Tratamento e Normalização dos Dados

Nesta etapa, foram conduzidos procedimentos sistemáticos de limpeza e tratamento dos dados, com o objetivo de assegurar a qualidade e a consistência das informações para as análises subsequentes. As seguintes ações foram realizadas:

#### 1. **Verificação e Preparação Inicial**

- Os dados foram carregados e submetidos a uma verificação rigorosa para identificar valores ausentes, inconsistências e erros.
- As variáveis foram analisadas com o suporte do dicionário de dados fornecido, o que facilitou a leitura, interpretação e compreensão dos atributos presentes.

#### 2. **Normalização e Padronização dos Dados**

- Os dados foram normalizados e padronizados conforme a necessidade, garantindo a uniformidade das informações.
- Foram aplicadas técnicas específicas de:

  - **Harmonização Étnica**
  - **Normalização de Gênero**
  - **Normalização de Cursos e Áreas Profissionais**

- Essas normalizações foram realizadas com o auxílio de Modelos de Linguagem de Grande Escala (LLMs – _Large Language Models_), proporcionando maior eficiência e precisão no processo.
- Todo o procedimento foi documentado em arquivos no formato Markdown, disponíveis nas respectivas pastas de cada tipo de normalização.

#### 3. **Divisão e Consolidação dos Dados**

- Os dados foram segmentados em três conjuntos principais:

  - Dados de Gênero
  - Dados de Cursos
  - Dados de Áreas Profissionais

- Cada conjunto foi normalizado separadamente, utilizando os dicionários específicos para assegurar a padronização adequada.
- Após a normalização, os dados foram integrados em um único arquivo consolidado, preservando todas as colunas originais e adicionando as colunas normalizadas correspondentes.
- O arquivo final resultante foi denominado `data_cleaned_normalized.csv`, contendo todas as informações tratadas e normalizadas.

#### 4. **Codificação e Decodificação dos Dados**

- Os dados passaram por processos de codificação e decodificação, também com o auxílio de LLMs, utilizando os dicionários previamente definidos para garantir a consistência e a correta interpretação dos valores.
- Os arquivos gerados foram:

  - `data_encoded.csv`: contém os dados tratados e normalizados, com as colunas devidamente codificadas.
  - `data_decoded.csv`: contém os dados tratados e normalizados, com as colunas decodificadas.

#### 5. **Geração de Dicionário Consolidado**

- Foi criado um dicionário consolidado intitulado `dictionary_consolidated.csv`, que reúne:

  - Todas as colunas presentes no arquivo `data_encoded.csv`.
  - A relação dos nomes das colunas com os respectivos dicionários utilizados no processo de normalização.

- Esse arquivo tem como finalidade facilitar a leitura, interpretação e posterior utilização dos dados.

#### 6. **Documentação dos Processos**

- Todo o fluxo de trabalho, incluindo os processos de codificação, decodificação e a criação dos dicionários, foi supervisionado e rigorosamente documentado.
- A documentação completa, incluindo os prompts utilizados durante a aplicação dos LLMs, encontra-se disponível na pasta `_Consolidated_`.

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

- IBGE. _Censo Demográfico 2022: Identificação étnico-racial da população, por sexo e idade_. **Instituto Brasileiro de Geografia e Estatística**, 2022. Disponível em: <https://agenciadenoticias.ibge.gov.br/media/com_mediaibge/arquivos/13ee0337cffc1de37bf0cd4da3988e1f.pdf>. Acessado em: 24 abr. 2025.

- INEP. _Censo da Educação Superior: Microdados do Censo da Educação Superior 2023_. **Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira**, 2023. Disponível em: <https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/censo-da-educacao-superior>. Acessado em: 09 maio 2025.

- INEP. _ÁREAS DE FORMAÇÃO E TREINAMENTO DA CINE-F 2013: MANUAL QUE ACOMPANHA A CLASSIFICAÇÃO INTERNACIONAL NORMALIZADA DA EDUCAÇÃO 2011_. **Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira**, 2017. Disponível em: <https://download.inep.gov.br/publicacoes/institucionais/estatisticas_e_indicadores/areas_de_formacao_e_treinamento_da_cine-f_2013.pdf>. Acessado em: 09 maio 2025.

- UNESCO. _INTERNATIONAL STANDARD CLASSIFICATION OF EDUCATION. Fields of education and training 2013 (ISCED-F 2013) – Detailed field descriptions_. **UNESCO Institute for Statistics**, 2015. Disponível em: <http://dx.doi.org/10.15220/978-92-9189-179-5-en>. Acessado em: 09 maio 2025.
