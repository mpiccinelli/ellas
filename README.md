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
  - `/dataset.xlsx`: Conjunto de dados da Survey ELLAS.
  - `/dictionary.xlsx`: Dicionário de dados, com a descrição das variáveis e seus significados.
  - `harmonization_ethnic_data.csv`: Dados de harmonização étnica.
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
Para as colunas não normalizadas (gênero, curso superior, pós graduação, mestrado, doutorado e pós doutorado), utilizamos um llm (large language model) para normalizar os dados, garantindo que todas as entradas fossem consistentes e seguissem o mesmo padrão. O LLM foi utilizado para corrigir erros de digitação e formatação, além de padronizar as respostas. Neste ponto carregamos para o contexto do LLM o arquivo com o dicionário de dados para referência textual do significado de cada variável, o dataset limpo e o arquivo OWL com a ontologia ELLAS, que descreve as classes e propriedades dos dados existentes na plataforma. Como a ontologia já possuia valores normalizados para as variáveis problemáticas, a idea era utilizar o LLM para fazer a normalização dos dados, utilizando a ontologia como referência. O LLM foi utilizado para gerar um arquivo CSV com os dados normalizados, que foi posteriormente carregado no dataset limpo.

## Resultados:

## Conclusões:

## Contribuições:

## Agradecimentos:

## Referências:

- Maciel, C., Guzman, I., Berardi, R., Caballero, B. B., Rodriguez, N., Frigo, L., Salgado, L., Jimenez, E., Bim, S. A. and Tapia, P. C. (2023) “Open Data Platform to Promote Gender Equality Policies in STEM”, In Proceedings of the Western Decision Sciences Institute (WDSI). April 2023. Portland Oregon, EUA.

- Berardi, R., Auceli, P., Maciel, C., Davila, G., Guzman, I., & Mendes, L. (2023). ELLAS: Uma plataforma de dados abertos com foco em lideranças femininas em STEM no contexto da América Latina. In Anais do XVII Women in Information Technology, (pp. 124-135). Porto Alegre: SBC. doi:10.5753/wit.2023.230764
