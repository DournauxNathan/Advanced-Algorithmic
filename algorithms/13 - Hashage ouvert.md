# Hachage Ouvert

## Description

Le **hachage ouvert** est une méthode d’implémentation d’une **table de hachage** où les collisions sont gérées à l’aide de **listes chaînées**. Chaque case de la table contient une **liste de mots (ou valeurs)** partageant le même indice de hachage.

### Caractéristiques :
- Chaque case (`ht[i]`) de la table pointe vers une **liste chaînée de mots**.
- Le **hachage** transforme une chaîne de caractères en un entier (indice).
- Si plusieurs mots ont le même indice, ils sont stockés dans la même liste (collision).
- Très efficace pour les structures comme les **dictionnaires**, **ensembles**, ou les bases de données simples.

### Structure :
```c
typedef struct Cellule {
    std::string value;
    struct Cellule* next;
} *Cell;

typedef Cell* HashTable; // Tableau de listes
````

---

## 1. Fonction de hachage

```c
int hash(char* str) {
    int sum = 0;
    int cpt = 1;
    while (*str) {
        sum += *(str++) * cpt * (++cpt);
    }
    return sum;
}
```

* **But** : Transformer une chaîne de caractères en un entier unique.
* **Entrée** : `str` : Chaîne de caractères.
* **Sortie** : Valeur entière (non bornée).
* **Complexité temporelle** : O(n), où `n` est la longueur de la chaîne.
* **Description** : La fonction effectue une sommation pondérée des caractères avec un multiplicateur croissant (`cpt`). Elle sert à distribuer les mots dans la table.

---

## 2. Vérifier si un mot est présent (`contains`)

```c
int contains(HashTable ht, std::string word) {
    int index = hash(word) % ht.size();
    Cell c = ht[index];
    while (c) {
        if (c->value == word) return 1;
        c = c->next;
    }
    return 0;
}
```

* **But** : Vérifier si un mot existe dans la table.
* **Entrée** : `ht` : Table de hachage, `word` : Mot à chercher.
* **Sortie** : 1 si le mot est trouvé, 0 sinon.
* **Complexité temporelle** : O(n) dans le pire cas (collisions), O(1) en moyenne.
* **Description** : On calcule l’indice via `hash % taille`, puis on parcourt la liste associée à cet indice pour chercher le mot.

---

## 3. Ajouter un mot (`add`)

```c
void add(HashTable ht, std::string word) {
    int index = hash(word) % ht.size();
    Cell cur = ht[index];
    while (cur) {
        if (cur->value == word) return;
        cur = cur->next;
    }

    Cell c = createCell(word);
    c->next = ht[index];
    ht[index] = c;
}
```

* **But** : Ajouter un mot à la table s’il n’est pas déjà présent.
* **Entrée** : `ht` : Table de hachage, `word` : Mot à insérer.
* **Sortie** : Aucune.
* **Complexité temporelle** : O(n) en cas de collisions, O(1) en moyenne.
* **Description** : On vérifie d’abord si le mot est déjà présent. Si ce n’est pas le cas, on l’insère en tête de la liste associée à l’indice.

---

## 4. Supprimer un mot (`remove`)

```c
void remove(HashTable ht, std::string word) {
    int index = hash(word) % ht.size();
    Cell c = ht[index];

    if (!c) return;

    if (c->value == word) {
        ht[index] = c->next;
        return;
    }

    while (c->next) {
        if (c->next->value == word) {
            c->next = c->next->next;
            return;
        }
        c = c->next;
    }
}
```

* **But** : Supprimer un mot s’il est présent dans la table.
* **Entrée** : `ht` : Table de hachage, `word` : Mot à supprimer.
* **Sortie** : Aucune.
* **Complexité temporelle** : O(n) dans la liste chaînée, O(1) en moyenne.
* **Description** : Si le mot est en tête, on met à jour l’indice directement. Sinon, on parcourt la liste et on ajuste les pointeurs pour supprimer la cellule correspondante.

---

### Résumé

| Opération  | But                              | Complexité moyenne | Complexité pire cas |
| ---------- | -------------------------------- | ------------------ | ------------------- |
| `hash`     | Génère un indice pour une chaîne | O(n)               | O(n)                |
| `contains` | Vérifie si un mot est présent    | O(1)               | O(n)                |
| `add`      | Ajoute un mot si absent          | O(1)               | O(n)                |
| `remove`   | Supprime un mot                  | O(1)               | O(n)                |

---

Le **hachage ouvert** est une stratégie de gestion des collisions simple, efficace, et très utilisée dans les **maps**, **sets**, ou les dictionnaires de langage naturel. Son efficacité dépend fortement de la **fonction de hachage** et de la **taille de la table**.
