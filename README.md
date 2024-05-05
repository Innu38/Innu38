### Hi there 👋

<!--
**Innu38/Innu38** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
#include <stdio.h>
#include <stdlib.h>

// Structure pour un élément de la liste chaînée
struct Node {
    int data;
    struct Node* next;
};

// Fonction pour ajouter un élément à la fin de la liste
void append(struct Node** head, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = NULL;

    if (*head == NULL) {
        *head = newNode;
    } else {
        struct Node* current = *head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
    }
}

// Fonction pour supprimer un élément de la liste
void delete(struct Node** head, int value) {
    if (*head == NULL) {
        return;
    }

    struct Node* temp = *head;
    if (temp->data == value) {
        *head = temp->next;
        free(temp);
        return;
    }

    while (temp->next != NULL && temp->next->data != value) {
        temp = temp->next;
    }

    if (temp->next == NULL) {
        return;
    }

    struct Node* toDelete = temp->next;
    temp->next = toDelete->next;
    free(toDelete);
}

// Fonction pour rechercher un élément dans la liste
int search(struct Node* head, int value) {
    struct Node* current = head;
    while (current != NULL) {
        if (current->data == value) {
            return 1; // Trouvé
        }
        current = current->next;
    }
    return 0; // Non trouvé
}

// Fonction pour afficher la liste
void display(struct Node* head) {
    struct Node* current = head;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->next;
    }
    printf("\n");
}

// Exemple d'utilisation
int main() {
    struct Node* myList = NULL;

    append(&myList, 10);
    append(&myList, 20);
    append(&myList, 30);

    printf("Liste initiale : ");
    display(myList);

    delete(&myList, 20);
    printf("Après suppression de 20 : ");
    display(myList);

    printf("Recherche de 30 : %s\n", search(myList, 30) ? "Trouvé" : "Non trouvé");

    return 0;
}
c++