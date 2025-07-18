
# La Liste Chaînée

## Description

Une **liste chaînée** est une structure de données linéaire composée d'une séquence d'éléments appelés **cellules**. Chaque cellule contient une **valeur** et un **pointeur vers la cellule suivante**, formant ainsi une chaîne d'éléments liés dynamiquement en mémoire.

### Caractéristiques :
- **Allocation dynamique** : Chaque cellule est allouée séparément, ce qui permet de gérer efficacement l'espace mémoire sans gaspillage.
- **Croissance flexible** : Contrairement aux tableaux, la taille n’a pas besoin d’être définie à l’avance.
- **Manipulation facile** : Les insertions/suppressions en début de liste sont rapides (O(1)).

### Structure :
```c
typedef struct Cellule {
    int value;
    struct Cellule* next;
} *Cell;
````

Chaque cellule contient :

* Un entier `value` : la valeur stockée.
* Un pointeur `next` vers la cellule suivante.

---

## 1. Afficher la liste

```c
void display(Cell c) {
    while(c) {
        printf("%d ", c->value);
        c = c->next;
    }
}
```

* **But** : Parcourir la liste et afficher chaque valeur.
* **Entrée** : `c` : Tête de la liste.
* **Sortie** : Affiche les valeurs sur la sortie standard.
* **Complexité temporelle** : O(n)
* **Description** : La fonction parcourt la liste tant que le pointeur `c` n’est pas nul, et imprime chaque valeur. Elle s’arrête à la fin de la liste.

---

## 2. Insertion en début de liste

```c
Cell insertFirst(Cell c, int value) {
    DEBUG("yo");
    Cell r = createCell(value);
    r->next = c;
    return r;
}
```

* **But** : Ajouter un élément au début de la liste.
* **Entrée** : `c` : Liste existante, `value` : Valeur à insérer.
* **Sortie** : Nouvelle tête de la liste.
* **Complexité temporelle** : O(1)
* **Description** : Une nouvelle cellule est créée, puis son champ `next` est relié à l’ancienne tête. On retourne la nouvelle cellule comme tête.

---

## 3. Insertion en fin de liste

```c
Cell insertLast(Cell c, int value) {
    if (!c) {
        return createCell(value);
    }
    c->next = insertLast(c->next, value);
    return c;
}
```

* **But** : Ajouter un élément à la fin de la liste.
* **Entrée** : `c` : Liste existante, `value` : Valeur à insérer.
* **Sortie** : Tête de la liste modifiée.
* **Complexité temporelle** : O(n)
* **Description** : Fonction récursive. Si la liste est vide, on crée une cellule. Sinon, on appelle `insertLast` sur la cellule suivante, jusqu’à la fin.

---

## 4. Suppression du premier élément

```c
Cell deleteFirst(Cell c) {
    if (c) {
        return c->next;
    }
    return c;
}
```

* **But** : Supprimer l’élément en tête de liste.
* **Entrée** : `c` : Tête de la liste.
* **Sortie** : Nouvelle tête de la liste.
* **Complexité temporelle** : O(1)
* **Description** : Si la liste n’est pas vide, on retourne directement l’élément suivant comme nouvelle tête.

---

## 5. Suppression du dernier élément

```c
Cell deleteLast(Cell c) {
    if (!c || !c->next) return NULL;

    Cell r = c;
    while (c->next->next) {
        c = c->next;
    }
    c->next = NULL;
    return r;
}
```

* **But** : Supprimer le dernier élément de la liste.
* **Entrée** : `c` : Tête de la liste.
* **Sortie** : Tête de la liste modifiée.
* **Complexité temporelle** : O(n)
* **Description** : On parcourt jusqu’à l’avant-dernier élément, puis on met son `next` à `NULL`. La cellule terminale est ainsi supprimée.

---

## 6. Longueur de la liste

```c
int length(Cell c) {
    int l = 0;
    while (c) {
        c = c->next;
        l++;
    }
    return l;
}
```

* **But** : Compter le nombre d’éléments dans la liste.
* **Entrée** : `c` : Tête de la liste.
* **Sortie** : Nombre d’éléments (entier).
* **Complexité temporelle** : O(n)
* **Description** : On parcourt toute la liste et on incrémente un compteur à chaque cellule.

---

## 7. Insertion à une position donnée

```c
Cell randomInsert(Cell c, int pos, int value) {
    if (pos == 0 || !c) {
        Cell n = createCell(value);
        n->next = c;
        return n;
    }
    c->next = randomInsert(c->next, pos - 1, value);
    return c;
}
```

* **But** : Insérer un élément à la position `pos` dans la liste.
* **Entrée** : `c` : Liste existante, `pos` : Position cible, `value` : Valeur à insérer.
* **Sortie** : Tête de la liste modifiée.
* **Complexité temporelle** : O(n)
* **Description** : Si `pos == 0`, on insère en tête. Sinon, on insère récursivement dans la suite de la liste jusqu'à atteindre la bonne position.
---

### Résumé

| Opération      | But                             | Complexité |
| -------------- | ------------------------------- | ---------- |
| `display`      | Afficher les valeurs            | O(n)       |
| `insertFirst`  | Ajouter en tête                 | O(1)       |
| `insertLast`   | Ajouter en fin                  | O(n)       |
| `deleteFirst`  | Supprimer le premier élément    | O(1)       |
| `deleteLast`   | Supprimer le dernier élément    | O(n)       |
| `length`       | Compter le nombre d'éléments    | O(n)       |
| `randomInsert` | Insertion à une position donnée | O(n)       |

Cette implémentation de **liste chaînée simple** permet une gestion flexible de données, très utile pour les piles, files, ou tout système nécessitant une collection dynamique.

```
