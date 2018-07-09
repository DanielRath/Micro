1. Defina a fun��o `void Atraso(volatile unsigned int x);` que fornece um atraso de `x` milissegundos. Utilize o Timer_A para a contagem de tempo, e assuma que o SMCLK j� foi configurado para funcionar a 1 MHz. Esta fun��o poder� ser utilizada diretamente nas outras quest�es desta prova.

        void atraso (volatile unsigned int x) 
	//volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
   		 {
        		TA0CCR0 = (62.5*x)-1; //quando TAR=TA0CCR0=62.5*x,de TAR no instante em que o timer ser� zerado (TAIFG=1)
        		TA0CTL = TASSEL_2 + ID_3 + MC_1;
	//TASSEL_2: seleciona SMCLK como fonte do clock principal;
	//ID_0: divide valor de SMCLK por 1; MC_1: Up_mode (modo de contagem).
        		while(1)
           		{
               			while((TA0CTL & TAIFG)==0); //enquanto n�o estiver interrompido
                    		TA0CTL &= ~TAIFG; //TAIFG=0
                   		P1OUT ^= LED;
           		 }
   		}



2. Pisque os LEDs da Launchpad numa frequ�ncia de 100 Hz.


		#include <msp430g2553.h>
      		#define LED1 BIT0
        	#define LED2 BIT6
        	#define LED (LED1|LED2)
		int main(void)
			{
				WDTCTL = WDTPW + WDTHOLD; // Stop WDT
				BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
				DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
				P1OUT &= ~LED; //LED come�a apagado
				P1DIR |= LED; //P1DIR LED � sa�da
				TA0CCR0 = 1250-1;
				TA0CTL = TASSEL_2 + ID_3 + MC_1;
			//quando o contador zera TAIFG=1
				while(1)
					{
						while((TA0CTL & TAIFG)==0); //enquanto n�o estiver interrompido
							P1OUT ^= LED;
							TA0CTL &= ~TAIFG;
					}
			return 0;
			}


3. Pisque os LEDs da Launchpad numa frequ�ncia de 20 Hz.
		#include <msp430g2553.h>
      		#define LED1 BIT0
        	#define LED2 BIT6
        	#define LED (LED1|LED2)
		int main(void)
			{
				WDTCTL = WDTPW + WDTHOLD; // Stop WDT
				BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
				DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
				P1OUT &= ~LED; //LED come�a apagado
				P1DIR |= LED; //P1DIR LED � sa�da
				TA0CCR0 = 6250-1;
				TA0CTL = TASSEL_2 + ID_3 + MC_1;
			//quando o contador zera TAIFG=1
				while(1)
					{
						while((TA0CTL & TAIFG)==0); //enquanto n�o estiver interrompido
							P1OUT ^= LED;
							TA0CTL &= ~TAIFG;
					}
			return 0;
			}




4. Pisque os LEDs da Launchpad numa frequ�ncia de 1 Hz.
		#include <msp430g2553.h>
		#define LED1 BIT0
		#define LED2 BIT6
		#define LED (LED1|LED2)
		int main(void)
			{
				WDTCTL = WDTPW + WDTHOLD; // Stop WDT
				BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
				DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
				P1OUT &= ~LED; //LED come�a apagado
				P1DIR |= LED; //P1DIR LED � sa�da
				TA0CCR0 = 62500-1;
				TA0CTL = TASSEL_2 + ID_3 + MC_1;
			//quando o contador zera TAIFG=1
				while(1)
					{
						while((TA0CTL & TAIFG)==0); //enquanto n�o estiver interrompido
							P1OUT ^= LED;
							TA0CTL &= ~TAIFG;
					}
			return 0;
			}




5. Pisque os LEDs da Launchpad numa frequ�ncia de 0,5 Hz.

		#include <msp430g2553.h>
      		#define LED1 BIT0
        	#define LED2 BIT6
        	#define LED (LED1|LED2)
		int main(void)
			{
				WDTCTL = WDTPW + WDTHOLD; // Stop WDT
				BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
				DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
				P1OUT &= ~LED; //LED come�a apagado
				P1DIR |= LED; //P1DIR LED � sa�da
				TA0CCR0 = 62500-1;
				TA0CTL = TASSEL_2 + ID_3 + MC_3;
			//contador no modo up_down: para atingir o n�mero de contagens (2*62500), correspondente ao per�odo desejado
			//quando o contador zera TAIFG=1
				while(1)
					{
						while((TA0CTL & TAIFG)==0); //enquanto n�o estiver interrompido
							P1OUT ^= LED;
							TA0CTL &= ~TAIFG;
					}
			return 0;
			}





6. Repita as quest�es 2 a 5 usando a interrup��o do Timer A para acender ou apagar os LEDs.

	Pisque os LEDs da Launchpad numa frequ�ncia de 100 Hz.



	        #include <msp430g2553.h>
	        #include <intrinsics.h> // Para rodar interrupcoes
	        #define LED1 BIT0
	        #define LED2 BIT6
	        #define LED (LED1|LED2)

	        void atraso (volatile unsigned int x)
	        //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
	            {
	                    TA0CCR0 = (x)-1; //quando TAR=TA0CCR0=62.5*x,de TAR no instante em que o timer ser� zerado (TAIFG=1)
	                    TA0CTL = TASSEL_2 + ID_0 + MC_1 + TAIE; //TAIE:Timer A counter interrupt enable; MC_3: modo up_down
	                    _BIS_SR(LPM0_bits + GIE);//LPM0_bits: CPU off; GIE: General interrupt enable - interrompe instru��es mascar�veis
	            }

	        int main(void)
	        {
	            WDTCTL = WDTPW + WDTHOLD; // Stop WDT
	            BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
	            DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
	            P1OUT &= ~LED; //LED come�a apagado
	            P1DIR |= LED;
	            atraso(10000);
	        }

	        #pragma vector = TIMER0_A1_VECTOR
	        //vetor de interrup��o do Timer0_A1
	        __interrupt void TA0_ISR(void)
	        {
	            TA0CTL &= ~TAIFG; //TAIFG=0; ao N�O se zerar a flag de interrup��o, demora muito mais
	            P1OUT ^= LED;
	        }
		

	Pisque os LEDs da Launchpad numa frequ�ncia de 20 Hz.

	        #include <msp430g2553.h>
	        #include <intrinsics.h> // Para rodar interrupcoes
	        #define LED1 BIT0
	        #define LED2 BIT6
	        #define LED (LED1|LED2)

	        void atraso (volatile unsigned int x)
	        //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
	            {
	                    TA0CCR0 = (x)-1; //quando TAR=TA0CCR0=62.5*x,de TAR no instante em que o timer ser� zerado (TAIFG=1)
	                    TA0CTL = TASSEL_2 + ID_0 + MC_1 + TAIE; //TAIE:Timer A counter interrupt enable; MC_3: modo up_down
	                    _BIS_SR(LPM0_bits + GIE);//LPM0_bits: CPU off; GIE: General interrupt enable - interrompe instru��es mascar�veis
	            }

	        int main(void)
	        {
	            WDTCTL = WDTPW + WDTHOLD; // Stop WDT
	            BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
	            DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
	            P1OUT &= ~LED; //LED come�a apagado
	            P1DIR |= LED;
	            atraso(50000);
	        }

	        #pragma vector = TIMER0_A1_VECTOR
	        //vetor de interrup��o do Timer0_A1
	        __interrupt void TA0_ISR(void)
	        {
	            TA0CTL &= ~TAIFG; //TAIFG=0; ao N�O se zerar a flag de interrup��o, demora muito mais
	            P1OUT ^= LED;
	        }





	Pisque os LEDs da Launchpad numa frequ�ncia de 1 Hz.

		#include <msp430g2553.h>
		#include <intrinsics.h> // Para rodar interrupcoes
		#define LED1 BIT0
		#define LED2 BIT6
		#define LED (LED1|LED2)

 		void atraso (volatile unsigned int x)
		//volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
	        {
	                TA0CCR0 = (62.5*x)-1; //quando TAR=TA0CCR0=62.5*x,de TAR no instante em que o timer ser� zerado (TAIFG=1)
	                TA0CTL = TASSEL_2 + ID_3 + MC_1 + TAIE;
		//Timer A counter interrupt enable
                _BIS_SR(LPM0_bits + GIE);
	        //LPM0_bits: CPU off - defines for C
		//GIE: General interrupt enable - interrompe instru��es mascar�veis
	        }

		int main(void)
		{
		    WDTCTL = WDTPW + WDTHOLD; // Stop WDT
		    BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
		    DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
		    P1OUT &= ~LED; //LED come�a apagado
		    P1DIR |= LED;
		    atraso(1000);
		}

		#pragma vector = TIMER0_A1_VECTOR
		//vetor de interrup��o do Timer0_A1
		__interrupt void TA0_ISR(void)
		{
		    TA0CTL &= ~TAIFG; //TAIFG=0; ao N�O se zerar a flag de interrup��o, demora muito mais
		    P1OUT ^= LED;
		}






	Pisque os LEDs da Launchpad numa frequ�ncia de 0,5 Hz.

	        #include <msp430g2553.h>
	        #include <intrinsics.h> // Para rodar interrupcoes
	        #define LED1 BIT0
	        #define LED2 BIT6
	        #define LED (LED1|LED2)

	        void atraso (volatile unsigned int x)
	        //volatile: indica para o compilador que a vari�vel pode ser modificada de forma n�o expl�cita. Unsigned determina que um n�mero int � sem sinal
	            {
	                    TA0CCR0 = (62.5*x)-1; //quando TAR=TA0CCR0=62.5*x,de TAR no instante em que o timer ser� zerado (TAIFG=1)
	                    TA0CTL = TASSEL_2 + ID_3 + MC_3 + TAIE; //TAIE:Timer A counter interrupt enable; MC_3: modo up_down
	                    _BIS_SR(LPM0_bits + GIE);//LPM0_bits: CPU off; GIE: General interrupt enable - interrompe instru��es mascar�veis
	            }

	        int main(void)
	        {
	            WDTCTL = WDTPW + WDTHOLD; // Stop WDT
	            BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
	            DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
	            P1OUT &= ~LED; //LED come�a apagado
	            P1DIR |= LED;
	            atraso(1000);
	        }

	        #pragma vector = TIMER0_A1_VECTOR
	        //vetor de interrup��o do Timer0_A1
	        __interrupt void TA0_ISR(void)
	        {
	            TA0CTL &= ~TAIFG; //TAIFG=0; ao N�O se zerar a flag de interrup��o, demora muito mais
	            P1OUT ^= LED;
	        }




7. Defina a fun��o `void paralelo_para_serial(void);` que l� o byte de entrada via porta P1 e transmite os bits serialmente via pino P2.0. Comece com um bit em nivel alto, depois os bits na ordem P1.0 - P1.1 - � - P1.7 e termine com um bit em n�vel baixo. Considere um per�odo de 1 ms entre os bits.



8. Fa�a o programa completo que l� um byte de entrada serialmente via pino P2.0 e transmite este byte via porta P1. O sinal serial come�a com um bit em nivel alto, depois os bits na ordem 0-7 e termina com um bit em n�vel baixo. Os pinos P1.0-P1.7 dever�o corresponder aos bits 0-7, respectivamente. Considere um per�odo de 1 ms entre os bits.



9. Defina a fun��o `void ConfigPWM(volatile unsigned int freqs, volatile unsigned char ciclo_de_trabalho);` para configurar e ligar o Timer_A em modo de compara��o. Considere que o pino P1.6 j� foi anteriormente configurado como sa�da do canal 1 de compara��o do Timer_A, que somente os valores {100, 200, 300, �, 1000} Hz s�o v�lidos para a frequ�ncia, que somente os valores {0, 25, 50, 75, 100} % s�o v�lidos para o ciclo de trabalho, e que o sinal de clock SMCLK do MSP430 est� operando a 1 MHz.


















