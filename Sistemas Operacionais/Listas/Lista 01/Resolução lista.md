
## 1.
	- Máquina estendida: Conceder abstrações para fácilitar integração de sistemas aplicativo com o hardware 
	- Gerenciador de recursos: Gerenciar os recursos da máquina (CPU, memorias, **discos**, redes, etc.)

## 2.
	- Modo núcleo fornece ao sistema acesso privilegiado ao hardware.
	- Modo Usuário bloqueia, ou restringew acesso a funções criticas do sistema, impedindo assim que o sistema comprometa a estabilidade do sistema operacional

	- A vantagem em usar dois modos se dá principalmente por 3 pontos:
		- **Segurança**: Impede que qualquer software instalado não tenha acesso as camadas inferiores da máquina, assim evitando quebras de sistema.
		- **Estabilidade**: Reduz o risco de falhas, já que, geralmente, somente o S.O poderá executar operações criticas
		- **Eficiência**: Permite melhor controle para a alocação de recursos, evitando sobrecarregar o hardware.

## 3.
	- Isso se dá pelo fato que as instruções relacionadas ao acesso de dispositivos de entrada e saida são operações realizadas diretamente no hardware. Permitir o acesso a estas a qualquer software poderia acarretar em problemas de corrompimento de dados, invasões de seguranção ou conflitos na comunicação com o dispositivo.

## 4.
	- As intruções que devem ser esclusivas do modo 