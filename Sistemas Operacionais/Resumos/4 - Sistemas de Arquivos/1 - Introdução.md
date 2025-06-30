Todos as aplicações de computador necessitam armazenar e recuperar informações. Armazenar dados somente em memória é limitado em temporário: os dados são perdidos quanto o processo termina ou falha. Além disso, vários processos podem precisar acessar os mesmos dados ao mesmo tempo, o que não é possível se esses dados estiverem restritos a um único processo.

Para resolver esses problemas, surgem os três requisitos principais para o armazenamento de longo prazo:
1. Capacidade de armazenar grandes volumes de dados.
2. Persistência dos dados mesmo após o fim dos processos.
3. Acesso simultâneo por múltiplos processos.

Dispositivos como **discos magnéticos** e **unidades de estado sólido (SSD's)** são usados para esse fim, pois permitem acesso persistente e aleatório aos dados. No entanto, operações diretas de leitura e escrita em blocos de disco são complexas e pouco práticas, especialmente em sistemas com muitos usuários e aplicações.

A solução então é uma nova abstração: o **Arquivo**. Arquivos são unidades lógicas de informação criadas e manipuladas por processos, armazenadas de forma persistente no disco. Eles são gerenciados pelo **sistema de arquivos**, parte do sistema operacional responsável por como os arquivos são organizados, nomeados, acessados, protegidos e armazenados.