#include <stdio.h>

// Função para imprimir o tabuleiro
void imprimirTabuleiro(char tabuleiro[3][3]) {
    printf("\nTabuleiro:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%c ", tabuleiro[i][j]);
        }
        printf("\n");
    }
}

// Função para verificar se alguém ganhou
int verificarVencedor(char tabuleiro[3][3]) {
    // Verificar linhas e colunas
    for (int i = 0; i < 3; i++) {
        if (tabuleiro[i][0] == tabuleiro[i][1] && tabuleiro[i][1] == tabuleiro[i][2] && tabuleiro[i][0] != ' ') {
            return 1; // Alguém ganhou
        }
        if (tabuleiro[0][i] == tabuleiro[1][i] && tabuleiro[1][i] == tabuleiro[2][i] && tabuleiro[0][i] != ' ') {
            return 1; // Alguém ganhou
        }
    }

// Verificar diagonais
    if (tabuleiro[0][0] == tabuleiro[1][1] && tabuleiro[1][1] == tabuleiro[2][2] && tabuleiro[0][0] != ' ') {
        return 1; // Alguém ganhou
    }
    if (tabuleiro[0][2] == tabuleiro[1][1] && tabuleiro[1][1] == tabuleiro[2][0] && tabuleiro[0][2] != ' ') {
        return 1; // Alguém ganhou
    }
    
  // Verificar se é um empate
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (tabuleiro[i][j] == ' ') {
                return 0; // Jogo não terminou
            }
        }
    }

  return -1; // É um empate
}

int main() {
    char tabuleiro[3][3] = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };
    int vezDoX = 1; // Se for 1, é a vez do 'X', se for 0, é a vez do 'O'
    int linha, coluna;
    int jogadaValida = 0;
    do {
        imprimirTabuleiro(tabuleiro);
        // Obter a jogada do jogador atual
        do {
            printf("\nJogador %c, insira a linha e a coluna (1-3) separadas por espaço: ", vezDoX ? 'X' : 'O');
            scanf("%d %d", &linha, &coluna);
            linha--;
            coluna--;
            // Verificar se a jogada é válida
            if (linha >= 0 && linha < 3 && coluna >= 0 && coluna < 3 && tabuleiro[linha][coluna] == ' ') {
                jogadaValida = 1;
            } else {
                printf("Jogada inválida. Tente novamente.\n");
            }
        } while (!jogadaValida);
        // Marcar a jogada no tabuleiro
        tabuleiro[linha][coluna] = vezDoX ? 'X' : 'O';
        // Trocar a vez do jogador
        vezDoX = !vezDoX;
        // Verificar se alguém ganhou ou se é um empate
        int resultado = verificarVencedor(tabuleiro);
        if (resultado == 1) {
            imprimirTabuleiro(tabuleiro);
            printf("\nParabéns! Jogador %c venceu!\n", vezDoX ? 'O' : 'X');
            break;
        } else if (resultado == -1) {
            imprimirTabuleiro(tabuleiro);
            printf("\nEmpate! O jogo acabou.\n");
            break;
        }
    } while (1); // Loop infinito, termina quando o jogo acaba
    return 0;
}
