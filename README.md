# lanchonete-trabalho-
lanchonete 

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_PRODUTOS 100

typedef struct {
    char nome[50];
    float preco;
} Produto;

Produto produtos[MAX_PRODUTOS];
int totalProdutos = 0;

void adicionarProduto(const char* nome, float preco) {
    if (totalProdutos < MAX_PRODUTOS) {
        strcpy(produtos[totalProdutos].nome, nome);
        produtos[totalProdutos].preco = preco;
        totalProdutos++;
        printf("Produto adicionado: %s • R$%.2f\n", nome, preco);
    } else {
        printf("Limite de produtos atingido!\n");
    }
}

void listarProdutos() {
    printf("\n--• Lista de Produtos ---\n");
    for (int i = 0; i < totalProdutos; i++) {
        printf("%d. %s • R$%.2f\n", i + 1, produtos[i].nome, produtos[i].preco);
    }
}

float fazerPedido(int indices[], int quantidade) {
    float total = 0;
    for (int i = 0; i < quantidade; i++) {
        if (indices[i] >= 0 && indices[i] < totalProdutos) {
            total += produtos[indices[i]].preco;
        }
    }
    return total;
}

int main() {
    adicionarProduto("Hambúrguer", 15.50);
    adicionarProduto("Refrigerante", 5.00);
    adicionarProduto("Batata Frita", 10.00);

    listarProdutos();

    int pedidos[10];
    int quantidade;

    printf("\nQuantos produtos você deseja pedir? ");
    scanf("%d", &quantidade);

    printf("Digite os números dos produtos (separados por espaço): ");
    for (int i = 0; i < quantidade; i++) {
        scanf("%d", &pedidos[i]);
        pedidos[i]--; // Ajuste para índice de 0
    }

    float total = fazerPedido(pedidos, quantidade);
    printf("Total do pedido: R$%.2f\n", total);

    return 0;
}
