Para todas as quest�es, utilize os LEDs e/ou os bot�es da placa Launchpad do MSP430.

1. Escreva um c�digo em C que pisca os LEDs ininterruptamente.
	//c�digo para piscar os dois LEDs ininterruptamente.	
	#include <msp430g2553.h>  //Declarando a Biblioteca do msp430g2553
	//defini��es para clarear o c�digo
	#define LED1 BIT0
	#define LED2 BIT6
	#define LEDS (LED1|LED2)

	void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um 	n�mero int � sem sinal
	{
	  while ((i--)>0); //realiza um countdown enquanto i>0
	}

	int main(void)
	{
 	 WDTCTL = WDTPW | WDTHOLD; //WhatchDog Timer Reinicia o sistema periodicamente
	  //WDT: WhatchDog Timer; CTL: Control; WDTHOLD: bit for stopping the WDT
	  P1OUT |= LEDS; //|=: ou bit a bit - configurando os bits 0 e 6 como sa�da
	  P1DIR |= LEDS; //levar os pinos 0 e 6 para Vcc - ligando os dois leds, setando-os (or)
	  while(1) //loop infinito
	  {
	      atraso (0xffff); //valor passado � fun��o atraso determina a frequ�ncia
	      P1OUT ^= LEDS; //xor bit-a-bit: inverte
	  }
	  return 0;
	}


2. Escreva um c�digo em C que pisca os LEDs ininterruptamente. No ciclo que pisca os LEDs, o tempo que os LEDs ficam ligados deve ser duas vezes maior do que o tempo que eles ficam desligados.

	//c�digo para piscar os dois LEDs ininterruptamente. O tempo que os LEDs ficam ligados deve ser duas vezes maior do que o tempo que eles ficam desligados.	
	#include <msp430g2553.h>  //Declarando a Biblioteca do msp430g2553
	//defini��es para clarear o c�digo
	#define LED1 BIT0
	#define LED2 BIT6
	#define LEDS (LED1|LED2)

	void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um 	n�mero int � sem sinal
	{
	  while ((i--)>0); //realiza um countdown enquanto i>0
	}

	int main(void)
	{
 	 WDTCTL = WDTPW | WDTHOLD; //WhatchDog Timer Reinicia o sistema periodicamente
	  //WDT: WhatchDog Timer; CTL: Control; WDTHOLD: bit for stopping the WDT
	  P1OUT |= LEDS; //|=: ou bit a bit - configurando os bits 0 e 6 como sa�da
	  P1DIR |= LEDS; //levar os pinos 0 e 6 para Vcc - ligando os dois leds, setando-os (or)
	  while(1) //loop infinito
	  {
	      P1OUT |= LEDS; //liga os leds
              atraso (0xffffffff); //valor passado � fun��o atraso determina a frequ�ncia
              atraso (0xffffffff); 
              P1OUT &= ~LEDS; //desliga os leds
              atraso (0xffffffff); //valor passado � fun��o atraso determina a frequ�ncia             
	  }
	  return 0;
	}


3. Escreva um c�digo em C que acende os LEDs quando o bot�o � pressionado.

4. Escreva um c�digo em C que pisca os LEDs ininterruptamente somente se o bot�o for pressionado.

5. Escreva um c�digo em C que acende os LEDs quando o bot�o � pressionado. Deixe o MSP430 em modo de baixo consumo, e habilite a interrup��o do bot�o.