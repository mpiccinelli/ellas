**Resumo Revisado do Pipeline de Normalização das Colunas `D9_3_1_O_college_area_other`, `D9_3_2_O_master_area_other`, `D9_3_3_O_doctorate_area_other`e `D9_3_4_O_postdoc_area_other`**

1.  **Extração de valores únicos e Correção ortográfica**

    - Carregamos o CSV original e extraímos todas as respostas distintas das colunas `D9_3_1_O_college_area_other`, `D9_3_2_O_master_area_other`, `D9_3_3_O_doctorate_area_other`e `D9_3_4_O_postdoc_area_other`, capturando erros de digitação e variações de idioma.
    - Para cada valor único e levando em conta o campo `Country` (idioma da resposta), aplicamos o serviço interno do LLM para normalização, corrigindo acentos, grafias e harmonizando português e espanhol.

      _Prompts:_

      ```
      Seguem os dados originais (normalization_course_base.csv).
      • Abra o arquivo usando encoding='utf-8-sig' e separador ;.
      • Crie a coluna  Language: Brasil → PT-br; Peru/Bolívia → ES.
      • Concatene os dados das colunas `D9_3_1_O_college_area_other`, `D9_3_2_O_master_area_other`, `D9_3_3_O_doctorate_area_other`e `D9_3_4_O_postdoc_area_other`.
      • Para cada idioma, liste TODOS os valores únicos do resultado da concatenação entre as colunas `D9_3_1_O_college_area_other`, `D9_3_2_O_master_area_other`, `D9_3_3_O_doctorate_area_other`e `D9_3_4_O_postdoc_area_other` e mostre-os em uma tabela interativa.
      ```

      ```
      Quais e quantos são os termos únicos em espanhol?
      ```

      ```
      Corrija todos os termos únicos em espanhol: grafia, acentuação, capitalização e expansão de abreviações. Apresente a tabela original×corrigido e, ao fim, a lista final de termos corretos.
      ```

      ```
      Agora faça o mesmo para o português: identifique todos os termos únicos em PT-br e informe o total.
      ```

      ```
      Corrija os 226 termos em português quanto a grafia, acentuação, capitalização e expansão de abreviações. Mostre tabela original×corrigido e a lista consolidada.
      ```

      ```
      Usando os dicionários finais ES + PT-br, crie no dataset original as colunas `D9_3_1_O_college_area_other_spelling`, `D9_3_2_O_master_area_other_spelling`, `D9_3_3_O_doctorate_area_other_spelling`e `D9_3_4_O_postdoc_area_other_spelling`,  com o termo corrigido correspondente a cada valor em sua coluna original, posicione as colunas "spelling" logo a direita da sua coluna de origem. Salve o arquivo como "normalization_courses_with_spelling.csv" (utf-8-sig, separado por ';'), exiba uma prévia das primeiras linhas e me envie o link para download.
      ```

2.  **Padronização linguística**

    - Extraímos os valores corrigidos e, um a um, usamos o serviço de tradução ao espanhol do LLM (mantendo inalterados os já em espanhol), gerando a coluna D9...`translate_ES`.

      _Prompts:_

      ```
      Seguem os dados originais (normalization_courses_with_spelling.csv).
      • Abra o arquivo usando encoding='utf-8-sig' e separador ;.
      • Crie a coluna  Language: Brasil → PT-br; Peru/Bolívia → ES.
      • Empilhe os dados das colunas `D9_3_1_O_college_area_other_spelling`, `D9_3_2_O_master_area_other_spelling`, `D9_3_3_O_doctorate_area_other_spelling`e `D9_3_4_O_postdoc_area_other_spelling`.
      • Para o idioma português, liste TODOS os valores únicos do resultado da concatenação entre as colunas `D9_3_1_O_college_area_other_spelling`, `D9_3_2_O_master_area_other_spelling`, `D9_3_3_O_doctorate_area_other_spelling`e `D9_3_4_O_postdoc_area_other_spelling` e mostre-os em uma tabela interativa.
      ```

      ```
      Traduza todos os 181 termos encontrados para espanhol. Apresente a tabela original×traduzido.
      ```

      ```
      Usando o dicionário original×traduzido, crie no dataset original as colunas `D9_3_1_O_college_area_other_translate_es`, `D9_3_2_O_master_area_other_translate_es`, `D9_3_3_O_doctorate_area_other_translate_es`e `D9_3_4_O_postdoc_area_other_translate_es`,  com o termo traduzido correspondente em sua coluna `spelling`, posicione as colunas "translate_es" logo a direita da sua coluna de origem (`spelling`). Salve o arquivo como "normalization_courses_with_translated.csv" (utf-8-sig, separado por ';'), exiba uma prévia das primeiras linhas e me envie o link para download.
      ```