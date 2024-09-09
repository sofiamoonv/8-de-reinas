/*
Programador: NAVARRETE LEON SOFIA LUCIA 
Fecha Entrega: Septiembre 9, 2024
Archivo: ocho_reinas.c
Enlace: 
*/
#include <stdio.h>
#include <stdbool.h>

#define N 8

void imprimirTablero(int tablero[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            printf("%c ", tablero[i][j] ? 'R' : '.');
        printf("\n");
    }
    printf("\n");
}

bool esSeguro(int tablero[N][N], int fila, int col) {
    int i, j;

    // Revisar esta fila a la izquierda
    for (i = 0; i < col; i++)
        if (tablero[fila][i])
            return false;

    // Revisar diagonal superior izquierda
    for (i = fila, j = col; i >= 0 && j >= 0; i--, j--)
        if (tablero[i][j])
            return false;

    // Revisar diagonal inferior izquierda
    for (i = fila, j = col; j >= 0 && i < N; i++, j--)
        if (tablero[i][j])
            return false;

    return true;
}

bool resolverNReinas(int tablero[N][N], int col) {
    if (col >= N)
        return true;

    for (int i = 0; i < N; i++) {
        if (esSeguro(tablero, i, col)) {
            tablero[i][col] = 1;

            if (resolverNReinas(tablero, col + 1))
                return true;

            tablero[i][col] = 0; // Backtrack
        }
    }

    return false;
}

int main() {
    int tablero[N][N] = {{0}};

    if (resolverNReinas(tablero, 0) == false) {
        printf("No existe solución\n");
        return 0;
    }

    imprimirTablero(tablero);
    return 0;
}
