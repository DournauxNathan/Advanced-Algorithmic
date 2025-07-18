# Liste Doublement Chaînée

## Description

Une **liste doublement chaînée** est une structure linéaire dans laquelle chaque cellule contient :
- un **pointeur vers la cellule suivante** (`next`) ;
- un **pointeur vers la cellule précédente** (`previous`).

Cette structure permet une navigation fluide **dans les deux directions**, ce qui facilite certaines opérations comme l’inversion, la suppression ou l’insertion à des positions relatives.

### Caractéristiques :
- Accès bidirectionnel.
- Généralement circulaire (comme ici), ce qui évite les `NULL` et permet des parcours infinis.
- Chaque cellule a deux liaisons : avant et arrière.

### Structure :
```c
typedef struct Cellule {
    int value;
    struct Cellule* next;
    struct Cellule* previous;
} *Cell;
````

---

## 1. Affichage en sens inverse (`reverseDisplay`)

```c
void reverseDisplay(Cell c) {
    if (!c) return;

    Cell last = c->previous;
    c = c->previous;

    while (1) {
        printf("%d ", c->value);
        c = c->previous;
        if (c == last) break;
    }

    DEBUG("test");
    printf("\n");
}
```

* **But** : Afficher les éléments de la liste en partant de la fin vers le début.
* **Entrée** : `c` : Pointeur vers une cellule quelconque de la liste.
* **Sortie** : Affichage des valeurs en ordre inverse.
* **Complexité temporelle** : O(n)
* **Description** : On part du dernier élément (`c->previous`) et on recule à chaque itération jusqu’à revenir à ce dernier.

---

## 2. Suppression du premier élément (`removeFirst`)

```c
Cell removeFirst(Cell c) {
    if (!c) return c;
    if (c->next == c) return NULL;

    c->previous->next = c->next;
    c->next->previous = c->previous;
    return c->next;
}
```

* **But** : Supprimer le premier élément de la liste.
* **Entrée** : `c` : Pointeur vers la tête de la liste.
* **Sortie** : Nouvelle tête de la liste.
* **Complexité temporelle** : O(1)
* **Description** : Les liens entre les deux cellules entourant la tête sont mis à jour pour l'exclure. Si un seul élément, la liste devient vide.

---

## 3. Suppression du dernier élément (`removeLast`)

```c
Cell removeLast(Cell c) {
    if (!c || c->next == c) return NULL;

    Cell last = c->previous;
    last->next->previous = last->previous;
    last->previous->next = last->next;
    return c;
}
```

* **But** : Supprimer le dernier élément de la liste.
* **Entrée** : `c` : Pointeur vers une cellule de la liste.
* **Sortie** : Cellule `c` inchangée, sauf si la liste devient vide.
* **Complexité temporelle** : O(1)
* **Description** : Le dernier élément est supprimé en mettant à jour les pointeurs de ses voisins.

---

## 4. Insertion à une position donnée (`insert`)

```c
Cell insert(Cell c, int pos, int value) {
    Cell first = c;
    Cell n = createCell(value);

    if (!c) {
        n->next = n;
        n->previous = n;
        return n;
    }

    if (pos == 0) {
        n->next = c;
        n->previous = c->previous;
        n->previous->next = n;
        c->previous = n;
        return n;
    }

    if (pos > 0) {
        while (pos > 1 && c->next != first) {
            pos--;
            c = c->next;
        }
        n->next = c->next;
        n->previous = c;
        n->previous->next = n;
        n->next->previous = n;
        return first;
    } else {
        while (pos < -1 && c->previous != first) {
            pos++;
            c = c->previous;
        }
        if (c->previous == first && pos < -1) {
            n->previous = first->previous;
            n->next = first;
            n->previous->next = n;
            n->next->previous = n;
            return n;
        }
        n->previous = c->previous;
        n->next = c;
        n->previous->next = n;
        n->next->previous = n;
        return first;
    }

    return c;
}
```

* **But** : Insérer un élément à la position `pos` dans la liste.
* **Entrée** : `c` : Cellule de départ (tête), `pos` : Position relative (positive ou négative), `value` : Valeur à insérer.
* **Sortie** : Nouvelle tête de liste ou ancienne si l’insertion n’est pas en tête.
* **Complexité temporelle** : O(n)
* **Description** :

  * Si `pos == 0`, insertion en tête.
  * Si `pos > 0`, on avance vers l’avant.
  * Si `pos < 0`, on recule vers l’arrière.
  * Les pointeurs `next` et `previous` sont mis à jour pour insérer proprement la nouvelle cellule.

---

### Résumé

| Opération        | But                                  | Complexité |
| ---------------- | ------------------------------------ | ---------- |
| `reverseDisplay` | Affiche les éléments en sens inverse | O(n)       |
| `removeFirst`    | Supprime le premier élément          | O(1)       |
| `removeLast`     | Supprime le dernier élément          | O(1)       |
| `insert`         | Insère à une position donnée         | O(n)       |

---

Les **listes doublement chaînées circulaires** offrent une flexibilité maximale pour naviguer et modifier les données. Elles sont particulièrement adaptées aux **structures de navigation**, **systèmes de cache**, ou pour modéliser des **éléments connectés dans les deux sens**.
