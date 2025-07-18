# Arbres Binaires – Fonctions Utiles

## 1. Taille de l’arbre (`treeSize`)

```c
int treeSize(Node root){
    if(!root) return 0;
    return treeSize(root->leftChild) + treeSize(root->rightChild) + 1;
}
````

* **But** : Retourne le **nombre total de nœuds**.
* **Complexité** : O(n) — chaque nœud est visité une fois.

---

## 2. Hauteur de l’arbre (`treeHeight`)

```c
int treeHeight(Node n){
    if(!n) return 0;
    if(!n->leftChild && !n->rightChild) return 0;
    int lheight = treeHeight(n->leftChild);
    int rheight = treeHeight(n->rightChild);
    return (lheight > rheight ? lheight : rheight) + 1;
}
```

* **But** : Calcule la **hauteur** de l’arbre (= profondeur maximale).
* **Convention** : Hauteur d’un nœud feuille = 0.
* **Complexité** : O(n)

---

## 3. Compter les feuilles (`leafsCount`)

```c
int leafsCount(Node root){
    if(!root) return 0;
    if(!root->leftChild && !root->rightChild) return 1;
    return leafsCount(root->leftChild) + leafsCount(root->rightChild);
}
```

* **But** : Retourne le **nombre de feuilles** (nœuds sans enfants).
* **Complexité** : O(n)

---

## 4. Arbre plein (`isFull`)

```c
int isFull(Node n){
    if(!n) return 1;
    if((!n->leftChild && n->rightChild) || (n->leftChild && !n->rightChild))
        return 0;
    return isFull(n->leftChild) & isFull(n->rightChild);
}
```

* **But** : Vérifie si l’arbre est **plein** : chaque nœud a 0 ou 2 enfants.
* **Retourne** : 1 si vrai, 0 sinon.
* **Complexité** : O(n)

---

## 5. Inverser l’arbre (`reverseTree`)

```c
Node reverseTree(Node root){
    if(!root) return root;
    Node tmp = reverseTree(root->leftChild);
    root->leftChild = reverseTree(root->rightChild);
    root->rightChild = tmp;
    return root;
}
```

* **But** : Inverse l’arbre gauche ↔ droit **récursivement**.
* **Complexité** : O(n)

---

### 🌱 Résumé des fonctions

| Fonction      | Description              | Complexité |
| ------------- | ------------------------ | ---------- |
| `treeSize`    | Nombre total de nœuds    | O(n)       |
| `treeHeight`  | Profondeur max           | O(n)       |
| `leafsCount`  | Nombre de feuilles       | O(n)       |
| `isFull`      | Arbre plein ?            | O(n)       |
| `reverseTree` | Inversion gauche ↔ droit | O(n)       |

---

## 💡 Définitions Rappels

* **Hauteur d’un arbre** : Longueur du plus long chemin entre la racine et une feuille.
* **Arbre plein (full)** : Chaque nœud a soit **0 soit 2** enfants.
* **Arbre complet** : Tous les niveaux sauf le dernier sont pleins, et les feuilles sont le plus à gauche possible.
* **Arbre parfait** : Plein et toutes les feuilles au même niveau.

---
