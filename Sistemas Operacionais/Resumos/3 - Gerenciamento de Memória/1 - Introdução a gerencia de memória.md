
## Dream Techs (Tecnologias dos sonhos)

Representam os desejos ideais de programadores quanto à memória principal de um sistema. Esses desejos se resumem em quatro requisitos:

- Grande
    
- Rápida
    
- Não volátil
    
- Baixo custo
    

> ⚠️ Esses requisitos são, até hoje, impossíveis de alcançar simultaneamente com as tecnologias atuais.

---

## Hierarquia de Memória

Na arquitetura de computadores, a memória é organizada em **níveis hierárquicos**, normalmente representados em forma de pirâmide:

![Hierarquia de memória](Pasted%20image%2020250608192639.png)

As memórias no topo são:

- Mais rápidas
    
- Mais próximas ao processador
    
- Com menor capacidade
    

As memórias na base:

- São mais lentas
    
- Possuem maior capacidade
    
- São **não voláteis** (persistem mesmo sem energia)
    

---

## Gerenciador de Memória

### Multiprogramação

A multiprogramação ocorre em sistemas com múltiplos núcleos (multi-core), permitindo múltiplos processos simultâneos.

#### Como armazenar N processos em memória?

Dividindo a memória em **N partições** fixas. Ao chegar um novo processo:

- Ele entra em uma fila.
    
- É alocado na primeira partição disponível.
    

> ❗ **Desvantagem:** Se o processo ocupa menos espaço que a partição, o restante da memória é desperdiçado.

#### Como dar a cada programa seu próprio espaço de endereços?

Usa-se registradores **base** e **limite** para proteger os espaços:

- Exemplo: Programa de 40KB armazenado no endereço 20
    
    - Base = 20
        
    - Limite = 20 + 40 = 60
        

> Com isso, cada processo tem seu próprio intervalo de endereços.

---

### O que é MMU?

**MMU (Memory Management Unit)** é um hardware responsável por:

- Converter **endereços virtuais (lógicos)** em **endereços físicos**.
    

> A memória virtual oferece a sensação de memória infinita, mas está limitada pela capacidade física do sistema.

---

## Memória Particionada

### Tipos

- **Partições fixas**
    
    - Simples
        
    - Tamanho fixo
        
    - **Mais desperdício**
        
- **Partições variáveis**
    
    - Alocação dinâmica
        
    - **Menor fragmentação interna**, mas **maior fragmentação externa**
        
    - Acontece em tempo de execução
        

---

### Swapping

Processo de mover dados entre a memória principal e a secundária (disco).

- **Swap-in**: disco → memória principal
    
- **Swap-out**: memória principal → disco
    

> 🧠 Usado para liberar espaço na RAM, movendo dados inativos para o disco.

---

## Estruturas para Gerenciar Memória

![Estruturas de Gerenciamento](Pasted%20image%2020250608213543.png)

### 1. Mapa de Bits (Bitmaps)

- A memória é dividida em unidades fixas.
    
- Cada unidade é representada por **1 bit**:
    
    - `0`: livre
        
    - `1`: ocupada
        

### 2. Lista Encadeada (Linked List)

- Lista ligada com segmentos de memória.
    
- Cada nó contém:
    
    - ID do processo
        
    - Início e fim da alocação
        
- Espaços não utilizados são marcados com `H` (Hold)
    

---

## Algoritmos de Alocação

- **Primeira escolha**
    
    - Escolhe a **primeira partição** disponível com tamanho adequado.
        
- **Melhor escolha**
    
    - Escolhe a **menor partição possível** que ainda comporta o processo.
        
- **Pior escolha**
    
    - Escolhe a **maior partição** (menos eficiente devido ao desperdício).
        

---

👉 Próximo capítulo: Sobre memórias virtuais

[[2 - Sobre memórias virtuais]]

---
