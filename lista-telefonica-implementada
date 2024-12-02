#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>


#define TAMANHO 101 // tamanho da tabela hash


typedef struct Contato {

    char nome[50];
    char telefone[20];
    struct Contato* proximo; // tratamento de colisões

} Contato;


// tabela hash

Contato* tabelaHash[TAMANHO];


// hash simples

int funcaoHash(const char* nome) {

    int hash = 0;

    while (*nome) {

        hash = (hash + *nome) % TAMANHO;
        nome++;

    }

    return hash;

}


// declarando a function buscarPorNome

Contato* buscarPorNome(const char* nome);


// function que adiciona um contato

void adicionarContato() {

    char nome[50], telefone[20];
    printf("Digite o nome: ");
    scanf("%s", nome);
    printf("Digite o telefone: ");
    scanf("%s", telefone);

    int indice = funcaoHash(nome);


    // verificando se o contato já existe

    Contato* contatoExistente = buscarPorNome(nome);

    if (contatoExistente) {

        printf("Contato já existe. Atualizando número.\n");
        strcpy(contatoExistente->telefone, telefone);

        return;

    }


    // criando um novo contato

    Contato* novo = (Contato*) malloc(sizeof(Contato));
    strcpy(novo->nome, nome);
    strcpy(novo->telefone, telefone);
    novo->proximo = tabelaHash[indice];
    tabelaHash[indice] = novo;

    printf("Contato adicionado com sucesso.\n");

}


// function que busca um contato pelo nome

Contato* buscarPorNome(const char* nome) {

    int indice = funcaoHash(nome);
    Contato* atual = tabelaHash[indice];

    while (atual) {

        if (strcmp(atual->nome, nome) == 0) {

            return atual;

        }

        atual = atual->proximo;

    }

    return NULL;

}


// function que busca um contato

void buscarContato() {

    char nome[50];
    printf("Digite o nome para buscar: ");
    scanf("%s", nome);

    clock_t inicio = clock();
    Contato* contato = buscarPorNome(nome);
    clock_t fim = clock();

    if (contato) {

        printf("Telefone de %s: %s\n", contato->nome, contato->telefone);
        printf("Tempo de busca: %.2f ms\n", (double)(fim - inicio) / CLOCKS_PER_SEC * 1000);

    } else {

        printf("Contato não encontrado.\n");

    }
}


// function que remove um contato

void removerContato() {

    char nome[50];
    printf("Digite o nome para remover: ");
    scanf("%s", nome);

    int indice = funcaoHash(nome);
    Contato* atual = tabelaHash[indice];
    Contato* anterior = NULL;

    while (atual) {

        if (strcmp(atual->nome, nome) == 0) {

            if (anterior) {

                anterior->proximo = atual->proximo;

            } else {

                tabelaHash[indice] = atual->proximo;

            }

            free(atual);
            printf("Contato removido com sucesso.\n");

            return;

        }

        anterior = atual;
        atual = atual->proximo;

    }

    printf("Contato não encontrado.\n");

}


// function que exibe todos os contatos

void exibirContatos() {

    for (int i = 0; i < TAMANHO; i++) {

        Contato* atual = tabelaHash[i];

        if (atual) {

            printf("Índice %d:\n", i);

            while (atual) {

                printf("Nome: %s, Telefone: %s\n", atual->nome, atual->telefone);
                atual = atual->proximo;

            }
        }
    }
}


int main() {

    int opcao;

    do {

        printf("\nEscolha uma opção:\n");
        printf("1 - Adicionar contato\n");
        printf("2 - Buscar contato por nome\n");
        printf("3 - Remover contato\n");
        printf("4 - Exibir todos os contatos\n");
        printf("0 - Sair\n");
        printf("Digite o número da opcão correspondente: ");
        
        scanf("%d", &opcao);

        switch (opcao) {

            case 1:
                adicionarContato();
                break;

            case 2:
                buscarContato();
                break;

            case 3:
                removerContato();
                break;

            case 4:
                exibirContatos();
                break;

            case 0:
                printf("Saindo.\n");
                break;

            default:
                printf("Opção inválida! Tente novamente!\n");

        }

    } while (opcao != 0);

    return 0;

}
