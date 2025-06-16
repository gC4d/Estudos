
## Busca de páginas

Busca de páginas é o processo de descobrir onde está uma página virtual específica na memória física, quando o processador acessa o endereço virtual.
### Passo a passo da busca de página

1. **Endereço virtual** é gerado pela CPU (por exemplo, ao acessar uma variável).
2. O endereço virtual é dividido em:
    - **Número da página virtual (VPN)**.
    - **Deslocamento (offset)** dentro da página.
3. A MMU (Unidade de Gerenciamento de Memória) precisa **traduzir o número da página virtual (VPN)** para o **número do quadro físico (PFN)**.
4. Essa tradução pode acontecer de três formas:
##### 1. **TLB (Translation Lookaside Buffer)**

- Primeiro, o sistema verifica se a página está na **TLB**.
- A TLB é uma **memória cache especial de alta velocidade**, contendo mapeamentos recentes de VPN → PFN.
- Se encontrar a página na TLB (**TLB hit**):
    - A tradução é imediata.    
    - Soma-se o offset ao endereço físico.  
- Se **não encontrar** (**TLB miss**), vai para o próximo passo.
##### 2. **Tabela de Páginas (Page Table)**

- A MMU consulta a **tabela de páginas** na memória principal.
- A tabela informa se a página está:
    - Presente na memória RAM (com o número do quadro físico).
    - Ou está **ausente** (foi movida para o disco/swap).
- Se a página estiver presente:
    - Faz a tradução VPN → PFN.
    - Insere a entrada na TLB (se houver espaço).
- Se a página estiver ausente (**page fault**), vai para o próximo passo.\

##### 3. **Busca no Disco (Page Fault Handler)**

- O sistema operacional é chamado para **carregar a página do disco para a RAM**.
- Escolhe-se um quadro de página (pode exigir substituição de alguma página atual).
- A tabela de páginas e a TLB são atualizadas.
- A instrução é **repetida**, agora com a página presente.

#### Como otimizar a busca?

- **Manter a TLB atualizada** com páginas frequentemente usadas.
- Usar **algoritmos de substituição de página** eficientes (ex: LRU, Clock).    
- Evitar page faults com estratégias como o **conjunto de trabalho (working set)**.