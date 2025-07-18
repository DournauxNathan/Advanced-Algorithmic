# Arbres AVL

## Définition

Un **arbre AVL** (Adelson-Velsky & Landis) est un arbre binaire de recherche **auto-équilibré** dans lequel la **hauteur des sous-arbres gauche et droit** de chaque nœud diffère d’au plus 1.

> Cette propriété garantit une hauteur logarithmique, assurant une complexité moyenne **O(log n)** pour les opérations de recherche, insertion et suppression.

---

## 1. Mise à jour de la hauteur (`updateHeight`)

```c
void updateHeight(Node n){
    if(!n) return;
    n->height = 0;
    if(n->leftChild && n->leftChild->height + 1 > n->height)
        n->height = n->leftChild->height + 1;
    if(n->rightChild && n->rightChild->height + 1 > n->height)
        n->height = n->rightChild->height + 1;
}
````

* **But** : Recalcule la hauteur d’un nœud en fonction de ses enfants.
* **Hauteur d’un nœud** : `1 + max(hauteur_gauche, hauteur_droite)`

---

## 2. Rotations

### a. Rotation gauche (`leftRotate`)

```c
Node leftRotate(Node root){
    if(!root || !root->rightChild) return root;

    Node newRoot = root->rightChild;
    root->rightChild = newRoot->leftChild;
    newRoot->leftChild = root;

    updateHeight(root);
    updateHeight(newRoot);

    return newRoot;
}
```

* **But** : Rotation pour corriger un déséquilibre **droite-droite**.
* **Effet** : Le sous-arbre droit devient racine, l’ancienne racine passe à gauche.

---

### b. Rotation droite (`rightRotate`)

```c
Node rightRotate(Node root){
    if(!root || !root->leftChild) return root;

    Node newRoot = root->leftChild;
    root->leftChild = newRoot->rightChild;
    newRoot->rightChild = root;

    updateHeight(root);
    updateHeight(newRoot);

    return newRoot;
}
```

* **But** : Rotation pour corriger un déséquilibre **gauche-gauche**.
* **Effet** : Le sous-arbre gauche devient racine.

---

## 3. Équilibrage (`balance`)

```c
int getBalance(Node n){
    int lh = -1, rh = -1;
    if(n->leftChild) lh = n->leftChild->height;
    if(n->rightChild) rh = n->rightChild->height;
    return rh - lh;
}

Node balance(Node root){
    if(!root) return root;

    int balance = getBalance(root);

    if(balance < -1){ // Déséquilibre à gauche
        if(getBalance(root->leftChild) > 0)
            root->leftChild = leftRotate(root->leftChild);
        return rightRotate(root);
    }

    if(balance > 1){ // Déséquilibre à droite
        if(getBalance(root->rightChild) < 0)
            root->rightChild = rightRotate(root->rightChild);
        return leftRotate(root);
    }

    return root;
}
```

* **But** : Applique les bonnes rotations selon le déséquilibre.
* **Cas couverts** :

  * Gauche-Gauche ➝ Rotation droite
  * Gauche-Droite ➝ Rotation gauche puis droite
  * Droite-Droite ➝ Rotation gauche
  * Droite-Gauche ➝ Rotation droite puis gauche

---

## 4. Insertion (`insert`)

```c
Node insert(Node root, int value){
    if(!root) return createNode(value);
    if(value < root->value)
        root->leftChild = insert(root->leftChild, value);
    else
        root->rightChild = insert(root->rightChild, value);

    updateHeight(root);
    return balance(root);
}
```

* **But** : Insertion classique d’un ABR, suivie d’un rééquilibrage.
* **Complexité** : O(log n)

---

## 5. Suppression (`remove`)

```c
Node remove(Node root, int value){
    if(!root) return root;

    if(value < root->value){
        root->leftChild = remove(root->leftChild, value);
    } else if(value > root->value){
        root->rightChild = remove(root->rightChild, value);
    } else {
        if(!root->leftChild && !root->rightChild){
            Node empty;
            return empty;
        }
        if(!root->leftChild) return root->rightChild;
        if(!root->rightChild) return root->leftChild;

        Node max = getMaxNode(root->leftChild);
        root->value = max->value;
        max->value = value;
        root->leftChild = remove(root->leftChild, value);
    }

    updateHeight(root);
    return balance(root);
}
```

* **But** : Suppression classique dans un ABR avec équilibrage.
* **Remarques** :

  * La suppression d’un nœud à deux enfants remplace la valeur par celle du maximum gauche.
  * Nécessite mise à jour de la hauteur et équilibrage.
* **Complexité** : O(log n)

---

## Résumé des opérations AVL

| Opération       | Fonction      | Complexité |
| --------------- | ------------- | ---------- |
| Insertion       | `insert`      | O(log n)   |
| Suppression     | `remove`      | O(log n)   |
| Rotation gauche | `leftRotate`  | O(1)       |
| Rotation droite | `rightRotate` | O(1)       |
| Équilibrage     | `balance`     | O(1)       |

---

## Schéma visuel : Rotation droite

Avant :

```
      5
     /
    3
   /
  2
```

Après `rightRotate(5)` :

```
      3
     / \
    2   5
```

---

## AVL vs ABR classique

| Propriété           | ABR classique | AVL                                              |
| ------------------- | ------------- | ------------------------------------------------ |
| Équilibrage garanti | ❌ Non         | ✅ Oui                                            |
| Complexité max      | O(n)          | O(log n)                                         |
| Complexité moyenne  | O(log n)      | O(log n)                                         |
| Vitesse insertion   | ✅ Rapide      | ⛔ Légèrement plus lente                          |
| Cas d’usage         | Simple        | Performant si nombreuses insertions/suppressions |

---

## Notes

* Une hauteur de `-1` peut être utilisée pour les feuilles inexistantes (null).
* L’AVL est une bonne alternative au `std::set` ou `std::map` en C si l’on souhaite maîtriser soi-même la structure.
