# Application d'une pile : Calculette postfixée

Cette application implémente une calculette en **notation postfixée** (Reverse Polish Notation, RPN), utilisant une pile pour évaluer des expressions arithmétiques simples. La pile permet de gérer les opérandes et les résultats des opérations à mesure que l'expression est lue.

## Fonctionnement de l'algorithme

### Initialisation

La pile est initialisée avec une capacité de 100 éléments et une taille de 0. Elle est utilisée pour stocker les opérandes lors du traitement de l'expression.

### Traitement de l'expression

L'expression est traitée caractère par caractère, selon les règles suivantes :
- **Chiffre** : Si le caractère est un chiffre (`0-9`), il est converti en entier et ajouté à la pile.
- **Opérateur** :
  - Si le caractère est un opérateur (`+`, `-`, `x`), les deux derniers opérandes sont extraits de la pile, l'opération est effectuée, et le résultat est réinséré dans la pile.

### Gestion des erreurs

Des messages d'erreur sont affichés dans les cas suivants :
- **Pas assez de nombres** : Si l'opération nécessite moins de deux opérandes.
- **Trop de nombres** : Si l'expression ne laisse qu'un seul résultat à la fin.
- **Expression invalide** : Si des caractères non numériques ou des opérateurs non supportés sont rencontrés.

### Résultat final

Si l'expression est valide, le résultat est affiché après avoir été extrait de la pile. Sinon, des messages d'erreur sont affichés pour informer l'utilisateur de l'erreur rencontrée.

## Code source

```c
void compute(char* calculus, int calculusSize) {
    // Initialisation de la pile
    Stack s;
    s.capacity = 100;  // Capacité maximale de la pile
    s.size = 0;  // Taille initiale de la pile
    s.tab = (int*)malloc(s.capacity * sizeof(int));  // Allocation dynamique de mémoire pour la pile

    // Vérification de l'allocation mémoire
    if (s.tab == NULL) {
        printf("Memory allocation failed.\n");
        return;
    }

    int i = 0;
    // Boucle pour traiter chaque caractère de l'expression
    while (i < calculusSize) {
        // Si le caractère est un chiffre, on l'ajoute à la pile
        if (isdigit(calculus[i])) {
            push(&s, calculus[i] - '0');  // Conversion du caractère en entier et ajout à la pile
        } 
        // Si l'opérateur est une addition
        else if (calculus[i] == '+') {
            // Vérification qu'il y a suffisamment d'opérandes dans la pile
            if (s.size < 2) {
                printf("NOT ENOUGH NUMBERS\n");  // Erreur si pas assez d'opérandes
                free(s.tab);  // Libération de la mémoire de la pile
                return;
            }
            // On extrait les deux derniers éléments de la pile et on effectue l'addition
            int b = pop(&s);
            int a = pop(&s);
            push(&s, a + b);  // On ajoute le résultat de l'addition dans la pile
        } 
        // Si l'opérateur est une soustraction
        else if (calculus[i] == '-') {
            // Vérification qu'il y a suffisamment d'opérandes dans la pile
            if (s.size < 2) {
                printf("NOT ENOUGH NUMBERS\n");
                free(s.tab);
                return;
            }
            // On extrait les deux derniers éléments de la pile et on effectue la soustraction
            int b = pop(&s);
            int a = pop(&s);
            push(&s, a - b);  // On ajoute le résultat de la soustraction dans la pile
        } 
        // Si l'opérateur est une multiplication
        else if (calculus[i] == 'x') {
            // Vérification qu'il y a suffisamment d'opérandes dans la pile
            if (s.size < 2) {
                printf("NOT ENOUGH NUMBERS\n");
                free(s.tab);
                return;
            }
            // On extrait les deux derniers éléments de la pile et on effectue la multiplication
            int b = pop(&s);
            int a = pop(&s);
            push(&s, a * b);  // On ajoute le résultat de la multiplication dans la pile
        }
        i++;  // On passe au caractère suivant
    }

    // Après avoir traité toute l'expression, on vérifie la taille de la pile
    // Si la pile contient exactement un élément, c'est le résultat
    if (s.size == 1) {
        printf("%d\n", pop(&s));  // Affichage du résultat final
    } 
    // Si la pile est vide, cela signifie qu'il y a eu un manque de nombres dans l'expression
    else if (s.size == 0) {
        printf("NOT ENOUGH NUMBERS\n");
    } 
    // Si la pile contient plus d'un élément, cela signifie qu'il y a trop de nombres non utilisés
    else {
        printf("TOO MANY NUMBERS\n");
    }

    // Libération de la mémoire allouée pour la pile
    free(s.tab);
}
```

### Explication détaillée des parties :

1. **Initialisation de la pile** :
   - Une pile `s` est créée avec une capacité de 100 éléments.
   - La pile est initialement vide (`size = 0`), et de la mémoire est allouée dynamiquement pour les éléments de la pile.

2. **Boucle de traitement de l'expression** :
   - Chaque caractère de l'expression est vérifié pour savoir s'il s'agit d'un chiffre ou d'un opérateur.
   - Si c'est un chiffre, il est converti en entier et ajouté à la pile.
   - Si c'est un opérateur (`+`, `-`, `x`), les deux derniers opérandes sont extraits de la pile, l'opération correspondante est effectuée, puis le résultat est réinséré dans la pile.

3. **Vérifications des erreurs** :
   - Lors de chaque opération, on vérifie si la pile contient au moins deux éléments pour effectuer l'opération.
   - Si ce n'est pas le cas, un message d'erreur est affiché et la fonction retourne immédiatement.
   - À la fin de l'exécution, on vérifie que la pile contient un seul élément, sinon un message d'erreur est affiché pour informer que l'expression était mal formée.

4. **Libération de la mémoire** :
   - À la fin de la fonction, la mémoire allouée pour la pile est libérée, ce qui est essentiel pour éviter les fuites de mémoire.
