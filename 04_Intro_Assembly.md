Para todas as quest�es, considere que as vari�veis `f`, `g`, `h`, `i` e `j` s�o do tipo inteiro (16 bits na arquitetura do MSP430), e que o vetor `A[]` � do tipo inteiro. Estas vari�veis est�o armazenadas nos seguintes registradores:


- f: R4

- g: R5

- h: R6

- i: R7

- j: R8

- A: R9


Utilize os registradores R11, R12, R13, R14 e R15 para armazenar valores tempor�rios.


1. Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instru��es: mov.w, add.w e sub.w.


	(a) `f = 0;`
		mov.w #0, R4 #copia o valor (da constante) 0 no registrador R4 


	(b) `g++;`

 (incremento)
		mov.w #1, R11 #copia o valor (da constante) 1 no registrador tempor�rio R11 
		add.w R11, R5

	(c) `h--;`

		mov.w #1,R12
		sub.w R12, R6

	(d) `i += 2;
		mov.w #2, R13
		add.w R13, R7
`
	(e) `j -= 2;`


		mov.w #2, R14
		sub.w R14, R8

2. Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instru��es: mov.w, add.w, sub.w, clr.w, dec.w, decd.w, inc.w e incd.w.


	(a) `f = 0;`


		clr.w R4

	(b) `g++;`


		inc.w R5

	(c) `h--;
		dec.w R6`



	(d) `i += 2;`

		incd.w R7
	

	(e) `j -= 2;`


		decd,w R8

Traduza as seguintes linhas em C para a linguagem assembly do MSP430. Utilize somente as seguintes instru��es: mov.w, add.w, sub.w, clr.w, dec.w, decd.w, inc.w e incd.w.


	(a) `f *= 2;`


		add.w R4,R4

	(b) `g *= 3;`


		mov.w R5, R11
		add.w R11, R5 #multiplicando por 2
		add.w R11, R5 #multiplicando por 3

	(c) `h *= 4;`
		mov.w R6, R12
		add.w R12, R6 #multiplicando por 2
		add.w R12, R6 #multiplicando por 3
		add.w R12, R6 #multiplicando por 4	

	
(d) `A[2] = A[1] + A[0];`


		add.w 2(R9), 4(R9) #2(R9)=A[1]
		add.w R9, 4(R9)

	(e) `A[3] = 2*f - 4*h;`


		add.w R4,R4 #2*f
		mov.w R6, R12
		add.w R12, R6 #multiplicando h por 2
		add.w R12, R6 #multiplicando h por 3
		add.w R12, R6 #multiplicando h por 4
		add.w R4, 6(R9) #A[3]=2*f
		sub.w R6, 6(R9)	#A[3]-=2*f

	(f) `A[3] = 2*(f - 2*h);`
		add.w R6, R6 #2*h
		add.w R4, 6(R9) #A[3]=f
		sub.w R6, 6(R9) #A[3] = (f - 2*h);
		add.w 6(R9), 6(R9) #A[3] = 2*(f - 2*h);