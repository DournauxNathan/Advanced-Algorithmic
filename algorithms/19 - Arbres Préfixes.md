# Arbres Préfixes (Trie)

## Définition

Un **arbre préfixe** (ou **Trie**) est une structure arborescente utilisée pour représenter efficacement un ensemble de **chaînes de caractères**.  
Chaque **nœud** représente un caractère, et un chemin de la racine à une **feuille** représente un mot.

> Les nœuds sans `firstChild` sont considérés comme **terminaisons de mots** (feuilles).

---

## Structure de base

Chaque `Node` possède :
- `value` : un caractère (par ex. 'a', 'b', etc.)
- `firstChild` : pointeur vers le premier enfant (prochaine lettre du mot)
- `rightSibling` : pointeur vers le frère suivant (lettre alternative au même niveau)

---

## 1. Taille de l’arbre (`treeSize`)

```c
int treeSize(Node root) {
    if (!root) return 0;

    int size = 1; // On compte le nœud courant
    size += treeSize(root->firstChild);
    size += treeSize(root->rightSibling);

    return size;
}
````

* **But** : Calcule le nombre total de nœuds dans l’arbre.
* **Complexité** : O(n), où n = nombre total de nœuds.

---

## 2. Affichage des mots (`display`)

```c
void displayHelper(Node node, char* prefix, int depth) {
    if (!node) return;

    prefix[depth] = node->value;
    prefix[depth + 1] = '\0';

    if (!node->firstChild) {
        print(prefix);  // mot complet
    } else {
        displayHelper(node->firstChild, prefix, depth + 1);
    }

    displayHelper(node->rightSibling, prefix, depth);
}

void display(Node root) {
    char prefix[100];
    displayHelper(root, prefix, 0);
}
```

* **But** : Affiche tous les mots stockés dans l’arbre.
* **Préfixe** : Chaîne construite progressivement (caractère par caractère).
* **Complexité** : O(m × k) où `m` = mots, `k` = longueur moyenne.

---

## 3. Compter le nombre de mots (`wordCount`)

```c
int wordCount(Node root) {
    if (!root) return 0;

    int count = 0;

    if (!root->firstChild) {
        count = 1; // feuille = fin de mot
    } else {
        count = wordCount(root->firstChild);
    }

    count += wordCount(root->rightSibling);
    return count;
}
```

* **But** : Compte les mots complets dans le Trie.
* **Complexité** : O(n)

---

## 4. Recherche d’un mot (`contains`)

```c
bool contains(Node root, std::string word) {
    if (!root || word.empty()) return false;

    Node current = root;

    while (current && current->value != word[0]) {
        current = current->rightSibling;
    }

    if (!current) return false;

    if (word.size() == 1) {
        return (current->firstChild == nullptr); // fin de mot
    } else {
        return contains(current->firstChild, word.substr(1));
    }
}
```

* **But** : Vérifie si un mot est présent dans le Trie.
* **Complexité** : O(k × d), `k` = taille du mot, `d` = nombre de frères max à chaque niveau.
* **Remarque** : Fonctionnelle uniquement si les mots finissent par une **feuille**.

---

## 5. Insertion d’un mot (`insert`)

```c
Node insert(Node root, string word) {
    if (word.size() == 0) {
        Node current = root;
        Node prev = NULL;
        while (current && current->value < '\0') {
            prev = current;
            current = current->rightSibling;
        }
        if (!current || current->value != '\0') {
            Node endNode = createNode('\0');
            if (!prev) {
                endNode->rightSibling = root;
                root = endNode;
            } else {
                endNode->rightSibling = current;
                prev->rightSibling = endNode;
            }
        }
        return root;
    }

    char c = word[0];
    Node current = root;
    Node prev = NULL;

    while (current && current->value < c) {
        prev = current;
        current = current->rightSibling;
    }

    if (current && current->value == c) {
        string suffix = word.substr(1);
        current->firstChild = insert(current->firstChild, suffix);
    } else {
        Node newNode = createNode(c);
        string suffix = word.substr(1);
        newNode->firstChild = insert(newNode->firstChild, suffix);
        if (!prev) {
            newNode->rightSibling = root;
            root = newNode;
        } else {
            newNode->rightSibling = current;
            prev->rightSibling = newNode;
        }
    }
    return root;
}
```

* **But** : Insère un mot caractère par caractère, en ordre croissant de lettres à chaque niveau.
* **Fin de mot** : représentée par un nœud `'\0'`
* **Complexité** : O(k × d), `k` = taille du mot, `d` = insertion triée parmi les frères.

---

## Schéma visuel

Insertion de "chat", "chien", "choix"

```
         c
         |
         h ————————
         |            \
         a             i
         |             |
         t (\0)       e — x
                       |    \
                      n     \0
                      |
                     \0
```

---

## Résumé des opérations Trie

| Opération    | Fonction    | Complexité |
| ------------ | ----------- | ---------- |
| Taille arbre | `treeSize`  | O(n)       |
| Affichage    | `display`   | O(m × k)   |
| Insertion    | `insert`    | O(k × d)   |
| Contient mot | `contains`  | O(k × d)   |
| Compter mots | `wordCount` | O(n)       |

---

## Remarques

* **Trie vs AVL / HashMap** :

  * Trie est optimal pour :

    * Rechercher des mots par **préfixe**
    * **Autocomplétion** rapide
    * Stocker un grand dictionnaire sans redondance
  * Moins performant si :

    * L'alphabet est très grand
    * Les mots sont très courts ou peu nombreux

---
