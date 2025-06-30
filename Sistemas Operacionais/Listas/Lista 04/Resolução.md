### Lista de Exercícios 04

#### Sistema de Arquivos

1. O que é um sistema de arquivos e qual sua função principal?
    
    Um sistema de arquivos é um método e uma estrutura de dados que um sistema operacional utiliza para controlar como os dados são armazenados e recuperados no disco. Sua função principal é organizar e gerenciar arquivos e diretórios, permitindo que os usuários e o sistema operacional acessem e manipulem os dados de forma eficiente e segura.
    
2. **Considere as seguintes técnicas para alocação de arquivos em disco: contínua; com lista encadeada; com lista encadeada utilizando uma tabela na memória (FAT) e indexada (I-Nodes). Comente as principais vantagens e desvantagens de cada uma delas. Defina critérios para determinar qual que tipo de arquivo deveria utilizar qual técnica. Determine um conjunto de características que devem ser consideradas para determinar os critérios, tais como: tamanho do arquivo, quantidade de acessos ao arquivo, tipo de acesso usualmente feito no arquivo (sequencial, aleatório, etc.), tipo de operação realizada no arquivo (leitura, escrita, etc.), dentre outras que você julgar interessante.**
    
    - **Alocação Contínua:**
        
        - **Vantagens:** Acesso sequencial muito rápido, pois os blocos estão adjacentes no disco. Simples de implementar.
            
        - **Desvantagens:** Sofre de fragmentação externa (espaço livre em pequenos pedaços espalhados). Difícil de expandir arquivos. Requer a declaração do tamanho do arquivo antecipadamente.
            
    - **Alocação com Lista Encadeada:**
        
        - **Vantagens:** Não há fragmentação externa, pois os blocos podem estar espalhados. Fácil de expandir arquivos.
            
        - **Desvantagens:** Acesso aleatório lento, pois é preciso percorrer a lista de blocos. Armazenamento de ponteiros consome espaço. Confiabilidade reduzida se um ponteiro estiver corrompido.
            
    - **Alocação com Lista Encadeada utilizando uma Tabela na Memória (FAT):**
        
        - **Vantagens:** Supera o problema do acesso aleatório lento da lista encadeada pura, pois a tabela está na memória. Fácil de expandir arquivos.
            
        - **Desvantagens:** A tabela FAT pode ser grande para discos grandes, consumindo muita memória. Um único ponto de falha (se a FAT for corrompida, o sistema de arquivos é danificado).
            
    - **Alocação Indexada (I-Nodes):**
        
        - **Vantagens:** Acesso aleatório eficiente. Fácil de expandir arquivos (até certo ponto, através de múltiplos níveis de indexação). Melhor para arquivos grandes e pequenos.
            
        - **Desvantagens:** Armazenamento dos blocos de índice (i-nodes) consome espaço. Pode ser mais complexo de implementar.
            
    
    **Critérios para determinar a técnica de alocação e características a considerar:**
    
    - **Tamanho do arquivo:**
        
        - Arquivos pequenos e acessados sequencialmente: Alocação contínua pode ser eficiente.
            
        - Arquivos de tamanhos variados e que crescem dinamicamente: Lista encadeada, FAT ou indexada seriam melhores.
            
        - Arquivos muito grandes: Indexada (I-Nodes) é geralmente a mais adequada devido ao acesso eficiente e expansibilidade.
            
    - **Quantidade de acessos ao arquivo:**
        
        - Arquivos frequentemente acessados aleatoriamente: Alocação indexada (I-Nodes) ou FAT.
            
        - Arquivos acessados principalmente sequencialmente: Alocação contínua ou lista encadeada (com cuidado para o desempenho).
            
    - **Tipo de acesso usualmente feito no arquivo (sequencial, aleatório, etc.):**
        
        - Acesso sequencial: Alocação contínua é ideal.
            
        - Acesso aleatório: Alocação indexada (I-Nodes) ou FAT são preferíveis.
            
    - **Tipo de operação realizada no arquivo (leitura, escrita, etc.):**
        
        - Arquivos que sofrem muitas modificações de tamanho (escrita): Lista encadeada, FAT ou indexada são mais flexíveis.
            
        - Arquivos lidos com frequência, mas pouco modificados: Alocação contínua (se o tamanho for fixo).
            
    - **Necessidade de compactação/desfragmentação:** Sistemas com fragmentação externa (contínua) precisarão de mais manutenção.
        
    - **Recursos de memória disponíveis:** A técnica FAT consome memória para a tabela.
        
    - **Complexidade de implementação:** Alocação contínua é a mais simples, enquanto a indexada é mais complexa.
        
3. **O que aconteceria se o mapa de bits ou a lista de livres contendo a informação sobre blocos livres de disco tivesse sido completamente perdida devido a um desastre? Há algum modo de recuperar o disco desse desastre, ou adeus, disco? Discuta sua resposta, separadamente, para os sistemas de arquivos Unix e para o FAT-16.**
    
    Se o mapa de bits ou a lista de livres (que rastreiam os blocos de disco disponíveis) fossem completamente perdidos, o sistema operacional não saberia quais blocos estão ocupados e quais estão livres. Isso levaria à corrupção generalizada dos dados, pois novos dados poderiam ser gravados sobre dados existentes, e arquivos existentes poderiam ser inacessíveis.
    
    - **Unix (com I-nodes):** Em sistemas Unix, a recuperação é possível, mas difícil. Um utilitário como o `fsck` (File System Check) pode ser usado. Ele percorreria todo o sistema de arquivos, verificando os i-nodes (que contêm ponteiros para os blocos de dados) para determinar quais blocos estão em uso. A partir dessa informação, um novo mapa de bits de blocos livres poderia ser reconstruído. Blocos que não fossem referenciados por nenhum i-node seriam marcados como livres. No entanto, arquivos que estivessem sendo escritos no momento do desastre ou arquivos danificados poderiam ser irrecuperáveis ou recuperados parcialmente como "lost+found". Embora demorado e complexo, não significa "adeus, disco".
        
    - **FAT-16:** A recuperação em FAT-16 seria consideravelmente mais difícil e com menos chances de sucesso completo. A FAT (File Allocation Table) é a estrutura principal que mapeia os clusters de um arquivo. Se a FAT principal e suas cópias (se existirem e se também forem perdidas) forem corrompidas ou perdidas, é extremamente complicado reconstruir a alocação de arquivos. Não há uma estrutura de dados equivalente aos i-nodes do Unix que permita reconstruir a FAT a partir dos metadados dos arquivos. Utilitários de recuperação de dados tentariam varrer o disco em busca de cabeçalhos de arquivos conhecidos e tentar reconstruir a sequência de clusters, mas seria um processo com alta probabilidade de perda de dados e fragmentação. Nesse cenário, a perda da FAT principal e suas cópias significaria, em muitos casos, "adeus, disco" para a maioria dos dados utilizáveis, a menos que haja backups recentes.
        
4. **Como funciona o processo de montagem e desmontagem de um sistema de arquivos?**
    
    - **Montagem:** A montagem é o processo de tornar um sistema de arquivos acessível ao sistema operacional e, consequentemente, aos usuários. Quando um sistema de arquivos é montado, o sistema operacional estabelece uma ligação entre um diretório existente na hierarquia de arquivos (ponto de montagem) e a raiz do sistema de arquivos a ser montado. Isso envolve a leitura de informações de superbloco do sistema de arquivos (que contém metadados essenciais sobre a estrutura do sistema de arquivos) e a integração de sua estrutura de diretórios e arquivos com a hierarquia global do sistema. Após a montagem, os arquivos e diretórios do sistema de arquivos montado aparecem como parte da estrutura de diretórios do sistema.
        
    - **Desmontagem:** A desmontagem é o processo inverso, onde o sistema de arquivos é desconectado da hierarquia do sistema operacional. Antes de desmontar, o sistema operacional garante que todas as operações pendentes (escritas em cache, etc.) sejam concluídas e que nenhum arquivo ou processo esteja utilizando o sistema de arquivos. Uma vez desmontado, o sistema de arquivos não pode mais ser acessado através de seu ponto de montagem e pode ser removido fisicamente do sistema (por exemplo, um pen drive) ou estar pronto para outras operações.
        
5. **O que são permissões de arquivos e por que são importantes?**
    
    Permissões de arquivos são um conjunto de regras que definem quem pode acessar um arquivo ou diretório e que tipo de operações pode realizar sobre ele (leitura, escrita, execução). Elas são importantes por várias razões:
    
    - **Segurança:** Permissões de arquivo ajudam a proteger a integridade e a confidencialidade dos dados, impedindo que usuários não autorizados acessem, modifiquem ou excluam arquivos.
        
    - **Privacidade:** Garantem que informações pessoais ou confidenciais sejam acessíveis apenas aos usuários ou grupos designados.
        
    - **Estabilidade do sistema:** Impedem que usuários ou programas maliciosos danifiquem arquivos essenciais do sistema operacional.
        
    - **Colaboração:** Permitem que múltiplos usuários compartilhem arquivos de forma controlada, definindo quem pode ler, escrever ou executar.
        
    - **Controle de acesso:** Fornecem um mecanismo granular para controlar o acesso aos recursos do sistema.
        
6. **O que é fragmentação de arquivos e como ela pode impactar o desempenho do sistema?**
    
    Fragmentação de arquivos ocorre quando um arquivo é armazenado em pedaços não contíguos (fragmentos) em diferentes locais do disco. Isso geralmente acontece ao longo do tempo, à medida que arquivos são criados, excluídos e modificados, deixando pequenos espaços vazios entre os arquivos. Quando um novo arquivo é criado ou um existente é expandido, o sistema operacional pode precisar armazenar seus dados nesses espaços não contíguos.
    
    A fragmentação pode impactar o desempenho do sistema de várias maneiras:
    
    - **Desempenho de leitura/escrita reduzido:** Para ler ou escrever um arquivo fragmentado, a cabeça de leitura/escrita do disco precisa se mover para múltiplos locais no disco para coletar todos os pedaços, o que aumenta o tempo de busca e a latência rotacional. Isso retarda as operações de E/S.
        
    - **Maior desgaste do hardware:** O movimento excessivo da cabeça do disco devido à fragmentação pode levar a um maior desgaste do drive.
        
    - **Inicialização e carregamento de programas mais lentos:** Arquivos de programas e do sistema operacional fragmentados podem levar mais tempo para serem carregados na memória, resultando em inicializações mais lentas do sistema e dos aplicativos.
        
    - **Uso ineficiente do espaço em disco:** Embora menos comum, em sistemas com muita fragmentação externa, pode haver espaço livre suficiente no total, mas nenhum bloco contíguo grande o suficiente para armazenar um novo arquivo grande.
        
7. **Quais são os principais tipos de sistemas de arquivos e onde são utilizados?**
    
    Existem muitos tipos de sistemas de arquivos, cada um otimizado para diferentes usos e sistemas operacionais. Alguns dos principais incluem:
    
    - **FAT (File Allocation Table):** Família de sistemas de arquivos (FAT12, FAT16, FAT32, exFAT) usada historicamente em DOS e Windows. FAT32 é ainda comum em pendrives e cartões de memória por sua ampla compatibilidade. exFAT é otimizado para mídias flash e suporta arquivos maiores que 4GB.
        
    - **NTFS (New Technology File System):** O sistema de arquivos padrão para Windows NT e todas as versões modernas do Windows. Oferece recursos avançados como segurança robusta (permissões), recuperação de falhas, compressão de arquivos, criptografia e suporte a arquivos e volumes muito grandes.
        
    - **ext (Extended File System):** A família de sistemas de arquivos padrão para Linux (ext2, ext3, ext4).
        
        - **ext2:** Antigo, sem journaling.
            
        - **ext3:** Adiciona journaling (melhora a resiliência a falhas) ao ext2.
            
        - **ext4:** A versão mais recente e comum no Linux, com melhor desempenho, suporte a volumes maiores e mais recursos.
            
    - **APFS (Apple File System):** O sistema de arquivos padrão para macOS, iOS, tvOS e watchOS. Projetado para SSDs e otimizado para criptografia e gerenciamento de espaço.
        
    - **HFS+ (Hierarchical File System Plus):** O sistema de arquivos anterior da Apple, ainda encontrado em alguns dispositivos mais antigos.
        
    - **UFS (Unix File System):** Um sistema de arquivos amplamente utilizado em sistemas Unix e tipo Unix (FreeBSD, OpenBSD, Solaris).
        
    - **ZFS (Zettabyte File System):** Desenvolvido pela Sun Microsystems, é um sistema de arquivos e gerenciador de volumes lógicos combinado. Oferece recursos avançados como integridade de dados por checksums, pooling de armazenamento, snapshots, clones e escalabilidade massiva. Usado em FreeBSD, Illumos, Linux (via OpenZFS) e alguns NAS.
        
8. **O que é uma máquina virtual e qual sua principal função em um sistema operacional?**
    
    Uma máquina virtual (VM) é uma emulação de um sistema de computador, que pode executar programas como se fosse um computador físico. Ela funciona como um sistema operacional convidado (_guest OS_) executando em um sistema operacional hospedeiro (_host OS_) ou diretamente sobre o hardware (_bare-metal hypervisor_). A principal função de uma máquina virtual em um sistema operacional é permitir a execução de múltiplos sistemas operacionais isolados no mesmo hardware físico.
    
9. **Quais são as principais vantagens do uso de máquinas virtuais?**
    
    As principais vantagens do uso de máquinas virtuais incluem:
    
    - **Consolidação de servidores:** Reduz o número de servidores físicos necessários, economizando custos de hardware, energia e espaço.
        
    - **Isolamento:** Cada máquina virtual é isolada das outras, o que significa que um problema em uma VM não afeta as outras.
        
    - **Portabilidade:** VMs podem ser facilmente movidas de um servidor físico para outro, facilitando a migração e o balanceamento de carga.
        
    - **Desenvolvimento e testes:** Ambientes de teste e desenvolvimento podem ser criados rapidamente e isolados do ambiente de produção.
        
    - **Segurança:** Permite a execução segura de aplicações não confiáveis em um ambiente isolado.
        
    - **Recuperação de desastres:** Facilita a criação de snapshots e backups, agilizando a recuperação de sistemas em caso de falhas.
        
    - **Compatibilidade:** Permite executar softwares legados que dependem de versões mais antigas de sistemas operacionais.
        
    - **Eficiência de recursos:** Otimiza o uso do hardware, aproveitando ao máximo a capacidade do servidor físico.
        
10. **O que é um sistema operacional seguro e quais características ele deve possuir?**
    
    Um sistema operacional seguro é aquele que implementa mecanismos e políticas para proteger os recursos do sistema (dados, hardware, software) contra acesso não autorizado, uso indevido, modificação ou destruição. Ele deve ser projetado para garantir a confidencialidade, integridade e disponibilidade dos dados e serviços.
    
    Características que um sistema operacional seguro deve possuir:
    
    - **Autenticação e autorização:** Mecanismos robustos para verificar a identidade dos usuários e processos (autenticação) e determinar quais recursos eles podem acessar (autorização).
        
    - **Controle de acesso:** Implementação de modelos de controle de acesso (MAC, DAC, RBAC) para gerenciar permissões de arquivos, diretórios e outros recursos.
        
    - **Auditoria e log:** Capacidade de registrar eventos de segurança (tentativas de login, acesso a arquivos, etc.) para detecção de atividades suspeitas e análise forense.
        
    - **Gerenciamento de memória:** Proteção de memória para evitar que um processo acesse a memória de outro.
        
    - **Proteção de kernel:** O kernel do sistema operacional deve ser isolado e protegido contra acesso não autorizado.
        
    - **Atualizações de segurança:** Mecanismo eficaz para aplicar patches e atualizações de segurança para corrigir vulnerabilidades.
        
    - **Firewall:** Capacidade de controlar o tráfego de rede, bloqueando conexões não autorizadas.
        
    - **Isolamento de processos:** Cada processo deve ser executado em seu próprio espaço de memória e ter permissões mínimas necessárias.
        
    - **Criptografia:** Suporte para criptografia de dados em repouso e em trânsito.
        
    - **Minimização de superfície de ataque:** Reduzir o número de serviços e funcionalidades expostas, para diminuir os pontos de entrada para ataques.
        
11. **Quais são as principais ameaças à segurança em sistemas operacionais?**
    
    As principais ameaças à segurança em sistemas operacionais incluem:
    
    - **Malware:** Software malicioso como vírus, worms, cavalos de Troia, ransomware, spyware e adware, que podem roubar dados, danificar sistemas ou comprometer a privacidade.
        
    - **Vulnerabilidades de software:** Falhas ou bugs em sistemas operacionais ou aplicativos que podem ser exploradas por atacantes para obter acesso não autorizado ou causar danos.
        
    - **Ataques de negação de serviço (DoS/DDoS):** Tentativas de sobrecarregar um sistema ou rede para torná-lo indisponível para usuários legítimos.
        
    - **Engenharia social:** Manipulação psicológica de pessoas para obter informações confidenciais ou induzi-las a realizar ações que comprometam a segurança.
        
    - **Ataques de força bruta:** Tentativas sistemáticas de adivinhar senhas ou chaves de criptografia.
        
    - **Phishing:** Tentativas de enganar usuários para que revelem informações confidenciais (senhas, dados bancários) através de e-mails ou sites falsos.
        
    - **Acesso não autorizado:** Intrusos obtendo acesso a sistemas ou dados sem permissão.
        
    - **Privilégios escalados:** Usuários ou programas obtendo mais permissões do que deveriam ter.
        
    - **Erro humano:** Configurações incorretas, senhas fracas ou falta de conscientização sobre segurança podem abrir brechas.
        
    - **Ameaças internas:** Usuários internos (funcionários, ex-funcionários) com acesso privilegiado que intencionalmente ou acidentalmente comprometem a segurança.
        
12. **Como funciona o controle de acesso em sistemas operacionais?**
    
    O controle de acesso em sistemas operacionais é o processo de determinar se um usuário ou processo tem permissão para acessar um determinado recurso (arquivo, diretório, dispositivo, serviço de rede, etc.) e que tipo de operação pode ser realizada sobre ele. Ele geralmente funciona através de três etapas principais:
    
    - **Autenticação:** O sistema primeiro verifica a identidade do usuário ou processo que tenta acessar o recurso. Isso geralmente é feito através de senhas, certificados digitais, biometria ou tokens de segurança.
        
    - **Autorização:** Uma vez que a identidade é verificada, o sistema consulta uma política de segurança para determinar quais ações o usuário ou processo autenticado está autorizado a realizar no recurso solicitado. Isso é frequentemente baseado em modelos como:
        
        - **Controle de Acesso Discricionário (DAC):** O proprietário de um recurso pode definir quem tem acesso e quais permissões (leitura, escrita, execução). É o modelo mais comum em sistemas de arquivos pessoais.
            
        - **Controle de Acesso Mandatório (MAC):** Uma autoridade central (o sistema operacional) define as permissões com base em rótulos de segurança e níveis de sensibilidade. Usado em ambientes de alta segurança.
            
        - **Controle de Acesso Baseado em Papel (RBAC):** As permissões são atribuídas a funções (papéis), e os usuários são atribuídos a esses papéis. Simplifica o gerenciamento de permissões em grandes organizações.
            
    - **Auditoria:** O sistema registra tentativas de acesso a recursos, bem-sucedidas ou falhas, em logs de segurança. Isso permite que os administradores monitorem a atividade, detectem atividades suspeitas e investiguem incidentes de segurança.
        
    
    Em resumo, o controle de acesso garante que apenas entidades autorizadas possam interagir com os recursos do sistema da maneira permitida, protegendo a integridade, confidencialidade e disponibilidade dos dados.