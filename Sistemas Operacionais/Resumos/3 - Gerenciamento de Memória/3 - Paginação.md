## Como organizar a tabela de páginas?

_Contexto:_ Com tabelas de páginas grandes, o armazenamento se torna um problema devido ao espaço ocupado. Para resolver isso, pode-se quebrar a tabela em partes menores.

---

### Solução 1 – Paginação hierárquica

Quebra a tabela de páginas em vários pedaços, ou seja, **a própria tabela é paginada**.

- A tabela de um processo é dividida em:
    
    - Tabela externa
        
    - Tabela interna
        
- Apenas as partes necessárias permanecem em memória.
    

#### Endereçamento em dois níveis

Utiliza duas estruturas:

- **PT1** (10 bits): índice da tabela externa
    
- **PT2** (10 bits): índice da tabela interna
    
- **Offset**: deslocamento dentro da página
    

---

### Solução 2 – Tabela de páginas em hash

Utiliza uma **função hash** para encontrar o índice da tabela.

- A entrada da função hash é a página virtual.
    
- O resultado identifica o frame correspondente na tabela.
    

---

### Solução 3 – Tabela de páginas invertida

Ao contrário da tabela tradicional, a invertida usa como índice os **quadros físicos**.

- **Tabela tradicional**:
    
    - Índice = página virtual → valor = quadro físico
        
- **Tabela invertida**:
    
    - Índice = quadro físico → valor = (processo, página virtual)
        

#### Desvantagem

Para acessar a página virtual **p** do processo **n**, é necessário **procurar na tabela inteira** pelo par (n, p), o que pode ser lento.

#### Solução: TLB + Hashing

- **TLB (Translation Lookaside Buffer)**:
    
    - Armazena traduções mais acessadas, evitando leitura na tabela.
        
- **Hashing da página virtual**:
    
    - Usa uma função hash no endereço virtual.
        
    - Cada bucket armazena uma lista encadeada de páginas com o mesmo valor de hash.
        
    - Acelera a busca, pois examina apenas 1 ou 2 entradas.
        

---

## Alocação de páginas

É o processo de definir quais quadros da memória física serão usados pelas páginas de um processo.

---

### Alocação fixa

O sistema operacional atribui um número **fixo** de quadros para cada processo.

#### Características

- Número de quadros é pré-definido.
    
- O processo substitui páginas quando precisa de mais.
    
- Usa algoritmos como **LRU** (Least Recently Used) ou **FIFO**.
    

#### Exemplo prático

- Processo P1 recebe 4 quadros.
    
- Pode manter até 4 páginas virtuais na memória física.
    
- Ao acessar uma 5ª página, precisa **remover uma das anteriores**.
    

#### Vantagens

- Simples de implementar.
    
- Menor sobrecarga de gerenciamento.
    
- Evita que um processo consuma toda a RAM.
    

#### Desvantagens

- Pode gerar muitos page faults.
    
- Desperdício de quadros se o processo usar menos que o fixo.
    
- Não se adapta ao uso real do processo.
    

---

### Alocação dinâmica

A quantidade de quadros varia conforme a necessidade do processo durante a execução.

#### Funcionamento

- O processo inicia com um número inicial de quadros.
    
- Se houver muitos page faults, o sistema **realoca quadros de outros processos** menos exigentes para o que precisa mais.
    

#### Exemplo prático

- P1 e P2 começam com 4 quadros cada.
    
- P1 tem muitos page faults → precisa de mais memória.
    
- P2 está ocioso → sistema tira 2 quadros de P2 e dá a P1.
    

#### Critérios para ajuste

- Frequência de page faults.
    
- Tempo de uso da CPU.
    
- Quantidade de quadros livres.
    
- Algoritmos como **WSClock** ou **Working Set**.
    

#### Vantagens

- Mais eficiente e adaptável.
    
- Reduz page faults.
    
- Melhor uso da memória física.
    

#### Desvantagens

- Implementação mais complexa.
    
- Pode haver fragmentação.
    
- Sobrecarga com realocações frequentes.
    
