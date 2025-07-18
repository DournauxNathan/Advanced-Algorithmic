# Arbres Binaires – Parcours

## Description

Les **parcours d'arbres binaires** consistent à visiter tous les nœuds d'un arbre de manière systématique. On distingue plusieurs méthodes de parcours, chacune adaptée à des besoins précis :

- **Parcours en profondeur** : visite récursive ou itérative par ordre préfixé, infixé ou postfixé.
- **Parcours en largeur** : visite niveau par niveau (utilisation d'une file).
- **Parcours itératif préfixé** : utilisation d'une pile pour simuler le parcours récursif.

Les fonctions présentées ci-dessous affichent les valeurs des nœuds sur une **ligne unique**, sans saut de ligne.

---

## 1. Parcours Préfixé (Recursive)

```c
void preOrderDisplay(Node root) {
    if (!root) return;
    display(root->value);
    preOrderDisplay(root->leftChild);
    preOrderDisplay(root->rightChild);
}
````

* **But** : Visiter et afficher la racine, puis le sous-arbre gauche, ensuite le sous-arbre droit.
* **Complexité** : O(n), chaque nœud étant visité exactement une fois.
* **Utilisation** : Approprié pour copier/arborescence ou expression préfixée.

---

## 2. Parcours Infixé

```c
void inOrderDisplay(Node root) {
    if (!root) return;
    inOrderDisplay(root->leftChild);
    display(root->value);
    inOrderDisplay(root->rightChild);
}
```

* **But** : Visiter le sous-arbre gauche, afficher la racine, puis le sous-arbre droit.
* **Complexité** : O(n)
* **Utilisation** : Particulièrement utile pour afficher les éléments d'un arbre binaire de recherche dans l'ordre croissant.

---

## 3. Parcours Postfixé

```c
void postOrderDisplay(Node root) {
    if (!root) return;
    postOrderDisplay(root->leftChild);
    postOrderDisplay(root->rightChild);
    display(root->value);
}
```

* **But** : Visiter d'abord le sous-arbre gauche, ensuite le sous-arbre droit, puis afficher la racine.
* **Complexité** : O(n)
* **Utilisation** : Fréquemment utilisé pour la suppression de l'arbre ou l'évaluation des expressions arborescentes.

---

## 4. Parcours en Largeur (Breadth-First Display)

```c
void breadthFirstDisplay(Node n) {
    if (!n) return;
    Queue q;
    q.push(n);
    while (!q.isEmpty()) {
        Node cur = q.pop();
        display(cur->value);
        if (cur->leftChild)  q.push(cur->leftChild);
        if (cur->rightChild) q.push(cur->rightChild);
    }
}
```

* **But** : Affiche les nœuds niveau par niveau, de haut en bas et de gauche à droite.
* **Complexité** : O(n)
* **Utilisation** : Utile pour des applications nécessitant un traitement par niveau (exemple : algorithmes de recherche en largeur).

---

## 5. Parcours Préfixé Itératif (avec Pile)

```c
void preOrderDisplay(Node root) {
    if (!root) return;
    Stack s;
    s.push(root);
    while (!s.isEmpty()) {
        Node cur = s.pop();
        display(cur->value);
        if (cur->rightChild) s.push(cur->rightChild);
        if (cur->leftChild)  s.push(cur->leftChild);
    }
}
```

* **But** : Réalise le parcours préfixé sans récursion en utilisant une pile pour gérer les nœuds.
* **Complexité** : O(n)
* **Utilisation** : Utile pour éviter les problèmes de débordement de pile lors d'arbres très profonds.

---

### Résumé

| Parcours                   | Description                                   | Complexité |
| -------------------------- | --------------------------------------------- | ---------- |
| Préfixé (récursif)         | Racine → Sous-arbre gauche → Sous-arbre droit | O(n)       |
| Infixé                     | Sous-arbre gauche → Racine → Sous-arbre droit | O(n)       |
| Postfixé                   | Sous-arbre gauche → Sous-arbre droit → Racine | O(n)       |
| En largeur (Breadth-first) | Visite niveau par niveau                      | O(n)       |
| Préfixé itératif           | Parcours préfixé simulé avec une pile         | O(n)       |

---

Ces différents parcours offrent des approches variées pour traiter ou afficher les données contenues dans un arbre binaire, en fonction des besoins (parcours global, affichage ordonné, gestion de mémoire, etc.).
