### Description générale de la pile (Stack)

Une **pile** est une structure de données linéaire qui suit le principe **LIFO** (Last In, First Out), c'est-à-dire que le dernier élément ajouté à la pile est le premier à en être retiré. Cela la rend idéale pour des situations où on souhaite traiter des éléments dans un ordre inversé de leur arrivée.

#### Fonctionnement :
- **Empiler (push)** : On ajoute un élément au sommet de la pile.
- **Dépiler (pop)** : On retire l'élément du sommet de la pile.
- **Top** : On accède à l'élément en haut de la pile sans le retirer.
- **Vider (isEmpty)** : On vérifie si la pile ne contient aucun élément.
- **Pleine (isFull)** : On vérifie si la pile a atteint sa capacité maximale, dans le cas où la taille de la pile est limitée.

#### Applications courantes :
Les piles sont couramment utilisées dans des algorithmes où les éléments doivent être traités dans un ordre spécifique, comme :
- **Gestion des appels de fonctions (pile d'exécution)** : Chaque appel de fonction est empilé sur la pile d'exécution, et une fois la fonction terminée, elle est dépilée.
- **Analyse syntaxique (par exemple dans les langages de programmation)** : Les piles sont utilisées dans les analyseurs de syntaxe pour vérifier la validité de parenthèses et d'autres structures.
- **Parcours de graphes (DFS)** : Une pile peut être utilisée pour implémenter le parcours en profondeur (Depth-First Search) d'un graphe.
- **Évaluation d'expressions (notamment les expressions postfixées)** : Les piles permettent de gérer l'évaluation des expressions où les opérateurs suivent les opérandes.

#### Structure de données :
La pile est souvent implémentée à l'aide de :
- **Tableaux dynamiques** : On utilise un tableau pour contenir les éléments et une variable pour suivre le sommet de la pile.
- **Listes chaînées** : Une approche basée sur des noeuds qui contiennent des valeurs et des pointeurs vers les éléments précédents.

En résumé, la pile est une structure de données simple et efficace pour la gestion d'éléments dans des situations où l'ordre inverse est requis. Elle est largement utilisée dans les systèmes informatiques pour des tâches comme la gestion des appels de fonctions, l'analyse syntaxique, et les algorithmes de recherche.

---
## Les Piles (Stacks)

Une pile est une structure de données de type LIFO (Last In, First Out), c'est-à-dire que le dernier élément ajouté à la pile est le premier à en être retiré.

### 1. Tester si la pile est vide
```c
int isEmpty(Stack* s)
{
    return s->size == 0; 
}
```
- **But de l'algorithme** : Vérifier si la pile est vide.
- **Entrée** :
  - `s` : Pointeur vers la pile.
- **Sortie** : `1` si la pile est vide, sinon `0`.
- **Complexité temporelle** : O(1).
- **Description** : La fonction vérifie si la taille de la pile est égale à 0. Si c'est le cas, la pile est vide, sinon elle contient des éléments.

---

### 2. Tester si la pile est pleine
```c
int isFull(Stack* s)
{
    return s -> size == s -> capacity;
}
```
- **But de l'algorithme** : Vérifier si la pile est pleine.
- **Entrée** :
  - `s` : Pointeur vers la pile.
- **Sortie** : `1` si la pile est pleine, sinon `0`.
- **Complexité temporelle** : O(1).
- **Description** : La fonction vérifie si la taille de la pile est égale à sa capacité maximale. Si c'est le cas, la pile est pleine.

---

### 3. Affichage depuis le fond de la pile
```c
void displayFromBottom(Stack* s) 
{
    for (int i = 0; i < s->size; i++) 
    {
        printf("%d ", s->tab[i]); 
    }
    printf("\n");
}
```
- **But de l'algorithme** : Afficher les éléments de la pile depuis le fond jusqu'au dessus.
- **Entrée** :
  - `s` : Pointeur vers la pile.
- **Sortie** : Affichage des éléments de la pile depuis le fond.
- **Complexité temporelle** : O(n), où n est la taille de la pile.
- **Description** : Cette fonction parcourt les éléments de la pile en partant du fond (indice 0) et affiche chaque élément.

---

### 4. Affichage depuis le dessus de la pile
```c
void displayFromTop(Stack* s) 
{
    if (s->size == 0)
    {
        printf("La pile est vide.\n");
        return;  
    }

    for (int i = s->size - 1; i >= 0; i--) 
    {
        printf("%d ", s->tab[i]); 
    }
    
    printf("\n"); 
}
```
- **But de l'algorithme** : Afficher les éléments de la pile depuis le dessus jusqu'au fond.
- **Entrée** :
  - `s` : Pointeur vers la pile.
- **Sortie** : Affichage des éléments de la pile depuis le dessus.
- **Complexité temporelle** : O(n), où n est la taille de la pile.
- **Description** : Cette fonction affiche les éléments de la pile en partant du dessus (le dernier élément ajouté) et en allant vers le fond.

---

### 5. Empiler un élément
```c
void push(Stack* s, int val)
{
    if (s -> size < s -> capacity) 
    {
        s -> tab[s -> size++] = val;  
    } 
    else 
    {
        debug("La pile est pleine, impossible d'ajouter l'élément.\n");
    }
}
```
- **But de l'algorithme** : Ajouter un élément au sommet de la pile.
- **Entrée** :
  - `s` : Pointeur vers la pile.
  - `val` : La valeur à empiler.
- **Sortie** : Aucun, mais un message d'erreur est affiché si la pile est pleine.
- **Complexité temporelle** : O(1).
- **Description** : La fonction vérifie d'abord si la pile n'est pas pleine, puis ajoute l'élément à la fin du tableau représentant la pile. Si la pile est pleine, un message d'erreur est affiché.

---

### 6. Dépiler un élément
```c
int pop(Stack* s)
{
    if (s->size > 0)
    {
        int val = s->tab[s->size - 1];
        
        s->size--;  
        
        return val; 
    }
    else 
    {
        debug("La pile est vide, impossible de dépiler.\n");
        
        return -1;
    }
}
```
- **But de l'algorithme** : Retirer et retourner l'élément du sommet de la pile.
- **Entrée** :
  - `s` : Pointeur vers la pile.
- **Sortie** : La valeur du sommet de la pile, ou `-1` si la pile est vide.
- **Complexité temporelle** : O(1).
- **Description** : Cette fonction vérifie si la pile contient des éléments. Si oui, elle retire l'élément du sommet et décrémente la taille de la pile. Si la pile est vide, un message d'erreur est affiché et la fonction retourne `-1`.
