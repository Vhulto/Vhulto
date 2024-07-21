#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define NUM_ITENS 10

// definição dos nomes para os itens
char* nomes_itens[NUM_ITENS] = {
    "faca",
    "espada",
    "machado",
    "arco",
    "lança",
    "escudo",
    "martelo",
    "adaga",
    "cimitarra",
    "clava"
};

typedef struct {
    int indice;
    int probabilidade;
} Item;

// número aleatorio entre 0 e 99
int random_number() {
    return rand() % 100;
}

// indice do item baseado nas probabilidades
int determinar_indice_item(Item* itens, int num_itens) {
    int r = random_number();
    int total_probabilidades = 0;

    // prob
    for (int i = 0; i < num_itens; i++) {
        total_probabilidades += itens[i].probabilidade;
    }

    // num aleatorio
    r = r % total_probabilidades;

    // Encontra o item correspondente ao número aleatório
    int acumulado = 0;
    for (int i = 0; i < num_itens; i++) {
        acumulado += itens[i].probabilidade;
        if (r < acumulado) {
            return itens[i].indice;
        }
    }

    return -1;
}

int main() {
    // itens com seus indices e probabilidades
    Item itens[NUM_ITENS] = {
        {0, 50},   // 0 "faca"
        {1, 10},   // 1 "espada"
        {2, 10},   // 2 "machado"
        {3, 5},    // 3 "arco"
        {4, 15},   // 4 "lança"
        {5, 20},   // 5 "escudo"
        {6, 30},   // 6 "martelo"
        {7, 25},   // 7 "adaga"
        {8, 8},    // 8 "cimitarra"
        {9, 12}    // 9 "clava"
    };

    srand(time(NULL));  

    int indice_resultado = determinar_indice_item(itens, NUM_ITENS);

    if (indice_resultado >= 0 && indice_resultado < NUM_ITENS) {
        char* nome_item = nomes_itens[indice_resultado];
        printf("Resultado: %s\n", nome_item);
    } else {
        printf("Erro.\n");
    }

    return 0;
}
