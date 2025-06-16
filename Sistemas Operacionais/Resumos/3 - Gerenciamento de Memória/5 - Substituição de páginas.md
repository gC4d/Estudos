Substituição de páginas acontece quando um processo precisa carregar uma página da memória secundária, mas não há quadros livres na RAM. Sendo assim, o sistema precisa remover uma página existente da memória para abrir espaço para a nova

#### Qual o objetivo dos algoritmos de substituição?
- Escolher qual páginas remover para minimizar o número de page faults futuros.
- Balancear o desempenho com simplicidade e custo computacional

## Principais algoritmos de substituição

1. Ótimo (OPT)
	1. Remove a página que será usada somente no futuro distante do processo.
	2. Impossível de implementar na prática, já que é impossível prever o futuro.
	3. Serve como referência teórica para validar a eficiência dos demais algoritmos.
2. FIFO (First-In, First-Out)
	1. Remove a página mais antiga em memória
	2. Simples, porém pode remover uma página que ainda esteja sendo usada.
	3. Sofre com o problema da anomalia de Belady 
		1. (mais quadros -> mais page faults)
3. LRU (Least Recently Used)
	1. Remove a página usada a mais tempo
	2. Baseado em localidade temporal
	3. Boa performance, mas difícil de aplicar corretamente
	4. Em sistemas reais, versões aproximadas são usadas
		1. LRU por bits ou Clock
4. Clock (ou segunda chance)
	1. Versão eficiente do LRU, citada anteriormente
	2. Cada página recebe um bit de uso
		1. se = 0 -> substitui.
		2. se = 1 -> zera o bit e dá uma segunda chance.
			1. Avança para a próxima página.
			2. Repete o processo até encontrar um bit 0
	3. As páginas são organizadas como um relógio circular e a leitura dos bits é feita em sentido horário.
5. NFU (Not Frequently Used)
	1. Mantêm contadores para quantas vezes cada página foi usada.