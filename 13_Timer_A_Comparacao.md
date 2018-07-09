Para todas as quest�es abaixo, utilize o modo de compara��o do Timer A.


1. Para os itens abaixo, confira a diferen�a no brilho do LED.
	
	(a) Pisque o LED no pino P1.6 numa frequ�ncia de 100 Hz e ciclo de trabalho de 25%.
	

        #include <msp430g2553.h>
        #define LED BIT6;
        #define PERIODO 10000 //Valor de TACCR0
        #define DUTY_CYCLE 2500 //Ciclo de trabalho
        
        int main (void)
        {
            WDTCTL = WDTPW + WDTHOLD; // Stop WDT
            BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
            DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
            P1DIR |= LED; //P1DIR: registrador de dire��o; |=: ou bit a bit (setar); quando=1, corresponde a uma sa�da
        
            //Para se utilizar LED como sa�da do modo de compara��o, realizar as seguintes defini��es, segundo o datasheet
            P1SEL |= LED;
            P1SEL2 &=~LED;
        
            //defini��es para o timerA
            TACCR0 = PERIODO-1;  //TA0CCR0 valor de TAR no instante da interrup��o
            //O TA possui 3 canais, o canal 0 possui um endere�o de interrup��o de maior prioridade
        
        
            //defini��es para o modo de compara��o
            TACCR1 = DUTY_CYCLE-1; //TACCR1 (Canal 1 do TA) valor de TAR no instante da interrup��o = ciclo de trabalho
            TACCTL1 = OUTMOD_7; //registrador que controla modos de cap e comp;
            //outmod_7: modo:set/reset - OUTn � zerado quando TAR=TACCRn, e setado quando TAR=TACCR0.
        
            TACTL = TASSEL_2 + ID_0 + MC_1;
            _BIS_SR(LPM0_bits);//modo de baixo consumo 0
            return 0;
        }


	(b) Pisque o LED no pino P1.6 numa frequ�ncia de 100 Hz e ciclo de trabalho de 50%.
	

        #include <msp430g2553.h>
        #define LED BIT6;
        #define PERIODO 10000 //Valor de TACCR0
        #define DUTY_CYCLE 5000 //Ciclo de trabalho

        int main (void)
        {
            WDTCTL = WDTPW + WDTHOLD; // Stop WDT
            BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
            DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
            P1DIR |= LED; //P1DIR: registrador de dire��o; |=: ou bit a bit (setar); quando=1, corresponde a uma sa�da

            //Para se utilizar LED como sa�da do modo de compara��o, realizar as seguintes defini��es, segundo o datasheet
            P1SEL |= LED;
            P1SEL2 &=~LED;

            //defini��es para o timerA
            TACCR0 = PERIODO-1;  //TA0CCR0 valor de TAR no instante da interrup��o
            //O TA possui 3 canais, o canal 0 possui um endere�o de interrup��o de maior prioridade


            //defini��es para o modo de compara��o
            TACCR1 = DUTY_CYCLE-1; //TACCR1 (Canal 1 do TA) valor de TAR no instante da interrup��o = ciclo de trabalho
            TACCTL1 = OUTMOD_7; //registrador que controla modos de cap e comp;
            //outmod_7: modo:set/reset - OUTn � zerado quando TAR=TACCRn, e setado quando TAR=TACCR0.

            TACTL = TASSEL_2 + ID_0 + MC_1;
            _BIS_SR(LPM0_bits);//modo de baixo consumo 0
            return 0;
        }


	(c) Pisque o LED no pino P1.6 numa frequ�ncia de 100 Hz e ciclo de trabalho de 75%.


        #include <msp430g2553.h>
        #define LED BIT6;
        #define PERIODO 10000 //Valor de TACCR0
        #define DUTY_CYCLE 7500 //Ciclo de trabalho

        int main (void)
        {
            WDTCTL = WDTPW + WDTHOLD; // Stop WDT
            BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
            DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
            P1DIR |= LED; //P1DIR: registrador de dire��o; |=: ou bit a bit (setar); quando=1, corresponde a uma sa�da

            //Para se utilizar LED como sa�da do modo de compara��o, realizar as seguintes defini��es, segundo o datasheet
            P1SEL |= LED;
            P1SEL2 &=~LED;

            //defini��es para o timerA
            TACCR0 = PERIODO-1;  //TA0CCR0 valor de TAR no instante da interrup��o
            //O TA possui 3 canais, o canal 0 possui um endere�o de interrup��o de maior prioridade


            //defini��es para o modo de compara��o
            TACCR1 = DUTY_CYCLE-1; //TACCR1 (Canal 1 do TA) valor de TAR no instante da interrup��o = ciclo de trabalho
            TACCTL1 = OUTMOD_7; //registrador que controla modos de cap e comp;
            //outmod_7: modo:set/reset - OUTn � zerado quando TAR=TACCRn, e setado quando TAR=TACCR0.

            TACTL = TASSEL_2 + ID_0 + MC_1;
            _BIS_SR(LPM0_bits);//modo de baixo consumo 0
            return 0;
        }
15625

2. Pisque o LED no pino P1.6 numa frequ�ncia de 1 Hz e ciclo de trabalho de 25%.


    #include <msp430g2553.h>
    #define LED BIT6;
    #define PERIODO 62500 //Valor de TACCR0
    #define DUTY_CYCLE 15625 //Ciclo de trabalho

    int main (void)
    {
        WDTCTL = WDTPW + WDTHOLD; // Stop WDT
        BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
        DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
        P1DIR |= LED; //P1DIR: registrador de dire��o; |=: ou bit a bit (setar); quando=1, corresponde a uma sa�da

        //Para se utilizar LED como sa�da do modo de compara��o, realizar as seguintes defini��es, segundo o datasheet
        P1SEL |= LED;
        P1SEL2 &=~LED;

        //defini��es para o timerA
        TACCR0 = PERIODO-1;  //TA0CCR0 valor de TAR no instante da interrup��o
        //O TA possui 3 canais, o canal 0 possui um endere�o de interrup��o de maior prioridade


        //defini��es para o modo de compara��o
        TACCR1 = DUTY_CYCLE-1; //TACCR1 (Canal 1 do TA) valor de TAR no instante da interrup��o = ciclo de trabalho
        TACCTL1 = OUTMOD_7; //registrador que controla modos de cap e comp;
        //outmod_7: modo:set/reset - OUTn � zerado quando TAR=TACCRn, e setado quando TAR=TACCR0.

        TACTL = TASSEL_2 + ID_3 + MC_1;
        _BIS_SR(LPM0_bits);//modo de baixo consumo 0
        return 0;
    }



3. Pisque o LED no pino P1.6 numa frequ�ncia de 1 Hz e ciclo de trabalho de 50%.



    #include <msp430g2553.h>
    #define LED BIT6;
    #define PERIODO 62500 //Valor de TACCR0
    #define DUTY_CYCLE 31250 //Ciclo de trabalho

    int main (void)
    {
        WDTCTL = WDTPW + WDTHOLD; // Stop WDT
        BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
        DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
        P1DIR |= LED; //P1DIR: registrador de dire��o; |=: ou bit a bit (setar); quando=1, corresponde a uma sa�da

        //Para se utilizar LED como sa�da do modo de compara��o, realizar as seguintes defini��es, segundo o datasheet
        P1SEL |= LED;
        P1SEL2 &=~LED;

        //defini��es para o timerA
        TACCR0 = PERIODO-1;  //TA0CCR0 valor de TAR no instante da interrup��o
        //O TA possui 3 canais, o canal 0 possui um endere�o de interrup��o de maior prioridade


        //defini��es para o modo de compara��o
        TACCR1 = DUTY_CYCLE-1; //TACCR1 (Canal 1 do TA) valor de TAR no instante da interrup��o = ciclo de trabalho
        TACCTL1 = OUTMOD_7; //registrador que controla modos de cap e comp;
        //outmod_7: modo:set/reset - OUTn � zerado quando TAR=TACCRn, e setado quando TAR=TACCR0.

        TACTL = TASSEL_2 + ID_3 + MC_1;
        _BIS_SR(LPM0_bits);//modo de baixo consumo 0
        return 0;
    }


4. Pisque o LED no pino P1.6 numa frequ�ncia de 1 Hz e ciclo de trabalho de 75%.




















    #include <msp430g2553.h>
    #define LED BIT6;
    #define PERIODO 62500 //Valor de TACCR0
    #define DUTY_CYCLE 46875 //Ciclo de trabalho

    int main (void)
    {
        WDTCTL = WDTPW + WDTHOLD; // Stop WDT
        BCSCTL1 = CALBC1_1MHZ; //MCLK e SMCLK @ 1MHz
        DCOCTL = CALDCO_1MHZ; //MCLK e SMCLK @ 1MHz
        P1DIR |= LED; //P1DIR: registrador de dire��o; |=: ou bit a bit (setar); quando=1, corresponde a uma sa�da

        //Para se utilizar LED como sa�da do modo de compara��o, realizar as seguintes defini��es, segundo o datasheet
        P1SEL |= LED;
        P1SEL2 &=~LED;

        //defini��es para o timerA
        TACCR0 = PERIODO-1;  //TA0CCR0 valor de TAR no instante da interrup��o
        //O TA possui 3 canais, o canal 0 possui um endere�o de interrup��o de maior prioridade


        //defini��es para o modo de compara��o
        TACCR1 = DUTY_CYCLE-1; //TACCR1 (Canal 1 do TA) valor de TAR no instante da interrup��o = ciclo de trabalho
        TACCTL1 = OUTMOD_7; //registrador que controla modos de cap e comp;
        //outmod_7: modo:set/reset - OUTn � zerado quando TAR=TACCRn, e setado quando TAR=TACCR0.

        TACTL = TASSEL_2 + ID_3 + MC_1;
        _BIS_SR(LPM0_bits);//modo de baixo consumo 0
        return 0;
    }
