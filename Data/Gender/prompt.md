**Resumo Revisado do Pipeline de Normalização da Coluna `D3_gender`**

1.  **Extração de valores únicos e Correção ortográfica**

    - Carregamos o CSV original e extraímos todas as respostas distintas da coluna `D3_gender`, capturando erros de digitação, variações de idioma e termos não relacionados.
    - Para cada valor único e levando em conta o campo `Country` (idioma da resposta), aplicamos o serviço interno do LLM para normalização, corrigindo acentos, grafias e harmonizando português e espanhol.

      _Prompt:_

      ```
      “Execute a **Etapa 1 – Extração e correção ortográfica** da variável `D3_gender` da seguinte forma:

      Abra o arquivo `normalization_gender_base.csv` e armazene ele em um dataframa em seguida, para cada registro:
      1. Extraia todos os valores **únicos** de `D3_gender`, incluindo `NaN` e strings vazias.
      2. Para cada valor único, utilize a **coluna** `Country` para inferir o idioma (português ou espanhol) e aplique o **serviço interno de correção ortográfica** (que corrige acentuação, capitalização, erros de digitação e harmoniza português ↔ espanhol).
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
