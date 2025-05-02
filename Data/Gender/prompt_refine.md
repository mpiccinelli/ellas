**Revisão da Etapa de Correção Ortográfica (Spelling) – Do Prompt Inicial à Solução Final**

Esse histórico documenta as dificuldades — núcleo dos scripts versus serviço interno, problemas de prompts iniciais pouco claros, as decisões de refinamento que levaram a um processo de correção ortográfica transparente e reproduzível.

> **Observação:** Este documento é a documentação da etapa de correção ortográfica (spelling) tal qual foi realizada. Entretanto, nos testes de reprodutibilidade, o modelo não conseguiu reproduzir o mesmo resultado. Para garantir a reprodutibilidade, o modelo precisou ser ajustado para seguir o fluxo de trabalho definido. O resultado final foi satisfatório, e o processo de refinamento do prompt reprodutível esta documentado no arquivo [`Prompt_reproduction.md`](../Gender/Reproduction/Prompt_reproduction.md)

1.  **Identificação do objetivo e primeiros comandos**

    - **O que queríamos:** Aplicar uma correção ortográfica na coluna `D3_gender` que corrigisse acentos, capitalização e erros de digitação, levando em conta o idioma indicado em `Country`.

      **Prompt:**

      ```
         Preciso que corrija cada um dos temos digitados erroneamente, atenção que alguns estão em espanhol e outros em portugues, corrija e mantenha no idioma original. Segue lista de textos para correção:
         ['Masculino' 'Femenino' 'No binario' 'No sabe' 'Genderqueer' 'Transgénero'
         'Feminino' 'Mulher' 'Heterossexual' 'FEMININO' 'homesexual' 'mulher' 'feminino' 'hetero' 'eminino' 'Heterosexual' 'hétero' 'Homem' 'Etero'
         'Feminino - Hétero Cisgênero' 'Mulher CIS' 'Hétero' 'Mulher cis' 'Masc' ...]
      ```

    - **O que o LLM fez:** O LLM tentou criar um dicionário de correção ortográfica usando um mapa de `replace` fixo, que não contemplava todos os casos de erro. Ele não considerou o idioma e não chamou o "serviço interno" de correção ortográfica, resultando em erros de digitação e inconsistências.

    - **Problema encontrado:** O prompt não estava claro sobre como o LLM deveria lidar com a correção ortográfica, levando a confusões sobre o uso de scripts fixos e dicionários manuais. Esse dicionário ainda não existia e acabou sendo gerado automaticamente pelo LLM com alguns valores parciais, e que desconsideram o idioma a ser usado na correção.

    - **Solução:**: Corrigir o prompt para o LLM. Ele deveria ter chamado o serviço interno de correção ortográfica (seu próprio contexto) para aplicar a lógica de correção, usando `Country` como referência.

2.  **Interpretações equivocadas e dúvidas surgidas**

    **Prompt:**

    ```
       O serviço interno de correção ortográfica deve ser chamado para corrigir os erros de digitação e acentuação. O idioma a ser usado na correção é o indicado na coluna `Country`. O dicionário de conferência (original → corrigido) será gerado automaticamente pelo LLM baseado em seu contexto.
    ```

    - **O que o LLM fez:** Em várias ocasiões o modelo tentou usar apenas scripts fixos (substituições manuais ou `replace`) em vez de chamar explicitamente o “serviço interno” nos valores únicos.

    - **Problema encontrado:** O modelo insistia em usar um dicionário fixo, mesmo quando o prompt indicava que ele deveria chamar o serviço interno. Isso gerou confusão e inconsistências, pois o dicionário não contemplava todos os casos de erro e não considerava o idioma.

    - **Solução:**: Refinar o prompt para que o LLM chamasse o serviço interno de correção ortográfica, garantindo que ele aplicasse a lógica correta de acordo com o idioma indicado em `Country`. Como o modelo insistia em usar um dicionário fixo, foi necessário criar um dicionário de conferência (original → corrigido) baseado no contexto do LLM.

3.  **Aperfeiçoamento do prompt e definição do fluxo**

    **Prompt:**

         ```
            Vamos tentar novamente. O objetivo é corrigir a coluna `D3_gender` do CSV, levando em conta o idioma indicado na coluna `Country`. O fluxo de trabalho deve ser o seguinte:
            1. **Carregar** o CSV base.
            2. **Extrair** valores únicos de `D3_gender`, incluindo nulos.
            3. **Inferir** idioma via `Country`para cada valor único.
            4. **Chamar** o serviço interno (seu contexto) de correção ortográfica (padronizando acentuação/capitalização e corrigindo erros). Faça essa correção para cada valor único, respeitando o idioma e como se estivesse corrigindo um texto inserido pelo usuário.
            5. **Gerar** um DataFrame temporário “`original_value` → `corrected_value`” com os valores únicos corrigidos para ser usado como dicionário de conferência.
            6. **Criar** uma nova coluna `Spelling` no DataFrame original, aplicando o mapeamento do dicionário de conferência.
            7. **Salvar** o arquivo final como `normalization_gender_spelling.csv`, contendo todas as colunas originais mais a nova coluna `Spelling`.
         ```

    - **O que o LLM fez:** O LLM seguiu o fluxo de trabalho definido, carregando o CSV, extraindo os valores únicos de `D3_gender`, inferindo o idioma via `Country`, chamando o serviço interno para correção ortográfica e gerando o DataFrame temporário com os valores corrigidos. Ele disponibilizou as 153 linhas do dicionário (original → corrigido) de forma interativa, permitindo a validação dos resultados. E perguntando se poderia serguir com a criação da nova coluna `Spelling` no DataFrame original.

    - **Problema encontrado:** Alguns termos não foram corrigidos, como `Femeninofeminino`e `Homem Sis`, que não foram reconhecidos como erros de digitação.

    - **Solução:** Como foram apenas dois casos, optamos por solicitar a correção pontual desses termos especificamente, e manter o restante. Isso removeu ambiguidades sobre uso de scripts, dicionários manuais, linguagens de programação e dicionários fixos.

4.  **Implementação e testes**

    - O LLM carregou com sucesso o arquivo, extraiu valores únicos, aplicou o mapeamento via dicionário (que representava o output do serviço interno) e criou a coluna `Spelling` no DataFrame original.
    - Validamos interativamente no painel, garantindo que termos como `Femeninofeminino`e `Homem Sis`, variantes acentuadas e erros de digitação fossem convertidos corretamente.

5.  **Conclusão da etapa**
    - **Arquivo final:** `normalization_gender_spelling.csv`, contendo todas as colunas originais mais `Spelling`.
    - **Critérios atendidos:**
      - Correção ortográfica baseada no idioma de cada entrada;
      - Manutenção da coluna original para rastreabilidade;
      - Geração de um dicionário de conferência (original → corrigido), auditável.
