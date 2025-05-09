
# Soluções para os problemas identificados:

Com base em padrões e definições reconhecidos internacionalmente, adotamos as categorias de gênero e orientação sexual a seguir por estarem fundamentadas em documentos e campanhas oficiais de organismos das Nações Unidas. No relatório _School-related violence and bullying on the basis of Sexual Orientation and Gender Identity or Expression (SOGIE)_ (UNESCO, 2018), utiliza-se o conceito SOGIE para englobar orientação sexual, identidade de gênero e expressão de gênero, o que justifica categorias como **Lésbica**, **Gay**, **Bissexual**, **Heterossexual**, **Panssexual**, **Asexsual**, **Queer** e **Interssexual** (UNESCO, 2018). No guia _Safe, Seen and Included_ (UNESCO, 2016), reforça-se a necessidade de inclusão de identidades de gênero não conformes, sustentando as categorias **Cisgênero**, **Transgênero** e **Não binario** (UNESCO, 2016). A campanha _UN Free & Equal_ do Alto Comissariado das Nações Unidas para os Direitos Humanos destaca a importância de expressões emergentes e aliadas, fundamentando **Outra expressão** e **Prefito não responder** como opções que respeitam a autodeterminação e o direito à não divulgação (OHCHR, 2018). Por fim, o manual técnico _Bringing it Out in the Open_ (UNESCO, 2019) recomenda oferecer alternativa de “No informado” para registros em branco ou situações em que a autoidentificação não pôde ser capturada (UNESCO, 2019).

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


## Resumo Revisado do Pipeline de Normalização da Coluna `D3_gender`**

1.  **Extração de valores únicos e Correção ortográfica**

    - Carregamos o CSV original e extraímos todas as respostas distintas da coluna `D3_gender`, capturando erros de digitação, variações de idioma e termos não relacionados.
    - Para cada valor único e levando em conta o campo `Country` (idioma da resposta), aplicamos o serviço interno do LLM para normalização, corrigindo acentos, grafias e harmonizando português e espanhol.

      _Prompt:_

      ```
      Esta planilha contem informações de gênero dos participantes de uma pesquisa no Brasil, Peru e Bolívia. O campo `D3_gender` foi coletado como um campo de texto aberto, gerando diversos valores com erros de digitação, faltando letras, sem acentos, ou com acentos em lugares errados, letras maiúsculas e minúsculas misturadas, entre tantos outros erros que inviabilizam o estudo efetivo dos dados dessa coluna. Precisamos normalizar a coluna para permitir a interpretação correta dos dados e, para isso, o primeiro passo será fazer a correção dos textos digitados errados. Preciso que me ajude com este procedimento. Cada termo precisa ser corrigido individualmente conforme o seu idioma de captação (A coluna `Country` indica o país de origem da pergunta e vamos usar ele como referência de idioma para a correção no idioma de entrada de dados, Se o país dor Brasil o idioma a ser usado na correção deverá ser o Português do Brasil, se for Bolívia ou Pero o idioma será o Espanhol). Nesta etapa não podemos alterar o significado da palavra, nem atribuir termos genéricos para valores faltantes, devemos apenas realizar a correção do texto digitado pelo usuário. A seguir as instruções para que você possa realizar o procedimento de correção: 
      
      “Execute a **Etapa 1 – Extração e correção ortográfica** da variável `D3_gender` da seguinte forma:

      Abra o arquivo `normalization_gender_base.csv` e armazene ele em um dataframe em seguida:
      1. Extraia todos os valores **únicos** de `D3_gender` e armazene.
      2. Para cada valor único, utilize a **coluna** `Country` para inferir o idioma (português ou espanhol) e aplique o **serviço interno de correção de texto** (corrigindo acentuação, capitalização, erros de digitação e pontuação conforme seu idioma).
      3. Monte um **DataFrame** secundario com duas colunas:
         - `original_value`: valor bruto extraído de `D3_gender`
         - `corrected_value`: saída do serviço interno de correção
      4. Use este dataframe como dicionário para corrigir os valores da coluna `D3_gender` do dataframe original, criando uma nova coluna `Spelling` a direita do campo `D3_gender`.
      5. Ao final, exiba a tabela resultante e forneça o link para download de deste dataframe com o nome `normalization_gender_spelling.csv`.
      ```

2.  **Padronização linguística**

    - Extraímos os valores corrigidos e, um a um, usamos o serviço de tradução ao espanhol do LLM (mantendo inalterados os já em espanhol), gerando a coluna `Translate_ES`.

      _Prompt:_

      ```
         “Execute a **Etapa 2 – Padronização linguística (Tradução ES)** da variável `D3_gender` da seguinte forma:

         Abra o arquivo **`normalization_gender_spelling.csv`** (resultado da Etapa 1) e carregue-o em um DataFrame. Em seguida:

         1. Extraia todos os valores **únicos** da coluna `Spelling`, garantindo que `NaN` e strings vazias sejam incluídos.
         2. Para cada valor único em `Spelling`, utilize o **serviço interno de tradução** para convertê-lo ao espanhol (deixando inalterados os termos já em espanhol).
         3. Monte um **DataFrame** secundário com duas colunas:
            - `spelling_value`: termo original corrigido ortograficamente;
            - `translation_es`: saída do serviço de tradução ao espanhol.
         4. Use esse DataFrame secundário como **dicionário** para substituir, no DataFrame principal, cada valor de `Spelling` pela sua versão `translation_es`, criando uma nova coluna **`Translation ES`** imediatamente à direita de `Spelling`.
         5. Ao final, exiba a tabela resultante (com as colunas originais mais `Spelling` e `Translatale_ES`) e forneça o link para download desse DataFrame, salvando-o com o nome **`normalization_gender_translation.csv`**.
      ```

3.  **Identificação de sinônimos**

    - Listamos os termos únicos de `Translate_ES`, utilizamos o LLM para normalizar cada string removendo parênteses, hífens, vírgulas e variações de caixa.
    - Agrupamos as variantes sob um **sinônimo canônico** (p. ex. “Femenino Cisgénero” → **Femenino**, “Femenino, Mujer, Hétero” → **Femenino**, ), sem alterar o sentido original, e preenchemos a coluna `Synonyms`.

      _Prompt:_

      ```
         “Execute a **Etapa 3 – Identificação de sinônimos** da variável `D3_gender` da seguinte forma:

         Abra o arquivo **`normalization_gender_translation.csv`** (resultado da Etapa 2) e carregue-o em um DataFrame. Em seguida:

         1. Extraia todos os valores **únicos** da coluna `Translate_ES`, garantindo que `NaN` e strings vazias sejam incluídos.
         2. Para cada valor único, normalize a string removendo acentuação, convertendo para caixa baixa, eliminando parênteses, hífens, vírgulas e espaços extras.
         3. Agrupe todas as variantes (por exemplo, “mujer”, “femenino cisgénero”, “femenino (mujer)”) sob um **sinônimo canônico** único (por exemplo, `Femenino`), sem alterar o sentido original. Termos sem sinônimos foram devem permanecer inalterados.
         4. Monte um **DataFrame** secundário com duas colunas:
            - `translate_es_value`: termo original padronizado em espanhol;
            - `synonym`: sinônimo canônico definido.
         5. Use esse DataFrame secundário como **dicionário** para criar, no DataFrame principal, uma nova coluna **`Synonyms`** imediatamente à direita de `Translate_ES`, mapeando cada valor de `Translate_ES` para seu `synonym`.
         6. Ao final, exiba a tabela resultante (incluindo `Spelling`, `Translate_ES` e `Synonyms`) e forneça o link para download deste DataFrame, salvando-o com o nome **`normalization_gender_synonyms.csv`**.
      ```

4.  **Contextualização**

    - Definir automaticamente, a partir da pergunta sobre gênero do participante, o conjunto de respostas válidas (por ex.: Masculino, Femenino, Gay, Pansexual, No informado etc.).
    - Todo sinônimo fora desse universo foi marcado como **“Fora de contexto”**, gerando a coluna **“Contextualização”**.

      _Prompt:_

      ```
         “Execute a **Etapa 4 – Contextualização** da variável `D3_gender` da seguinte forma:

         Abra o arquivo **`normalization_gender_synonyms.csv`** (resultado da Etapa 3) e carregue-o num DataFrame. Em seguida:

         1. Com base na pergunta “¿Cuál es su género?”, defina automaticamente o **conjunto de respostas válidas** que correspondem a identidades de gênero ou orientações (por exemplo:
            `Masculino`, `Femenino`, `Heterosexual`, `Homosexual`, `Bisexual`, `Pansexual`, `Asexual`, `Demisexual`, `Queer`, `Intersexual`, `Transgénero`, `Agénero`, `No binario`, `Ambos`, `Prefiero no responder`, `No informado`, `Otra expresión`).
         2. Para cada valor na coluna **`Synonyms`**, verifique se está nesse conjunto de válidos:
            - Se **sim**, mantenha o mesmo valor.
            - Se **não**, substitua por **`Fora de contexto`**.
         3. Crie uma nova coluna **`Contextualização`** imediatamente à direita de `Synonyms` e preencha-a com o resultado desse mapeamento.
         4. Ao final, exiba a tabela resultante (incluindo as colunas originais até `Synonyms` e a nova `Contextualization`) e forneça o link para download, salvando este DataFrame como **`normalization_gender_contextualization.csv`**.
      ```

5.  **Categorização SOGIE**

    - Com base na **lista de categorias finais fornecida pelo usuário** e suas definições, mapear cada termo de `Contextualization` para uma das 14 categorias (Cisgénero, Transgénero, No binario, Lesbiana, Gay, Heterosexual, Bisexual, Pansexual, Asexual, Queer, Intersexual, Otra expresión, Prefiero no responder, No informado), criando a coluna `SOGIE`.

      _Prompt:_

      ```
         “Execute a **Etapa 5 – Categorização SOGIE** da variável `D3_gender` da seguinte forma:

         Abra o arquivo **`normalization_gender_contextualization.csv`** (resultado da Etapa 4) e carregue-o em um DataFrame. Em seguida:

         1. Defina um dicionário que mapeie cada valor de **`Contextualização`** para uma das **14 categorias finais** fornecidas:
            - Cisgénero, Transgénero, No binario, Lesbiana, Gay, Heterosexual, Bisexual, Pansexual, Asexual, Queer, Intersexual, Demisexual, Otra expresión, Prefiero no responder, No informado. Para a definição do dicionário, utilize as definições SOGIE da UNESCO.
         2. Aplique esse mapeamento para criar a coluna **`SOGIE`**, onde cada entrada de `Contextualização` recebe sua categoria SOGIE correspondente.
         5. Ao final, exiba a tabela resultante (com todas as colunas originais mais a `SOGIE`) e forneça o link para download, salvando o DataFrame como **`normalization_gender_sogie.csv`**.
      ```

6.  **Classificação nos componentes SOGIE**  
    – Por fim, agrupamos as 14 categorias de `SOGIE` em um dos quatro componentes definidos pela UNESCO:  
    ​ • **Identidad de género** (Cisgénero, Transgénero, No binario, Intersexual)  
    ​ • **Expresión de género** (Queer, Género fluido)  
    ​ • **Orientación sexual** (Lesbiana, Gay, Bisexual, Pansexual, Asexual, Heterosexual, Demisexual)  
    ​ • **Otros metadatos** (Prefiero no responder, No informado, Otra expresión)  
    – Essa classificação gerou a coluna **“SOGIE_Classification”**.

    _Prompt:_

    ```
      “Execute a **Etapa 6 – Classificação nos componentes SOGIE** da variável `D3_gender` da seguinte forma:

      Abra o arquivo **`normalization_gender_sogie.csv`** (resultado da Etapa 5) e carregue-o em um DataFrame. Em seguida:

      1. Defina um dicionário que agrupe cada valor da coluna **`SOGIE`** em um dos quatro componentes SOGIE:
         - **Identidad de género**: Cisgénero, Transgénero, No binario, Intersexual
         - **Expresión de género**: Queer, Género fluido
         - **Orientación sexual**: Lesbiana, Gay, Bisexual, Pansexual, Asexual, Heterosexual, Demisexual
         - **Otros metadatos**: Prefiero no responder, No informado, Otra expresión
      2. Aplique esse mapeamento para criar a coluna **`SOGIE_Classification`**, onde cada entrada de `SOGIE` recebe o seu componente correspondente.
      3. Ao final, exiba a tabela resultante (incluindo todas as colunas originais mais `SOGIE_Classification`) e forneça o link para download, salvando o DataFrame como **`normalization_gender_sogie_classification.csv`**.
    ```

7.  **Exportação final**

    - Por fim, exportamos o DataFrame final com todas as colunas, para um arquivo CSV chamado `normalization_gender_data.csv`, que contém todas as etapas rastreáveis e alinhadas às definições SOGIE da UNESCO.
    - O arquivo CSV final contém as seguintes colunas: `survey_Id`, `Country`, `D3_gender`, `Spelling`, `Translate_ES`, `Synonyms`, `Contextualization`, `SOGIE`, `SOGIE_Classification`.

      _Prompt:_

      ```
         “Execute a **Etapa 7 – Exportação final** da variável `D3_gender` da seguinte forma:

         Abra o arquivo **`normalization_gender_sogie_classification.csv`** (resultado da Etapa 6) e carregue-o em um DataFrame. Em seguida:

         1. Verifique se o DataFrame contém todas as colunas geradas durante as etapas anteriores, na ordem:
            - `survey_Id`, `Country`, `D3_gender`, `Spelling`, `Translate_ES`, `Synonyms`, `Contextualization`, `SOGIE`, `SOGIE_Classification`
         2. Se necessário, reordene as colunas para corresponder exatamente à sequência acima.
         3. Exporte o DataFrame completo para um arquivo CSV chamado **`normalization_gender_data.csv`**, usando `sep=';'`.
         4. Ao final, forneça o link para download de **`normalization_gender_data.csv`**, garantindo que ele contenha todas as etapas rastreáveis e alinhadas às definições SOGIE da UNESCO.”
      ```
