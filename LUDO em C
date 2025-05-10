#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>
#include <unistd.h>
#define ANSI_RED "\033[1;31m"
#define ANSI_GREEN "\033[1;32m"
#define ANSI_YELLOW "\033[1;33m"
#define ANSI_BLUE "\033[1;34m"
#define ANSI_RESET "\033[0m"
 const char *cor;
struct pecas{ //Posição das 4 Peças
	int pos[4];
};
void tabuleiro(){ //Imprime o tabuleiro
    printf("\n\t\tRevise as posições do tabuleiro:\n\n");
    printf("\n");
    printf("\t                  24 25 26               \n");
    printf("\t                  23 %sJ2%s %sJ2%s               \n", ANSI_GREEN, ANSI_RESET, ANSI_GREEN, ANSI_RESET);
    printf("\t                  %sAS%s %sJ2%s 28               \n", ANSI_YELLOW, ANSI_RESET, ANSI_GREEN, ANSI_RESET);
    printf("\t                  21 %sJ2%s 29               \n", ANSI_GREEN, ANSI_RESET);
    printf("\t                  20 %sJ2%s 30               \n", ANSI_GREEN, ANSI_RESET);
    printf("\t                  19 %sJ2%s 31               \n", ANSI_GREEN, ANSI_RESET);
    printf("\t13 %sJ3%s 15 16 17 18    %sPF%s    32 33 34 %sAS%s 36 37 \n", ANSI_YELLOW, ANSI_RESET, ANSI_GREEN, ANSI_RESET, ANSI_GREEN, ANSI_RESET);
    printf("\t12 %sJ3%s %sJ3%s %sJ3%s %sJ3%s %sJ3%s %sPF%s    %sPF%s %sJ4%s %sJ4%s %sJ4%s %sJ4%s %sJ4%s 38  \n", ANSI_YELLOW, ANSI_RESET, ANSI_YELLOW, ANSI_RESET, ANSI_YELLOW, ANSI_RESET, ANSI_YELLOW, ANSI_RESET, ANSI_YELLOW, ANSI_RESET, ANSI_YELLOW, ANSI_RESET, ANSI_BLUE, ANSI_RESET, ANSI_BLUE, ANSI_RESET, ANSI_BLUE, ANSI_RESET, ANSI_BLUE, ANSI_RESET, ANSI_BLUE, ANSI_RESET, ANSI_BLUE, ANSI_RESET);
    printf("\t11 10 %sAS%s 08 07 06    %sPF%s    44 43 42 41 %sJ4%s 39 \n", ANSI_RED, ANSI_RESET, ANSI_RED, ANSI_RESET, ANSI_BLUE, ANSI_RESET);
    printf("\t                  05 %sJ1%s 45               \n", ANSI_RED, ANSI_RESET);
    printf("\t                  04 %sJ1%s 46               \n", ANSI_RED, ANSI_RESET);
    printf("\t                  03 %sJ1%s 47               \n", ANSI_RED, ANSI_RESET);
    printf("\t                  02 %sJ1%s %sAS%s               \n", ANSI_RED, ANSI_RESET, ANSI_BLUE, ANSI_RESET);
    printf("\t                  %sJ1%s %sJ1%s 49               \n", ANSI_RED, ANSI_RESET, ANSI_RED, ANSI_RESET);
    printf("\t                  52 51 50               \n\n");
}

int jogardado(){ //Jogar o dado
	int dado;
	system("pause");
	dado = rand()%6+1;
	return dado;
}
void pospecas(int jog, struct pecas *p) {
     // Adicionar cor ao número da peça com base no jogador atual
        if (jog == 0)
            cor = ANSI_RED;
        else if (jog == 1)
            cor = ANSI_GREEN;
        else if (jog == 2)
            cor = ANSI_YELLOW;
        else if (jog == 3)
            cor = ANSI_BLUE;
        else
            cor = ANSI_RESET;
    printf("%sPosições das peças do jogador %d:%s\n",cor, jog+1, ANSI_RESET);

    for (int i = 0; i < 4; i++) {
        int posicao = p[jog].pos[i];


        printf("%sPeça %d: %s%d%s\n", cor, i + 1, cor, posicao, ANSI_RESET);
    }
    printf("\n");
 return;
}
int informar(int *d, int pp, struct pecas *p, int jog){ //Informar a peça para movimento
	int peca, cont = 0, i;
	for(i = 0; i < 4; i++){
		if(p[jog].pos[i] == 0)
			cont++;
	}
	if(cont > 0 && d[0] == 6){
		printf("\nQual peça deseja tirar da casa inicial ou mover %d casas? ", d[pp]);
		scanf("%d", &peca);
	} else {
		printf("\nQual peça deseja mover %d casas? ", d[pp]);
		scanf("%d", &peca);
	}
	printf("\n");
	return peca;
}
void saida(struct pecas *p, int jogador, int peca, int local[][4]){ //Faz as peças sairem da posição inicial, quando dado = 6
	if(jogador == 0){
		p[jogador].pos[peca - 1] += 1;
		local[jogador][peca - 1] = 1;
	}
	else if(jogador == 1){
		p[jogador].pos[peca - 1] += 27;
		local[jogador][peca - 1] = 1;
	}
	else if(jogador == 2){
		p[jogador].pos[peca - 1] += 14;
		local[jogador][peca - 1] = 1;
	}
	else if(jogador == 3){
		p[jogador].pos[peca - 1] += 40;
		local[jogador][peca - 1] = 1;
	}
}
void capturarPecas(struct pecas *p, int local[][4], int pp, int jc, int jogador) {
                p[jc].pos[pp] = 0;
                local[jc][pp]= 0;
                printf("\n\tJogador %d capturou a peça do Jogador %d!\n", jogador + 1 , jc + 1);
                printf("\n\tPeça do Jogador %d voltará para posição inicial!\n", jc + 1);
                printf("\n\tJogador %d poderá jogar novamente!\n", jogador +1);
                printf("\n");

}
void jogo(struct pecas *p, int jogador, int quant){ //Função para a jogada dos jogadores
	int f=0, dado[3], peca, i, j, pvenc[4]={0,0,0,0}, vencedor = 0, cont = 0, local[quant][4];
	for(i = 0; i < quant; i++)
		for(j = 0; j < 4; j++)
			local[i][j] = 0;
	do{
		tabuleiro();
		for(i = 0; i < quant; i++){
             if(f == 5){ //Condição falsa para entrar só com o pular
               pular:
               printf("Perdeu sua vez...");
               if(i!=quant-1){
                i++;
               }else{
               i=0;
               }

             }
            reinicio:
        if (i == 0)
            cor = ANSI_RED;
        else if (i == 1)
            cor = ANSI_GREEN;
        else if (i == 2)
            cor = ANSI_YELLOW;
        else if (i == 3)
            cor = ANSI_BLUE;
        else
            cor = ANSI_RESET;
            sleep(1);
			printf("\n\t%sVez do Jogador %d%s\n",cor, i+1, ANSI_RESET);
			printf("Gire o Dado: \n");
			dado[0] = jogardado();
			sleep(1);
			printf("Você tirou o número: %s%d%s\n\n", cor, dado[0], ANSI_RESET);
			if(dado[0] == 6){
				printf("Gire o Dado Novamente:\n");
				dado[1] = jogardado();
				sleep(1);
				printf("Você tirou o número: %s%d%s\n\n", cor, dado[1], ANSI_RESET);

				if(dado[1] == 6){
					printf("Gire o Dado Novamente:\n");
					dado[2] = jogardado();
					sleep(1);
					printf("Você tirou o número: %s%d%s\n\n", cor, dado[2], ANSI_RESET);

					if(dado[2] == 6)
						printf("\nPerdeu sua vez...\n");
					else {
						//dado 1
						pospecas(i, p);
						peca = informar(dado, 0, p, i);

						if((peca < 1 || peca > 4) || local[i][peca - 1] + dado[0] > 57){
                                if(local[i][0]+ dado[0] > 57 && local[i][1]+ dado[0] > 57 && local[i][2]+ dado[0] > 57 && local[i][3]+ dado[0] > 57)
                                 goto pular;

							do{
								printf("Peca incorreta! Digite novamente.\n");
								peca = informar(dado, 0, p, i);

							}while((peca < 1 || peca > 4) || local[i][peca - 1] + dado[0] > 57);
						}
						if(p[i].pos[peca - 1] == 0){
							saida(p, i, peca, local);
						} else {
							if((i != 0) && p[i].pos[peca - 1] + dado[0] > 52){
								p[i].pos[peca - 1] += dado[0] - 52;
								local[i][peca - 1] += dado[0];
							} else {
								p[i].pos[peca - 1] += dado[0];
								local[i][peca - 1] += dado[0];
							}
						}
                        for (int pec = 0; pec < 4; pec++) {
                          for (int jog = 0; jog < quant; jog++) {
                           if(p[i].pos[peca - 1] != 0 && p[i].pos[peca - 1] != 1 && p[i].pos[peca - 1] != 9 && p[i].pos[peca - 1] != 14 && p[i].pos[peca - 1] != 22 && p[i].pos[peca - 1] != 27 && p[i].pos[peca - 1] != 35 && p[i].pos[peca - 1] != 40 && p[i].pos[peca - 1] != 48){
                         if(i!=jog && p[i].pos[peca - 1]== p[jog].pos[pec] && local[jog][pec]< 52){ // Verifica se o jogador é diferente do jogador atual
                             capturarPecas(p, local, pec, jog, i);
                              goto reinicio;
                            }
                          }
                          }

                        }

                            if(local[i][peca - 1]==57){
                             pvenc[i]++;
                             while(pvenc[i]<4){
                               printf("Sua peça chegou ao destino final! Jogue novamente!\n")  ;
                                goto reinicio;
                             }
                               if(pvenc[i]==4){
                                printf("\n\tParabéns Jogador %d, VOCÊ VENCEU O JOGO!!!\n", i+1);
                                vencedor=1;
                                break;
                               }
                           }
						pospecas(i, p);

						//dado 2
						peca = informar(dado, 1, p, i);

						if((peca < 1 || peca > 4) || local[i][peca - 1] + dado[1] > 57){
                            if(local[i][0]+ dado[1] > 57 && local[i][1]+ dado[1] > 57 && local[i][2]+ dado[1] > 57 && local[i][3]+ dado[1] > 57)
                                 goto pular;

							do{
								printf("Peça incorreta! Digite novamente.\n");
								peca = informar(dado, 1, p, i);
							}while((peca < 1 || peca > 4) || local[i][peca - 1] + dado[1] > 57);
						}
						if(p[i].pos[peca - 1] == 0){
							saida(p, i, peca, local);
						} else {
							if((i != 0) && p[i].pos[peca - 1] + dado[1] > 52){
								p[i].pos[peca - 1] += dado[1] - 52;
								local[i][peca - 1] += dado[1];
							} else {
								p[i].pos[peca - 1] += dado[1];
								local[i][peca - 1] += dado[1];
							}
						}
						for (int pec = 0; pec < 4; pec++) {
                          for (int jog = 0; jog < quant; jog++) {
                           if(p[i].pos[peca - 1] != 0 && p[i].pos[peca - 1] != 1 && p[i].pos[peca - 1] != 9 && p[i].pos[peca - 1] != 14 && p[i].pos[peca - 1] != 22 && p[i].pos[peca - 1] != 27 && p[i].pos[peca - 1] != 35 && p[i].pos[peca - 1] != 40 && p[i].pos[peca - 1] != 48){
                            if(i!=jog && p[i].pos[peca - 1]== p[jog].pos[pec] && local[jog][pec]< 52){ // Verifica se o jogador é diferente do jogador atual
                             capturarPecas(p, local, pec, jog, i);
                              goto reinicio;
                            }
                          }
                          }


                        }

                            if(local[i][peca - 1]==57){
                             pvenc[i]++;
                             while(pvenc[i]<4){
                               printf("Sua peça chegou ao destino final! Jogue novamente!\n")  ;
                                goto reinicio;
                             }
                               if(pvenc[i]==4){
                                printf("\n\tParabéns Jogador %d, VOCÊ VENCEU O JOGO!!!\n", i+1);
                                vencedor=1;
                                break;
                               }
                            }
						pospecas(i, p);

						//dado 3
						peca = informar(dado, 2, p, i);
						if((peca < 1 || peca > 4) || p[i].pos[peca - 1] == 0 || local[i][peca - 1] + dado[2] > 57){
                            if(local[i][0]+ dado[2] > 57 && local[i][1]+ dado[2] > 57 && local[i][2]+ dado[2] > 57 && local[i][3]+ dado[2] > 57)
                                 goto pular;
							do{
								printf("Peca Invalida ou na Posicao Inicial! Digite Novamente.\n");
								peca = informar(dado, 2, p, i);
							}while((peca < 1 || peca > 4) || p[i].pos[peca - 1] == 0 || local[i][peca - 1] + dado[2] > 57);
						}
						if((i != 0) && p[i].pos[peca - 1] + dado[2] > 52){
							p[i].pos[peca - 1] += dado[2] - 52;
							local[i][peca - 1] += dado[2];
						} else {
							p[i].pos[peca - 1] += dado[2];
							local[i][peca - 1] += dado[2];
						}
	                    for (int pec = 0; pec < 4; pec++) {
                          for (int jog = 0; jog < quant; jog++) {
                           if(p[i].pos[peca - 1] != 0 && p[i].pos[peca - 1] != 1 && p[i].pos[peca - 1] != 9 && p[i].pos[peca - 1] != 14 && p[i].pos[peca - 1] != 22 && p[i].pos[peca - 1] != 27 && p[i].pos[peca - 1] != 35 && p[i].pos[peca - 1] != 40 && p[i].pos[peca - 1] != 48){
                            if(i!=jog && p[i].pos[peca - 1]== p[jog].pos[pec] && local[jog][pec]< 52){ // Verifica se o jogador é diferente do jogador atual
                             capturarPecas(p, local, pec, jog, i);
                              goto reinicio;
                            }
                          }
                          }


                        }
                         if(local[i][peca - 1]==57){
                             pvenc[i]++;
                             while(pvenc[i]<4){
                               printf("Sua peça chegou ao destino final! Jogue novamente!\n")  ;
                                goto reinicio;
                             }
                            if(pvenc[i]==4){
                                printf("\n\tParabéns Jogador %d, VOCÊ VENCEU O JOGO!!!\n", i+1);
                                vencedor=1;
                                break;
                            }
                        }
						pospecas(i, p);
					}
				} else {
					//dado 1
					pospecas(i, p);
					peca = informar(dado, 0, p, i);
					if((peca < 1 || peca > 4) || local[i][peca - 1] + dado[0] > 57){
                        if(local[i][0]+ dado[0] > 57 && local[i][1]+ dado[0] > 57 && local[i][2]+ dado[0] > 57 && local[i][3]+ dado[0] > 57)
                            goto pular;
						do{
							printf("Peca Invalida! Digite Novamente.\n");
							peca = informar(dado, 0, p, i);
						}while((peca < 1 || peca > 4) || local[i][peca - 1] + dado[0] > 57);
					}
					if(p[i].pos[peca - 1] == 0){
							saida(p, i, peca, local);
					} else {
						if((i != 0) && p[i].pos[peca - 1] + dado[0] > 52){
							p[i].pos[peca - 1] += dado[0] - 52;
							local[i][peca - 1] += dado[0];
						} else {
							p[i].pos[peca - 1] += dado[0];
							local[i][peca - 1] += dado[0];
						}
					}
					for (int pec = 0; pec < 4; pec++) {
                          for (int jog = 0; jog < quant; jog++) {
                           if(p[i].pos[peca - 1] != 0 && p[i].pos[peca - 1] != 1 && p[i].pos[peca - 1] != 9 && p[i].pos[peca - 1] != 14 && p[i].pos[peca - 1] != 22 && p[i].pos[peca - 1] != 27 && p[i].pos[peca - 1] != 35 && p[i].pos[peca - 1] != 40 && p[i].pos[peca - 1] != 48){
                            if(i!=jog && p[i].pos[peca - 1]== p[jog].pos[pec] && local[jog][pec]< 52){ // Verifica se o jogador é diferente do jogador atual
                             capturarPecas(p, local, pec, jog, i);
                              goto reinicio;
                            }
                          }
                          }


                    }
                         if(local[i][peca - 1]==57){
                             pvenc[i]++;
                             while(pvenc[i]<4){
                               printf("Sua peça chegou ao destino final! Jogue novamente!\n")  ;
                                goto reinicio;
                             }
                            if(pvenc[i]==4){
                                printf("\n\tParabéns Jogador %d, VOCÊ VENCEU O JOGO!!!\n", i+1);
                                vencedor=1;
                                break;
                            }
                        }
					pospecas(i, p);

					//dado 2
					peca = informar(dado, 1, p, i);
					if((peca < 1 || peca > 4) || p[i].pos[peca - 1] == 0 || local[i][peca - 1] + dado[1] > 57){
                        if(local[i][0]+ dado[1] > 57 && local[i][1]+ dado[1] > 57 && local[i][2]+ dado[1] > 57 && local[i][3]+ dado[1] > 57)
                            goto pular;
						do{
							printf("Peça Inválida ou na Posição Inicial! Digite Novamente.\n");
							peca = informar(dado, 1, p, i);
						}while((peca < 1 || peca > 4) || p[i].pos[peca - 1] == 0 || local[i][peca - 1] + dado[1] > 57);
					}
					if((i != 0) && p[i].pos[peca - 1] + dado[1] > 52){
						p[i].pos[peca - 1] += dado[1] - 52;
						local[i][peca - 1] += dado[1];
					} else {
						p[i].pos[peca - 1] += dado[1];
						local[i][peca - 1] += dado[1];
					}
					for (int pec = 0; pec < 4; pec++) {
                          for (int jog = 0; jog < quant; jog++) {
                           if(p[i].pos[peca - 1] != 0 && p[i].pos[peca - 1] != 1 && p[i].pos[peca - 1] != 9 && p[i].pos[peca - 1] != 14 && p[i].pos[peca - 1] != 22 && p[i].pos[peca - 1] != 27 && p[i].pos[peca - 1] != 35 && p[i].pos[peca - 1] != 40 && p[i].pos[peca - 1] != 48){
                            if(i!=jog && p[i].pos[peca - 1]== p[jog].pos[pec] && local[jog][pec]< 52){ // Verifica se o jogador é diferente do jogador atual
                             capturarPecas(p, local, pec, jog, i);
                              goto reinicio;
                            }
                          }
                          }


                    }
                         if(local[i][peca - 1]==57){
                             pvenc[i]++;
                             while(pvenc[i]<4){
                               printf("Sua peça chegou ao destino final! Jogue novamente!\n")  ;
                                goto reinicio;
                             }
                            if(pvenc[i]==4){
                                printf("\n\tParabéns Jogador %d, VOCÊ VENCEU O JOGO!!!\n", i+1);
                                vencedor=1;
                                break;
                            }
                        }
					pospecas(i, p);
				}
			} else {
				//dado 1
				cont = 0;
				for(j = 0; j < 4; j++)
					if(p[i].pos[j] != 0){
						cont++;
					}
				if(cont != 0){
					pospecas(i, p);
					peca = informar(dado, 0, p, i);
					if((peca < 1 || peca > 4) || p[i].pos[peca - 1] == 0 || local[i][peca - 1] + dado[0] > 57){
                            if(local[i][0]+ dado[0] > 57 && local[i][1]+ dado[0] > 57 && local[i][2]+ dado[0] > 57 && local[i][3]+ dado[0] > 57)
                                 goto pular;
						do{
							printf("Peca Invalida ou na Posicao Inicial! Digite Novamente.\n");
							peca = informar(dado, 0, p, i);
						}while((peca < 1 || peca > 4) || p[i].pos[peca - 1] == 0 || local[i][peca - 1] + dado[0] > 57);
					}
					if((i != 0) && p[i].pos[peca - 1] + dado[0] > 52){
						p[i].pos[peca - 1] += dado[0] - 52;
						local[i][peca - 1] += dado[0];
					} else {
						p[i].pos[peca - 1] += dado[0];
						local[i][peca - 1] += dado[0];
					}
					for (int pec = 0; pec < 4; pec++) {
                          for (int jog = 0; jog < quant; jog++) {
                           if(p[i].pos[peca - 1] != 0 && p[i].pos[peca - 1] != 1 && p[i].pos[peca - 1] != 9 && p[i].pos[peca - 1] != 14 && p[i].pos[peca - 1] != 22 && p[i].pos[peca - 1] != 27 && p[i].pos[peca - 1] != 35 && p[i].pos[peca - 1] != 40 && p[i].pos[peca - 1] != 48){
                            if(i!=jog && p[i].pos[peca - 1]== p[jog].pos[pec] && local[jog][pec]< 52){ // Verifica se o jogador é diferente do jogador atual
                             capturarPecas(p, local, pec, jog, i);
                              goto reinicio;
                            }
                          }
                          }

                    }
                         if(local[i][peca - 1]==57){
                             pvenc[i]++;
                             while(pvenc[i]<4){
                               printf("Sua peça chegou ao destino final! Jogue novamente!\n")  ;
                                goto reinicio;
                             }
                            if(pvenc[i]==4){
                                printf("\n\tParabéns Jogador %d, VOCÊ VENCEU O JOGO!!!\n", i+1);
                                vencedor=1;
                                break;
                            }
                        }
					pospecas(i, p);
				}
			}
		}
	}while(vencedor != 1);
}
int main(){
	int op, aux = 0, i, j; //op = opção
	srand(time(NULL));
	printf("\n\t\tBem Vindo ao LUDO! Vamos começar nosso jogo...\n");
    sleep(2);
    printf("\n");
    printf("Escolha quantos jogadores irão participar:\n\t(1) 2 Jogadores\n\t(2) 4 Jogadores\n");
	do{
		if(aux != 0)
			printf("\tOpção inválida: Escolha entre as opções 1 e 2!\n");
		     scanf("%d", &op);
		      aux++;
	}while(op != 1 && op != 2);
	system("cls");
	switch (op){
		case 1:{ //Dois Jogadores
           struct pecas p[2];
			for(i = 0; i < 2; i++)
				for(j = 0; j < 4; j++)
					p[i].pos[j] = 0;
			jogo(p, i, 2);
			break;
		}
		case 2:{ //Quatro Jogadores
			struct pecas p[4];
			for(i = 0; i < 4; i++)
				for(j = 0; j < 4; j++)
					p[i].pos[j] = 0;
			jogo(p, i, 4);
			break;
		}
	}
	return 0;
}

