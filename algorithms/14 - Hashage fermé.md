# Hachage Fermé

## Description

Le **hachage fermé** est une technique où les collisions sont résolues **dans le tableau lui-même**, sans recourir à des listes chaînées. Lorsqu’une case est occupée, on applique une **sonde linéaire** (`rehash`) pour trouver la prochaine case libre.

### Caractéristiques :
- Chaque mot est stocké **directement dans le tableau**.
- En cas de collision, on cherche la prochaine case disponible (sondage linéaire).
- Le tableau est **doublé** automatiquement si la table devient trop pleine.
- Supprimer un élément peut nécessiter une **réinsertion partielle**.

---

## 1. Contient (`contains`)

```c
int contains(HashTable ht, std::string word) {
    int index = hash(word);
    int rehash = 0;
    while (ht[(index + rehash) % ht.size()] != "") {
        if (ht[(index + rehash) % ht.size()] == word) {
            return 1;
        }
        rehash++;
    }
    return 0;
}
````

* **But** : Vérifie si `word` est présent dans la table.
* **Entrée** : `ht` (table), `word` (mot à chercher).
* **Sortie** : 1 si trouvé, 0 sinon.
* **Complexité moyenne** : O(1) — **Pire cas** : O(n) si la table est presque pleine.

---

## 2. Ajouter (`add`)

```c
HashTable add(HashTable ht, std::string word) {
    int index = hash(word);
    int rehash = 0;

    while (ht[(index + rehash) % ht.size()] != "") {
        if (ht[(index + rehash) % ht.size()] == word) {
            return ht; // déjà présent
        }
        rehash++;
    }

    ht[(index + rehash) % ht.size()] = word;

    if (ht.incrementCount() >= ht.size() / 2)
        ht = doubleSize(ht); // double si la moitié est remplie

    return ht;
}
```

* **But** : Ajoute `word` s’il n’est pas déjà présent.
* **Entrée** : `ht` (table), `word` (mot).
* **Sortie** : Nouvelle table (agrandie si nécessaire).
* **Détail** :

  * On cherche une case libre avec `rehash`.
  * La table est doublée si **≥ 50 %** de remplissage.
* **Complexité** : O(1) en moyenne, O(n) si redimensionnement.

---

## 3. Redimensionnement (`doubleSize`)

```c
HashTable doubleSize(HashTable ht) {
    HashTable HT(ht.size() * 2);
    for (int i = 0; i < ht.size(); i++) {
        if (ht[i] != "")
            add(HT, ht[i]);
    }
    return HT;
}
```

* **But** : Agrandir la table en doublant sa taille.
* **Entrée** : `ht` (ancienne table).
* **Sortie** : Nouvelle table plus grande.
* **Complexité** : O(n) — **copie complète** des éléments existants.

---

## 4. Supprimer (`remove`)

```c
void remove(HashTable ht, std::string word) {
    int index = hash(word);
    int rehash = 0;
    bool removed = false;

    while (ht[(index + rehash) % ht.size()] != "") {
        if (ht[(index + rehash) % ht.size()] == word) {
            ht[(index + rehash) % ht.size()] = "";
            removed = true;
            break;
        }
        rehash++;
    }

    if (removed && ht[(index + rehash + 1) % ht.size()] != "") {
        HashTable HT(ht.size());
        for (int i = 0; i < ht.size(); i++) {
            if (ht[i] != "")
                add(HT, ht[i]);
        }
        for (int i = 0; i < ht.size(); i++) {
            ht[i] = HT[i];
        }
    }
}
```

* **But** : Supprime un mot de la table.
* **Particularité** : Si des éléments ont été placés par **collision**, ils doivent être réinsérés après suppression.
* **Complexité** : O(n) si besoin de reconstruire la table.

---

### Résumé

| Opération    | Rôle                          | Complexité moyenne | Complexité pire cas         |
| ------------ | ----------------------------- | ------------------ | --------------------------- |
| `contains`   | Vérifie si un mot est présent | O(1)               | O(n)                        |
| `add`        | Ajoute un mot si absent       | O(1)               | O(n) (si redimensionnement) |
| `remove`     | Supprime un mot               | O(1)               | O(n) (si réinsertion)       |
| `doubleSize` | Agrandit la table             | O(n)               | -                           |

---

## Avantages du hachage fermé

* Accès rapide en mémoire (tout est dans un tableau).
* Pas besoin de pointeurs ou de listes chaînées.
* Plus compact.

## Inconvénients

* Supprimer nécessite parfois de **réorganiser** les éléments.
* Les performances chutent si la table dépasse 50–70 % de remplissage.
* Une mauvaise fonction de hachage peut provoquer de longues chaînes de collisions.

---
