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
│   ├── Data
│       └── Ethnic
│           └── harmonization_ethnic_data.csv
│       └── Gender
│           └── normalization_gender_base.csv
│           └── normalization_gender_data.csv
│       └── dataset.xlsx
│       └── dictionary.xlsx
│       └── harmonization_ethnic_data.csv
│       └── data_cleaned.csv
│   ├── Ontology
│       └── Ellas3.1.owl
│   ├── Images
│       └── AE (Análise Exploratória)
│   └── Source
│       └── 1 - Limpeza e tratamento.ipynb
│       └── 2 - Análise Exploratória.ipynb
│   └── README.md
```

**Descrição dos Arquivos:**

- `ELLAS/Data`: Contém os dados utilizados na análise.
  - `Ethnic`: Contém os dados usados para harmonização étnica.
    - `harmonization_ethnic_data.csv`: Dados de harmonização étnica.
  - `Gender`: Contém os dados usados para normalização dos gêneros.
    - `normalization_gender_base.csv`: Dados base para normalização de gênero.
    - `normalization_gender_data.csv`: Dados de normalização de gênero.
  - `/dataset.xlsx`: Conjunto de dados da Survey ELLAS.
  - `/dictionary.xlsx`: Dicionário de dados, com a descrição das variáveis e seus significados.
  - `data_cleaned.csv`: Conjunto de dados limpo e tratado, pronto para análise.
- `ELLAS/Ontology`: Contém a ontologia utilizada na análise.
  - `Ellas3.1.owl`: Ontologia ELLAS, que descreve as classes e propriedades dos dados.
- `ELLAS/Images`: Contém imagens geradas durante a análise.
  - `AE (Análise Exploratória)`: Imagens geradas durante a análise exploratória dos dados.
- `ELLAS/Source`: Contém os códigos e scripts utilizados na análise.
  - `1 - Limpeza e tratamento.ipynb`: Notebook com o código para limpeza e tratamento dos dados.
  - `2 - Análise Exploratória.ipynb`: Notebook com o código para a análise exploratória dos dados.
- `ELLAS/README.md`: Arquivo com a descrição do projeto e da estrutura de arquivos.

## Metodologia:

Todos os dados foram processados utilizando Python 3.10 e as bibliotecas Pandas, Matplotlib e Seaborn. Os dados foram analisados utilizando Jupyter Notebook com o ambiente Anaconda. A análise foi realizada em um ambiente virtual com as seguintes bibliotecas instaladas:

```bash
pip install panda matplotlib seaborn
```

A análise foi dividida em quatro etapas principais: limpeza e tratamento dos dados, e análise exploratória, visualização e análise dos dados. A seguir, apresentamos um resumo de cada etapa:

### Limpeza e Tratamento dos Dados:

Nesta etapa, os dados foram carregados e verificados quanto à presença de valores ausentes, inconsistências e erros. As variáveis foram identificadas com o auxilio do dicionario fornecido para facilitar a leitura e compreensão. Os dados foram normalizados e padronizados, conforme necessário, para garantir a consistência. Além disso, foram aplicadas técnicas de harmonização étnica para garantir a comparabilidade dos dados entre os diferentes países, utilizando o arquivo `harmonization_ethnic_data.csv` como referência. Outra alteração foi a criação de duas novas colunas, uma representando o estado e outra a cidade de residência, a partir das respectivas colunas de cada pais.

### Análise Exploratória:

Nesta etapa, foram realizadas análises descritivas e estatísticas dos dados, com o objetivo de identificar padrões, tendências e relações entre as variáveis. Foram gerados gráficos e tabelas para facilitar a visualização dos resultados. A visualização dos gráficos nos permitiu identificar problemas de qualidade ds dados, como colunas não normalizadas nas variáveis de gênero, curso superior, pós graduação, mestrado, doutorado e pós doutorado. Além disso, foram identificados outros problemas, como a presença de valores ausentes e alguns outliers em campos como quantidade de filhos, idade e tempo de experiência.

#### Soluções para os problemas identificados:
Com base em padrões e definições reconhecidos internacionalmente, adotamos as categorias de gênero e orientação sexual a seguir por estarem fundamentadas em documentos e campanhas oficiais de organismos das Nações Unidas. No relatório *School-related violence and bullying on the basis of Sexual Orientation and Gender Identity or Expression (SOGIE)* (UNESCO, 2018), utiliza-se o conceito SOGIE para englobar orientação sexual, identidade de gênero e expressão de gênero, o que justifica categorias como **Lésbica**, **Gay**, **Bissexual**, **Heterossexual**, **Panssexual**, **Asexsual**, **Queer** e **Interssexual** (UNESCO, 2018). No guia *Safe, Seen and Included* (UNESCO, 2016), reforça-se a necessidade de inclusão de identidades de gênero não conformes, sustentando as categorias **Cisgênero**, **Transgênero** e **Não binario** (UNESCO, 2016). A campanha *UN Free & Equal* do Alto Comissariado das Nações Unidas para os Direitos Humanos destaca a importância de expressões emergentes e aliadas, fundamentando **Outra expressão** e **Prefito não responder** como opções que respeitam a autodeterminação e o direito à não divulgação (OHCHR, 2018). Por fim, o manual técnico *Bringing it Out in the Open* (UNESCO, 2019) recomenda oferecer alternativa de “No informado” para registros em branco ou situações em que a autoidentificação não pôde ser capturada (UNESCO, 2019).

A seguir, apresentamos a classificação das categorias finais segundo os componentes SOGIE (UNESCO, 2018):

**Identificação de gênero**  
- **Cisgênero**: pessoa cuja identidade de gênero corresponde ao sexo atribuído no nascimento.  
- **Transgênero**: pessoa cuja identidade de gênero difere do sexo atribuído ao nascer.  
- **Não binario**: pessoa que não se identifica exclusivamente como hombre ou mujer.  
- **Interssexual**: pessoa com variações de características sexuais biológicas (sex characteristics) que não se encaixam nas categorias típicas de “masculino” ou “feminino” (UNESCO, 2018).

**Expressão de gênero**  
- **Queer**: termo-guarda-chuva para expressões e identidades de gênero não normativas, incluindo pessoas em processo de questionamento.  
- **Gênero fluido**: pessoa cuja expressão de gênero varia ao longo do tempo, desafiando categorias fixas (UNESCO, 2016).

**Orientação sexual**  
- **Lésbica**: mulher que sente atração afetiva ou sexual por outras mulheres.  
- **Gay**: homem que sente atração afetiva ou sexual por outros homens.  
- **Bissexual**: atração afetiva ou sexual por mais de um gênero.  
- **Panssexual**: atração independentemente de gênero.  
- **Assexual**: pouca ou nenhuma atração sexual.  
- **Heterossexual**: atração por pessoas de gênero diferente.  
- **Demissexual**: atração sexual que ocorre apenas após formação de vínculo afetivo, integrando categorias complementares de orientação (UNESCO, 2019).

**Outros metadatos**  
- **Prefiro não responder** e **Não informado**: alternativas de não divulgação ou falha de resposta.  
- **Outra expressão**: identidades emergentes ou não enquadradas nas categorias acima.

Essa divisão segue integralmente os componentes Sexual Orientation, Gender Identity, Gender Expression e Sex Characteristics definidos pela UNESCO para a análise SOGIE (UNESCO, 2018; UNESCO, 2016).

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