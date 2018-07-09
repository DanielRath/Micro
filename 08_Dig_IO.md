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

    #include <msp430g2553.h>
    #define LED1 BIT0
    #define LED2 BIT6
    #define LEDS (LED1|LED2)
    #define BTN  BIT3

    void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero  int � sem sinal
    {
      while ((i--)>0); //realiza um countdown enquanto i>0
    }

    int main(void)
    {

        WDTCTL = WDTPW | WDTHOLD; //Desliga o WDT
    P1DIR |= LEDS; // define as portas correspondentes a LEDS (010000001) como sa�da (P0 e P6 em n�vel l�gico alto (1)), setando-os (or).
        P1DIR &= ~BTN;
        P1REN |= BTN; //habilita o resistor para o bot�o (btn)
        P1OUT |= BTN; //envia o seguinte dado (0000000100) para a sa�da, ou seja, 3 tenha n�vel l�gico alto - seja um resistor de pull up

        while(1)
            if ((P1IN&BTN)==0)
            {

                P1OUT |= LEDS;
            }
            else
                P1OUT &=~ LEDS;
        return 0;
    }


4. Escreva um c�digo em C que pisca os LEDs ininterruptamente somente se o bot�o for pressionado.

    #include <msp430g2553.h>
    #define LED1 BIT0
    #define LED2 BIT6
    #define LEDS (LED1|LED2)
    #define BTN  BIT3

    void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero  int � sem sinal
    {
      while ((i--)>0); //realiza um countdown enquanto i>0
    }

    int main(void)
    {

        WDTCTL = WDTPW | WDTHOLD; //Desliga o WDT
    P1DIR |= LEDS; // define as portas correspondentes a LEDS (010000001) como sa�da (P0 e P6 em n�vel l�gico alto (1)), setando-os (or).
        P1DIR &= ~BTN;
        P1REN |= BTN; //habilita o resistor para o bot�o (btn)
        P1OUT |= BTN; //envia o seguinte dado (0000000100) para a sa�da, ou seja, 3 tenha n�vel l�gico alto - seja um resistor de pull up

        while(1)
            if ((P1IN&BTN)==0)
            {
                while(1)
                {
                P1OUT ^= LEDS;
                atraso(0xffff);
                }
            }
        return 0;
    }


5. Escreva um c�digo em C que acende os LEDs quando o bot�o � pressionado. Deixe o MSP430 em modo de baixo consumo, e habilite a interrup��o do bot�o.

    #include <msp430g2553.h>
    #include <legacymsp430.h>
    #define LED1 BIT0
    #define LED2 BIT6
    #define LEDS (LED1|LED2)
    #define BTN  BIT3


    int main(void)
    {

        WDTCTL = WDTPW | WDTHOLD; //Desliga o WDT
        P1OUT &=~ LEDS; //os bits da sa�da correspondente aos LEDS recebem n�vel l�gico baixo
        P1DIR |= LEDS; // define as portas correspondentes a LEDS (010000001) como sa�da (P0 e P6 em n�vel l�gico alto (1)), setando-os (or).
        P1DIR &= ~BTN;
        P1REN |= BTN; //habilita o resistor para o bot�o (btn) como pull-up: mant�m em n�vel alto se n�o precionado
        P1OUT |= BTN; //envia o seguinte dado (0000000100) para a sa�da, ou seja, 3 tenha n�vel l�gico alto - seja um resistor de pull up
        P1IES |= BTN; //Interrupt Edge Select Registers - registrador de sele��o de borda de interrup��o. P1IES=1 interrup��o na transi��o do n�vel l�gico alto para o baixo
        P1IE |= BTN; //habilita a interrup��o por meio do bot�o
        _BIS_SR(LPM4_bits+GIE);

    }

    interrupt(PORT1_VECTOR) Interrupcao_P1(void)
    {
        if((P1IN&BTN)==0)//se o bot�o estiver pressionado, ficar nesse loop
        {
            P1OUT |= LEDS; //ao se soltar o bot�o, apaga o LED
        }
        else
        {
            P1OUT &=~ LEDS; //ao se soltar o bot�o, apaga o LED
            P1IFG &= ~BTN; //e zera-se a flag de interrup��o
        }

    }
