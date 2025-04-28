## Sistema Operacionais
****
Camada de software que opera entre  o hardware e os programas de aplicativos
- Estruturas de software amplas e complexas
	- Aspectos de baixo nível (Drivers)
	- Aspectos utilitários e interfaces gráficas
#### Abstração de recursos

**Abstrair**: prover interfaces simples e homogêneas 
- Simplificar o usa das interfaces de baixo nível
- Tornar os aplicativos independestes do hardware
- acesso homogêneo a dispositivos e tecnologias distintas

#### Gerência de recursos

**Gerenciar**: coordenar o uso dos recursos pelos programas
- Permitir o uso compartilhado do processador
- Sequenciar acesso a certos recursos (Ex. impressora)
- Impedir ataques de negação de serviço

#### Áreas de gerência

**Processador**: executar as tarefas dos usuários e do sistema.
**Memória**: fornecer áreas de memória isoladas para as aplicações
**Dispositivos**: configurar e criar abstrações de dispositivos físicos
**Arquivos**: criar e manter arquivos de diretórios
**Proteção**: definir e garantir regras de acesso aos recursos

**Outras áreas**: interface gráfica, suporte de rede, multimídia, energia, localização, etc.

#### Tipos de sistemas operacionais

**Batch**: executa tarefas sequenciais (transações, etc)
**De rede**: executa recursos em outros computadores
**Distribuído**: acessa recursos de forma transparente
**Multiusuário**: cada recurso tem um "dono" e regras de acesso 
**Servidor**: gestão eficiente de grandes volumes de recursos
**Desktop**: interface gráfica e suporte a interatividade
**Móvel**: gestão de energia, conectividade e sensores
**Embarcado**: hardware com poucos processos e energia
**Tempo real**: tem comportamento temporal previsível; pode ser soft real-time ou hard 
real-time
