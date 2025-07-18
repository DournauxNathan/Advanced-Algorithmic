# La Liste Chaînée – Partie 2

## Description

Cette deuxième partie enrichit l’implémentation de la **liste chaînée** avec des opérations plus avancées telles que la recherche d’un élément, l’inversion de la liste, le tri, la fusion de deux listes triées, l’insertion ordonnée, et la suppression des doublons.

Ces fonctions permettent d’exploiter pleinement les avantages dynamiques de la liste chaînée, et sont particulièrement utiles dans les algorithmes où la flexibilité de taille et la manipulation fréquente des éléments sont nécessaires.

---

## 1. Rechercher une valeur (`contains`)

```c
int contains(Cell c, int val) {
    while (c) {
        if (c->value == val) return 1;
        c = c->next;
    }
    return 0;
}
````

* **But** : Vérifier si une valeur est présente dans la liste.
* **Entrée** : `c` : Liste à parcourir, `val` : Valeur recherchée.
* **Sortie** : 1 si la valeur est trouvée, 0 sinon.
* **Complexité temporelle** : O(n)
* **Description** : La fonction parcourt la liste et renvoie 1 dès qu'elle trouve un élément correspondant. Sinon, elle retourne 0 après avoir parcouru toute la liste.

---

## 2. Inverser la liste (`invert`)

```c
Cell invert(Cell c) {
    Cell nc = NULL;
    Cell tmp;
    while (c) {
        tmp = c;
        c = c->next;
        tmp->next = nc;
        nc = tmp;
    }
    return nc;
}
```

* **But** : Inverser l’ordre des éléments de la liste.
* **Entrée** : `c` : Liste d’origine.
* **Sortie** : Nouvelle tête de la liste inversée.
* **Complexité temporelle** : O(n)
* **Description** : À chaque itération, l’élément courant est déplacé en tête de la nouvelle liste. On modifie dynamiquement les liens entre les cellules.

---

## 3. Fusion de deux listes triées (`merge`)

```c
Cell merge(Cell a, Cell b) {
    if (!a) return b;
    if (!b) return a;

    if (a->value < b->value) {
        a->next = merge(a->next, b);
        return a;
    }
    b->next = merge(a, b->next);
    return b;
}
```

* **But** : Fusionner deux listes triées en une seule triée.
* **Entrée** : `a`, `b` : Deux listes triées.
* **Sortie** : Nouvelle liste triée fusionnée.
* **Complexité temporelle** : O(n + m), où `n` et `m` sont les tailles des deux listes.
* **Description** : L’algorithme compare récursivement les têtes des deux listes et relie les plus petites valeurs en priorité.

---

## 4. Insertion ordonnée (`insert`)

```c
Cell insert(Cell c, int value) {
    if (!c) {
        return createCell(value);
    }
    if (c->value > value) {
        Cell n = createCell(value);
        n->next = c;
        return n;
    }
    c->next = insert(c->next, value);
    return c;
}
```

* **But** : Insérer un élément dans une liste triée en maintenant l’ordre.
* **Entrée** : `c` : Liste triée, `value` : Valeur à insérer.
* **Sortie** : Nouvelle tête de la liste.
* **Complexité temporelle** : O(n)
* **Description** : Si la valeur est inférieure à l’élément courant, elle est insérée avant. Sinon, la fonction s'appelle récursivement pour continuer la recherche de la bonne position.

---

## 5. Suppression des doublons (`simplify`)

```c
Cell simplify(Cell c) {
    if (!c) return c;

    Cell result = createCell(c->value);
    Cell last = result;
    c = c->next;

    while (c) {
        int v = c->value;
        c = c->next;

        // Chercher si v existe déjà dans le résultat
        Cell cur = result;
        while (cur) {
            if (cur->value == v) break;
            cur = cur->next;
        }

        // Si v est déjà présent, on ignore
        if (cur) continue;

        // Sinon on l'ajoute à la fin
        last->next = createCell(v);
        last = last->next;
    }

    return result;
}
```

* **But** : Supprimer les doublons d’une liste chaînée.
* **Entrée** : `c` : Liste initiale.
* **Sortie** : Nouvelle liste sans doublons.
* **Complexité temporelle** : O(n²)
* **Description** : On parcourt chaque élément et on le compare à ceux déjà stockés dans la nouvelle liste (`result`). Si la valeur est unique, on l'ajoute à la fin.

---

## 6. Tri par échange (Bubble Sort) (`sort`)

```c
void myswap(int& a, int& b) {
    a ^= b ^= a ^= b;
}

Cell sort(Cell c) {
    while (true) {
        bool swap = false;
        Cell cur = c;

        while (cur && cur->next) {
            if (cur->value > cur->next->value) {
                myswap(cur->value, cur->next->value);
                swap = true;
            }
            cur = cur->next;
        }

        if (!swap) break;
    }
    return c;
}
```

* **But** : Trier la liste chaînée par ordre croissant.
* **Entrée** : `c` : Liste à trier.
* **Sortie** : Tête de la liste triée.
* **Complexité temporelle** : O(n²)
* **Description** : Implémente un **tri à bulles** sur les valeurs des cellules. Les échanges sont réalisés via une astuce XOR (`myswap`), sans variable temporaire.

---

### Résumé

| Opération  | But                              | Complexité |
| ---------- | -------------------------------- | ---------- |
| `contains` | Vérifie la présence d’une valeur | O(n)       |
| `invert`   | Inverse la liste                 | O(n)       |
| `merge`    | Fusionne deux listes triées      | O(n + m)   |
| `insert`   | Insertion triée                  | O(n)       |
| `simplify` | Supprime les doublons            | O(n²)      |
| `sort`     | Trie les valeurs (tri à bulles)  | O(n²)      |

---

Avec cette deuxième partie, on dispose d’un ensemble d’opérations robustes pour gérer et manipuler efficacement des listes chaînées dynamiques, y compris dans des contextes d’algorithmes plus poussés comme le tri ou la fusion de listes ordonnées.

