
## O que é a Memória Virtual (MV)?

A memória virtual é uma técnica que utiliza a **memória secundária (como o HD ou SSD)** como uma extensão da **memória principal (RAM)**. Serve como um “cache” para partes de processos.

### Qual a vantagem disso?

Com o aumento do tamanho dos softwares modernos, os processos podem ultrapassar a capacidade da RAM. Com MV:

* Somente **partes ativas** de processos ficam na memória principal.
* As partes inativas ficam armazenadas na **memória secundária**.
* Permite **multiprogramação** eficiente.
* Programas **maiores que a RAM** podem ser executados.

---

## MV e MMU

Para usar a memória virtual, os processos **não acessam endereços físicos diretamente**, e sim **endereços lógicos (virtuais)**. A **MMU (Unidade de Gerenciamento de Memória)** converte esses endereços lógicos em **endereços físicos**.

---

## Técnicas de Memória Virtual

### Paginação

* Quebra o processo em páginas de tamanho fixo (\~4 KB).
* Cada **página** (no disco) mapeia um **frame** (na RAM).

#### Page Fault

Evento quando uma página requisitada **não está na RAM**, exigindo busca no disco.

---

### Tabela de Páginas

Responsável pelo mapeamento entre memória virtual e memória real.

#### Exemplo com imagem:

![Exemplo de tabela de páginas](Pasted%20image%2020250608233057.png)

* Endereço 5 → pertence à **segunda página (0k a 4k)**.
* Essa página está mapeada para o **terceiro frame (8k a 12k)**.
* Conversão: `5 + 8192 = 8197`, o endereço físico.

---

#### Entrada e Saída

* **Entrada**: Página virtual
* **Saída**: Página real

![Mapeamento de páginas](Pasted%20image%2020250608234556.png)

---

#### Busca de Endereços

Feita por **busca sequencial ou binária** — ambas **lentas**.

Exemplo de processo de busca:

![Exemplo de busca](Pasted%20image%2020250608235034.png)

---

### Componentes do Endereço

* **p (número da página)**: índice para tabela de páginas
* **d (deslocamento)**: define o endereço físico

#### Tamanhos de Página:

* **Páginas maiores**: leitura mais eficiente, tabela menor, **maior fragmentação interna**
* **Páginas menores**: menos eficiente, tabela maior, **menos fragmentação interna**

> ✅ **Fragmentação interna**: espaço desperdiçado dentro da partição
> ✅ **Fragmentação externa**: soma dos espaços desperdiçados em múltiplas partições

---

### Componentes da Tabela

* **Page frame number**: endereço real na RAM
* **Bit de residência**: 1 = na RAM | 0 = **page fault**
* **Bit de proteção**: permissões (leitura, escrita, execução)
* **Bit de modificação**: 1 = foi modificada
* **Bit de referência**: 1 = recentemente acessada
* **Bit de cache**: controla se pode ser armazenada em cache

---

### Onde armazenar as Tabelas

* **Array de registradores** (hardware)
* **Memória RAM**: com ajuda da MMU
* **Cache da MMU (associativa)**: aumenta desempenho

#### Registradores necessários:

* BASE da tabela
* TAMANHO da tabela

---

### Problema de Desempenho

A cada acesso:

1. Buscar na tabela
2. Buscar na RAM

> Isso causa **overhead**.

### Solução: TLB (Translation Lookaside Buffer)

TLB é um cache especial da MMU que **acelera a tradução de endereços**, evitando consultar a tabela na RAM toda vez.

---

## Segmentação

Separa o processo em **blocos arbitrários** por tipo de informação:

* Texto
* Imagem
* Áudio
* Código etc.

### Vantagens

* Permite **proteção de acesso por tipo de dado**.
  Exemplo: segmento de código = **somente leitura**, impedindo modificação indevida.

---
