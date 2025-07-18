# Arbres Binaires de Recherche (ABR)

## Description

Un **arbre binaire de recherche (ABR)** est un arbre binaire structuré de telle sorte que pour chaque nœud :
- Tous les éléments du **sous-arbre gauche** ont une valeur **strictement inférieure** au nœud courant.
- Tous les éléments du **sous-arbre droit** ont une valeur **supérieure ou égale** au nœud courant.

Cette structure permet une recherche efficace en **O(log n)** en moyenne (si l'arbre est équilibré).

---

## 1. Recherche d’un élément (`contains`)

```c
int contains(Node root, int value) {
    if (!root) return 0;
    if (root->value == value) return 1;
    if (root->value > value)
        return contains(root->leftChild, value);
    return contains(root->rightChild, value);
}
````

* **But** : Vérifie si une valeur est présente dans l’arbre.
* **Complexité** :

  * Meilleur cas (équilibré) : O(log n)
  * Pire cas (arbre dégénéré) : O(n)

---

## 2. Insertion d’un élément (`insert`)

```c
Node insert(Node root, int value) {
    if (!root) return createNode(value);
    if (root->value > value)
        root->leftChild = insert(root->leftChild, value);
    else
        root->rightChild = insert(root->rightChild, value);
    return root;
}
```

* **But** : Insère un élément à sa position correcte pour maintenir la propriété d’un ABR.
* **Remarque** : L’insertion accepte les doublons dans le sous-arbre droit.
* **Complexité** :

  * Moyenne : O(log n)
  * Pire cas : O(n)

---

## 3. Recherche du maximum (`getMaxNode`)

```c
Node getMaxNode(Node root) {
    if (!root) return root;
    if (!root->rightChild) return root;
    return getMaxNode(root->rightChild);
}
```

* **But** : Renvoie le nœud ayant la valeur maximale d’un arbre (toujours le plus à droite).
* **Utilité** : Requis pour la suppression de nœuds avec deux enfants.
* **Complexité** : O(h), où h est la hauteur de l’arbre.

---

## 4. Suppression d’un élément (`remove`)

```c
Node remove(Node root, int value) {
    if (!root) return root;

    if (root->value > value) {
        root->leftChild = remove(root->leftChild, value);
        return root;
    }
    if (root->value < value) {
        root->rightChild = remove(root->rightChild, value);
        return root;
    }

    // Cas 1 : Feuille
    if (!root->leftChild && !root->rightChild) {
        Node empty;
        return empty;
    }

    // Cas 2 : Un seul enfant
    if (!root->leftChild) return root->rightChild;
    if (!root->rightChild) return root->leftChild;

    // Cas 3 : Deux enfants
    Node max = getMaxNode(root->leftChild);
    root->value = max->value;
    max->value = value;
    root->leftChild = remove(root->leftChild, value);
    return root;
}
```

* **But** : Supprime un nœud tout en maintenant la structure de l’ABR.

* **Cas traités** :

  * Feuille (aucun enfant)
  * Nœud avec un seul enfant
  * Nœud avec deux enfants (remplacé par le maximum du sous-arbre gauche)

* **Complexité** : O(h)

* **⚠️ Remarque importante** :
  Le remplacement `max->value = value;` est une astuce pour réutiliser la fonction `remove`, mais peut être trompeur. Une alternative plus claire serait de supprimer `max` directement après copie de sa valeur dans `root`.

---

## Résumé des Opérations sur un ABR

| Opération      | Fonction     | Complexité Moy. | Complexité Pire Cas |
| -------------- | ------------ | --------------- | ------------------- |
| Recherche      | `contains`   | O(log n)        | O(n)                |
| Insertion      | `insert`     | O(log n)        | O(n)                |
| Suppression    | `remove`     | O(log n)        | O(n)                |
| Max d’un arbre | `getMaxNode` | O(h)            | O(n)                |

---

## Visualisation (exemple)

```
           8
         /   \
        3     12
       / \    /
      1   6  10
```

Après `insert(7)` :

```
           8
         /   \
        3     12
       / \    /
      1   6  10
           \
            7
```

---

Ce module est fondamental pour l’implémentation de structures plus avancées comme les arbres AVL, les arbres rouges-noirs, ou encore les ensembles dynamiques en C++.

```
