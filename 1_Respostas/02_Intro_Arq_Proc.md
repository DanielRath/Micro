1. Quais as diferenças entre os barramentos de dados e de endereços?
	O barramento de dados é utilizado na transmissão de informações entre os dispositivos, já o de endereços é utilizado na seleção da origem ou destino dos sinais transmitidos.

2. Quais são as diferenças entre as memórias RAM e ROM?
	O conceito da RAM consiste em uma memória de acesso aleatório, que é volátio - quando há perda da alimentação, perde-se também os dados. A ROM (Read-only memory), por outro lado, não é volátil, entretanto apresenta uma escrita bem mais lenta.

3.Considere o código abaixo:

#include <stdio.h>
int main(void)
{
	int i;
	printf("Insira um número inteiro: ");
	scanf("%d", &i);
	if(i%2)
		printf("%d eh impar.\n");
	else
		printf("%d eh par.\n");
	return 0;
}
Para este código, responda: (a) A variável i é armazenada na memória RAM ou ROM? Por quê? (b) O programa compilado a partir deste código é armazenado na memória RAM ou ROM? Por quê?
Resposta:(a) é armazenada na memória RAM, por devido à necessidade de alta velocidade para a escrita, e por ser volátil.
	 (b) o programa compilado é armazenado na memória ROM, visto que, ao desligar a alimentação e conectá-la novamente, há a necessidade do programa ser encontrado novamente.


4. Quais são as diferenças, vantagens e desvantagens das arquiteturas Harvard e Von Neumann?
	A arquitetura Harvard é mais complexa, é geralmente RISC (ênfase no software) e apresenta como vantagem apresentar uma maior velocidade, pois permite o simultâneo acesso às memórias.
A arquitetura Von Neuman é mais simples e é geralmente CISC (ênfase no hardware). Por não apresentar um acesso simultâneo às memórias, é mais lenta, sendo essa sua principal desvantagem.

5. Considere a variável inteira i, armazenando o valor 0x8051ABCD. Se i é armazenada na memória a partir do endereço 0x0200, como ficam este byte e os seguintes, considerando que a memória é: (a) Little-endian; (b) Big-endian.
Resposta:(a)CD AB 51 80
	 (b)80 51 AB CD

6. Sabendo que o processador do MSP430 tem registradores de 16 bits, como ele soma duas variáveis de 32 bits?
	Para serem realizadas operações com 32 bits, devem ser utilizados dois registradores: um armazenará os dados dos 16 bits mais significativos e o outr do 16 menos significativos.
