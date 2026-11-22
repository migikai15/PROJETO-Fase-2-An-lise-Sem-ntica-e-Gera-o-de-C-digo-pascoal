======================================================================

PROJETO - COMPILADORES: Fase 2 (Análise Semântica e Geração de Código)

======================================================================



NOME DOS INTEGRANTES:

- Gabriel Tortolio Fonseca - 10416751



1. ESTADO DE CONCLUSÃO DO TRABALHO

O projeto foi totalmente concluído, mantendo todas as funcionalidades da Fase 1 e implementando integralmente os requisitos da Fase 2:



- Fase 1 (Mantida):

  * Expressões regulares e Gramática Livre de Contexto (GLC) documentadas no cabeçalho de `compilador.c`.

  * Analisador léxico com a estrutura original de `Token`, gerando `saida_tokens.txt` e exibindo os tokens no formato `<Linha># <Token> | <Atributo>`.

  * Analisador sintático preditivo descendente recursivo com interrupção em erros léxicos e sintáticos.



- Fase 2 (Análise Semântica):

  * Implementação da minitabela de símbolos usando lista encadeada (`TNo`), armazenando identificador (`ID[16]`), endereço sequencial a partir de `0` e tipo (`tipo[7]`).

  * Implementação da função `busca_tabela_simbolos()` para consulta de endereços e reporte imediato de erro semântico caso o identificador não tenha sido declarado.

  * Verificação completa das regras semânticas exigidas:

    1. Variável utilizada somente após declaração prévia;

    2. Proibição do uso de palavras reservadas como nome de variável, parâmetro ou rotina;

    3. Identificador único e associado ao mesmo tipo ao longo do código;

    4. Verificação de que toda variável declarada que recebeu valor foi utilizada no corpo do programa;

    5. Compatibilidade de tipos em expressões, atribuições, condições e índices;

    6. Compatibilidade de número e tipo dos argumentos em chamadas de rotinas;

    7. Proibição do uso de procedimentos em expressões;

    8. Proibição do uso de funções como procedimentos (fora de expressões/atribuições);

    9. Compatibilidade do valor de retorno (`retorne`) com o tipo declarado na função.



- Fase 2 (Geração de Código Intermediário - MEPA):

  * Implementação da função `proximo_rotulo()` para geração segura de rótulos consecutivos (`L1`, `L2`, ...).

  * Geração do arquivo `saida_mepa.txt` contendo as instruções MEPA correspondentes a todos os comandos, expressões, laços, desvios condicionais e rotinas da linguagem.


2. DECISÕES DE DESIGN E IMPLEMENTAÇÃO

- Minitabela de Símbolos: Estruturada como lista encadeada (`TNo`), com tabela global para o algoritmo principal e lista local para parâmetros e variáveis locais de procedimentos/funções, liberada ao término de cada rotina.

- Precedência de Expressões: A análise de expressões foi estratificada por precedência (`OU`, `E`, operadores relacionais, `+`/`-`, `*`/`/`/`\`/`MOD` e primárias) para validar tipos corretamente e emitir instruções MEPA em ordem pós-fixada.

- Comandos de Controle e Rotinas: Implementados desvios (`DSVF`, `DSVS`, `NADA`) para `se/senao`, `enquanto` e `para` (incluindo suporte a `passo`), além de chamadas e retornos de rotinas (`ENPR`, `AMEM`, `CHPR`, `DMEM`, `RTPR`).

