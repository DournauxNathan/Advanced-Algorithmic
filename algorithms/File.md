# La File

## Description

Une **file** est une structure de données de type **FIFO (First In, First Out)**, ce qui signifie que le premier élément ajouté sera le premier à être retiré. Elle fonctionne de manière similaire à une file d'attente dans la vie réelle, comme une file au guichet d'un magasin où les clients sont servis dans l'ordre de leur arrivée.

### Caractéristiques :
- **Insertion (Enfiler)** : Un élément est ajouté à la fin de la file.
- **Retrait (Défiler)** : L'élément situé en tête de la file est retiré.
- **Accès** : Un accès direct à l'élément au début (tête) et à la fin (queue) de la file.

### Avantages :
- **Gestion séquentielle** : Elle permet un traitement séquentiel des éléments, garantissant que les éléments sont traités dans l'ordre dans lequel ils sont arrivés.
- **Utilisation courante** : Les files sont couramment utilisées dans les systèmes où l'ordre d'exécution ou de traitement est important, comme dans la gestion de processus, la simulation d'événements, ou encore pour implémenter des systèmes de type "buffet" (systèmes de gestion de ressources).

### Structure :
Une file peut être implémentée à l'aide d'un tableau ou d'une liste chaînée. Dans cette implémentation particulière, une **file circulaire** est utilisée pour gérer la mémoire de manière plus efficace, évitant le déplacement des éléments lorsque la tête ou la fin de la file change.

- **Tableau circulaire** : Le tableau est conçu pour se connecter sur lui-même à la fin. Ainsi, lorsque l'élément en tête est retiré et que de nouveaux éléments sont ajoutés, la mémoire est utilisée de manière optimale, sans gaspillage.

## Opérations principales :
1. **Tester si la file est vide** (`isEmpty`) : Vérifie si la taille de la file est nulle.
2. **Tester si la file est pleine** (`isFull`) : Vérifie si la file a atteint sa capacité maximale.
3. **Afficher la file** (`display`) : Affiche tous les éléments de la file depuis la tête jusqu'à la fin.
4. **Enfiler** (`push`) : Ajoute un élément à la fin de la file.
5. **Défiler** (`pop`) : Retire l'élément à la tête de la file.

## Complexité :
- **Insertion (push)** : O(1)
- **Retrait (pop)** : O(1)
- **Vérification (isEmpty, isFull)** : O(1)
- **Affichage (display)** : O(n), où `n` est le nombre d'éléments dans la file.

---

Les fichiers sont particulièrement utiles pour des implémentations telles que les systèmes d'attente (comme les file d'attente dans un service client) ou pour la gestion des processus dans un système d'exploitation. Elles peuvent également être utilisées dans les algorithmes de parcours en largeur ou dans des applications de simulation.

---

Je comprends mieux maintenant. Voici la documentation du code dans le format que vous demandez :

```markdown
# Gestion de la File

## 1. Tester si la file est vide

```c
int isEmpty(Queue* q)
{
    return q->size == 0; 
}
```
- **But de l'algorithme** : Vérifier si la file est vide.
- **Entrée** : `q` : Pointeur vers la file.
- **Sortie** : 1 si la file est vide, sinon 0.
- **Complexité temporelle** : O(1).
- **Description** : La fonction vérifie si la taille de la file est égale à 0. Si c'est le cas, la file est vide, sinon elle contient des éléments.

---

## 2. Tester si la file est pleine

```c
int isFull(Queue* q)
{
    return q->size == q->capacity; 
}
```
- **But de l'algorithme** : Vérifier si la file est pleine.
- **Entrée** : `q` : Pointeur vers la file.
- **Sortie** : 1 si la file est pleine, sinon 0.
- **Complexité temporelle** : O(1).
- **Description** : La fonction vérifie si la taille de la file est égale à sa capacité maximale. Si c'est le cas, la file est pleine, sinon elle peut encore contenir des éléments.

---

## 3. Afficher les éléments de la file

```c
void display(Queue* q)
{
    int i = q->start;  

    for (int j = 0; j < q->size; j++)
    {
        printf("%d ", q->tab[i]);  
        i = (i + 1) % q->capacity;  
    }
}
```
- **But de l'algorithme** : Afficher les éléments de la file depuis le début jusqu'à la fin.
- **Entrée** : `q` : Pointeur vers la file.
- **Sortie** : Affichage des éléments de la file dans l'ordre d'insertion.
- **Complexité temporelle** : O(n), où `n` est la taille de la file.
- **Description** : La fonction parcourt les éléments de la file, à partir de la position de départ (`q->start`), et les affiche un par un. Le calcul de `(i + 1) % q->capacity` permet de gérer la circulation de la file dans un tableau circulaire.

---

## 4. Enfiler un élément

```c
void push(Queue* q, int value)
{
    int position = (q->start + q->size) % q->capacity;

    q->tab[position] = value;

    q->size++;  
}
```
- **But de l'algorithme** : Ajouter un élément à la fin de la file.
- **Entrée** : `q` : Pointeur vers la file, `value` : L'élément à ajouter.
- **Sortie** : Aucune. L'élément est ajouté à la file.
- **Complexité temporelle** : O(1).
- **Description** : La fonction calcule la position de l'élément à ajouter à la fin de la file en utilisant `(q->start + q->size) % q->capacity`, puis insère l'élément à cette position. Après l'ajout, la taille de la file est incrémentée.

---

## 5. Défiler un élément

```c
int pop(Queue* q)
{
    int value = q->tab[q->start];  

    q->start = (q->start + 1) % q->capacity;  
    
    q->size--;  
    
    return value;
}
```
- **But de l'algorithme** : Retirer le premier élément de la file.
- **Entrée** : `q` : Pointeur vers la file.
- **Sortie** : La valeur du premier élément de la file.
- **Complexité temporelle** : O(1).
- **Description** : La fonction retire le premier élément de la file, met à jour la position de départ de la file en utilisant `(q->start + 1) % q->capacity`, et décrémente la taille de la file.

---

### Résumé :

- **isEmpty** : Vérifie si la file est vide.
- **isFull** : Vérifie si la file est pleine.
- **display** : Affiche les éléments de la file dans l'ordre d'insertion.
- **push** : Ajoute un élément à la fin de la file.
- **pop** : Retire l'élément au début de la file.

Cette implémentation utilise une gestion circulaire de la mémoire pour une gestion efficace de la file sans nécessiter de déplacements d'éléments dans le tableau.
