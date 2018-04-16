1. Dada uma vari�vel a do tipo char (um byte), escreva os trechos de c�digo em C para: 
(a) Somente setar o bit menos significativo de a. 
a | "00000001"
(b) Somente setar dois bits de a: o menos significativo e o segundo menos significativo. 
a | "00000011"
(c) Somente zerar o terceiro bit menos significativo de a. 
a & "11110111"
(d) Somente zerar o terceiro e o quarto bits menos significativo de a. 
a & "11100111"
(e) Somente inverter o bit mais significativo de a. 
a ^ "10000000"
(f) Inverter o nibble mais significativo de a, e setar o nibble menos significativo de a.
a ^ "11110000"
a | "00001111"

2.Considerando a placa Launchpad do MSP430, escreva o c�digo em C para piscar os dois LEDs ininterruptamente.
//c�digo para piscar os dois LEDs ininterruptamente.
#include <msp430g2553.h>  //Declarando a Biblioteca do msp430g2553
//defini��es para clarear o c�digo
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED1|LED2)

void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
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

3. Considerando a placa Launchpad do MSP430, escreva o c�digo em C para piscar duas vezes os dois LEDs sempre que o usu�rio pressionar o bot�o.
#include <msp430g2553.h>
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED1|LED2)
#define BTN  BIT3

void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
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
                P1OUT |= LEDS; //envia os seguintes dados (010000001) para a sa�da, ou seja, faz com que 0 e 6 tenha n�vel l�gico alto
                atraso(0xffff);
                P1OUT ^= LEDS; 
                atraso(0xffff);
                P1OUT ^= LEDS;
                atraso(0xffff);
                P1OUT ^= LEDS;
            }
        return 0;
}

4. Considerando a placa Launchpad do MSP430, fa�a uma fun��o em C que pisca os dois LEDs uma vez.

void piscar (void)
{
                P1OUT |= LEDS; //envia os seguintes dados (010000001) para a sa�da, ou seja, faz com que 0 e 6 tenha n�vel l�gico alto
                atraso(0xffff);
                P1OUT ^= LEDS; 
                atraso(0xffff);
                P1OUT ^= LEDS;
                atraso(0xffff);
                P1OUT ^= LEDS;
		atraso(0xffff);
}

5. Reescreva o c�digo da quest�o 2 usando a fun��o da quest�o 4.

//c�digo para piscar os dois LEDs ininterruptamente usando fun��o da quest�o 4
#include <msp430g2553.h>  //Declarando a Biblioteca do msp430g2553
//defini��es para clarear o c�digo
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED1|LED2)

void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
{
  while ((i--)>0); //realiza um countdown enquanto i>0
}

void piscar (void)
{
                P1OUT |= LEDS; //envia os seguintes dados (010000001) para a sa�da, ou seja, faz com que 0 e 6 tenha n�vel l�gico alto
                atraso(0xffff);
                P1OUT ^= LEDS; 
                atraso(0xffff);
                P1OUT ^= LEDS;
                atraso(0xffff);
                P1OUT ^= LEDS;
                atraso(0xffff);
}

int main(void)
{
  WDTCTL = WDTPW | WDTHOLD; //WhatchDog Timer Reinicia o sistema periodicamente
  //WDT: WhatchDog Timer; CTL: Control; WDTHOLD: bit for stopping the WDT
  P1OUT |= LEDS; //|=: ou bit a bit - configurando os bits 0 e 6 como sa�da
  P1DIR |= LEDS; //levar os pinos 0 e 6 para Vcc - ligando os dois leds, setando-os (or)
  while(1) //loop infinito
  {
      piscar();
  }
  return 0;
}

6. Reescreva o c�digo da quest�o 3 usando a fun��o da quest�o 4.

#include <msp430g2553.h>
#define LED1 BIT0
#define LED2 BIT6
#define LEDS (LED1|LED2)
#define BTN  BIT3

void atraso (volatile unsigned int i) //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
{
  while ((i--)>0); //realiza um countdown enquanto i>0
}

void piscar (void)
{
                P1OUT |= LEDS; //envia os seguintes dados (010000001) para a sa�da, ou seja, faz com que 0 e 6 tenha n�vel l�gico alto
                atraso(0xffff);
                P1OUT ^= LEDS; 
                atraso(0xffff);
                P1OUT ^= LEDS;
                atraso(0xffff);
                P1OUT ^= LEDS;
		atraso(0xffff);
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
                piscar();
            }
        return 0;
}