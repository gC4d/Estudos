
## O que é tabela de pagina e como ela auxilia na conversão de endereço lógico em físico?

É uma estrutura de dados utilizado pelo sistema operacional para fazer a conversão do endereço virtual para o endereço físico. Onde possui uma entrada, que pode ser a página ou o frame, e uma saída, que é efetivamente o endereço físico que será usado pelo processo durante seu processamento pela CPU.

## Best fit, worst fit, first fit e suas aplicações no desempenho

- O Best fit percorre a lista de memória e aloca o processo no espaço liberado no menor espaço possível.
- O Worst fit faz o inverso do best fit, percorre a lista de memória e aloca o processo no maior espaço possível para aquele processo.
- O first fit apenas percorre a lista e aloca o processo no primeiro espaço compatível com o tamanho do processo.

## O que é **Thrashing** e como evitar?

**Thrashing** ocorre quando o s.o passa mais tempo trocando páginas entre a memória principal e secundária (swap) do que executando processo de fato.
Isso pode ocorre devido a um grande número de processos rodando ao mesmo tempo, quando cada processo não tem o número de páginas suficientes em RAM para funcionar bem.

**Como resolver?**

- Adotando algoritmos de substituição otimizados, como clock, clock aprimorado ou LRU.
- Aumento o tamanho da memória principal
- Diminuindo o número de processos simultâneos
	- Reduzindo multiprogramação
