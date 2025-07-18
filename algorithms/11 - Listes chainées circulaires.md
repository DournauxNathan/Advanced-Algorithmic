# Liste Chaînée Circulaire

## Description

Une **liste chaînée circulaire** est une variante de la liste chaînée où **la dernière cellule pointe vers la première**, formant un cycle fermé. Contrairement à une liste classique, elle n’a pas de véritable "fin" : on peut la parcourir indéfiniment en suivant les pointeurs `next`.

### Caractéristiques :
- **Cycle fermé** : Le pointeur de la dernière cellule ne pointe pas vers `NULL`, mais vers la première cellule.
- **Accès en boucle** : Permet un parcours cyclique de la liste.
- **Représentation** : On stocke souvent un pointeur vers la **dernière cellule** (`tail`), ce qui rend certaines opérations (comme l’insertion en fin) plus efficaces.

---

## 1. Afficher la liste

```c
void display(Cell c) {
    if (!c) return;

    c = c->next;
    Cell stop = c;
    do {
        printf("%d ", c->value);
        c = c->next;
    } while (c != stop);

    printf("\n");
}
````

* **But** : Afficher tous les éléments de la liste une seule fois.
* **Entrée** : `c` : Pointeur vers la dernière cellule (fin de la boucle).
* **Sortie** : Affichage des valeurs.
* **Complexité temporelle** : O(n)
* **Description** : On commence à `c->next` (la tête logique), et on parcourt jusqu’à revenir au point de départ (`stop`). Le `do...while` garantit que chaque cellule est visitée une fois.

---

## 2. Insertion en tête (`insertFirst`)

```c
Cell insertFirst(Cell c, int value) {
    Cell n = createCell(value);
    if (!c) {
        n->next = n;
        return n;
    }
    n->next = c->next;
    c->next = n;
    return c;
}
```

* **But** : Ajouter un élément juste après le dernier (donc en tête logique).
* **Entrée** : `c` : Cellule finale, `value` : Valeur à insérer.
* **Sortie** : Pointeur vers la cellule finale (inchangé).
* **Complexité temporelle** : O(1)
* **Description** : On insère la nouvelle cellule entre `c` et `c->next` (le début logique). Si la liste est vide, la cellule se relie à elle-même.

---

## 3. Insertion en fin (`insertLast`)

```c
Cell insertLast(Cell c, int value) {
    Cell n = createCell(value);
    if (c) {
        n->next = c->next;
        c->next = n;
        return n;
    }
    n->next = n;
    return n;
}
```

* **But** : Ajouter un élément à la fin de la liste (et le désigner comme le nouveau `tail`).
* **Entrée** : `c` : Cellule finale actuelle, `value` : Valeur à insérer.
* **Sortie** : Nouvelle cellule finale.
* **Complexité temporelle** : O(1)
* **Description** : Même principe que `insertFirst`, mais on retourne la nouvelle cellule comme fin de la liste. En cas de liste vide, la cellule se pointe elle-même.

---

## 4. Suppression du premier élément (`deleteFirst`)

```c
Cell deleteFirst(Cell c) {
    if (!c || c == c->next) return NULL;
    c->next = c->next->next;
    return c;
}
```

* **But** : Supprimer l’élément en tête logique.
* **Entrée** : `c` : Cellule finale.
* **Sortie** : Cellule finale mise à jour (inchangée sauf si un seul élément).
* **Complexité temporelle** : O(1)
* **Description** : On fait pointer `c` vers `c->next->next`, supprimant la première cellule logique. Si un seul élément existait, la liste devient vide.

---

## 5. Suppression du dernier élément (`deleteLast`)

```c
Cell deleteLast(Cell c) {
    if (!c || c->next == c) return NULL;
    Cell last = c;
    while (c->next != last) {
        c = c->next;
    }
    c->next = last->next;
    return c;
}
```

* **But** : Supprimer la cellule finale (dernière insérée).
* **Entrée** : `c` : Cellule finale actuelle.
* **Sortie** : Nouvelle cellule finale.
* **Complexité temporelle** : O(n)
* **Description** : On parcourt la liste pour trouver la cellule juste avant `last`, puis on la fait pointer vers le début. Cette cellule devient la nouvelle fin.

---

### Résumé

| Opération     | But                         | Complexité |
| ------------- | --------------------------- | ---------- |
| `display`     | Affiche tous les éléments   | O(n)       |
| `insertFirst` | Insertion en tête logique   | O(1)       |
| `insertLast`  | Insertion en fin            | O(1)       |
| `deleteFirst` | Supprime le premier élément | O(1)       |
| `deleteLast`  | Supprime le dernier élément | O(n)       |

---

Les **listes chaînées circulaires** sont particulièrement utiles pour des structures de type **file tournante**, **jeu à tour de rôle**, ou toute situation nécessitant un **parcours en boucle continue**. Elles permettent une gestion élégante du cycle sans point d'arrêt explicite.
