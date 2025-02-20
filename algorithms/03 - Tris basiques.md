## Algorithmes de Tri

Cette section présente des algorithmes classiques de tri, souvent utilisés comme bases d’apprentissage en algorithmique. Ces algorithmes sont principalement utilisés pour organiser les éléments d'un tableau dans un ordre croissant ou décroissant. Ils sont fondamentaux pour comprendre les concepts de complexité algorithmique et les principes de base du tri.

### Algorithmes inclus :

1. **Tri à bulles (Bubble Sort)** : Un des algorithmes les plus simples à comprendre et à implémenter, bien qu'il soit inefficace pour de grandes quantités de données. Il fonctionne en comparant et en échangeant les éléments adjacents dans le tableau à chaque itération, jusqu'à ce que le tableau soit entièrement trié.

2. **Tri par insertion (Insertion Sort)** : Ce tri est basé sur l’idée de construire progressivement le tableau trié en insérant les éléments un par un dans leur position correcte, en déplaçant les éléments plus grands au fur et à mesure.

3. **Tri par sélection (Selection Sort)** : Cet algorithme trie le tableau en trouvant successivement le plus petit (ou plus grand) élément non trié et en le déplaçant à sa place dans le tableau. Il est plus efficace que le tri à bulles, mais toujours assez inefficace pour des tableaux de grande taille.

Ces algorithmes sont décrits avec leur implémentation en C, leur complexité temporelle, ainsi qu’une explication de leur fonctionnement pour comprendre les différences et les performances associées à chaque méthode.

---
### 1. Tri par sélection (Selection Sort)
```c
void sort(int *tab, int N)
{
    for (int i = 0; i < N - 1; i++) {
        // Trouver l'indice de la plus petite valeur dans la partie non triée
        int minIndex = i;
        for (int j = i + 1; j < N; j++) {
            if (tab[j] < tab[minIndex]) {
                minIndex = j;
            }
        }
        // Échanger la plus petite valeur trouvée avec l'élément à l'indice actuel
        swap(&tab[i], &tab[minIndex]);
    }
}
```
- **But de l'algorithme** : Trier les éléments d'un tableau en trouvant successivement le minimum dans la partie non triée et en l'échangeant avec l'élément à sa place.
- **Entrée** :
  - `tab` : Tableau d'entiers à trier.
  - `N` : Taille du tableau.
- **Sortie** : Le tableau `tab` est trié en ordre croissant.
- **Complexité temporelle** : O(n²), où n est la taille du tableau.
- **Description** : L'algorithme parcourt le tableau, cherche le plus petit élément dans la partie non triée, puis échange cet élément avec l'élément à la position actuelle. Cela répète l'opération jusqu'à ce que le tableau soit trié.

---

### 2. Tri à bulles (Bubble Sort)
```c
void sort(int *tab, int N)
{
    for (int i = 0; i < N - 1; i++) {
        int swapped = 0;
        for (int j = 0; j < N - 1 - i; j++) {
            if (tab[j] > tab[j + 1]) {
                swap(&tab[j], &tab[j + 1]);
                swapped = 1;
            }
        }
        if (!swapped) {
            break;
        }
    }
}
```
- **But de l'algorithme** : Trier un tableau en comparant et échangeant des éléments adjacents.
- **Entrée** :
  - `tab` : Tableau d'entiers à trier.
  - `N` : Taille du tableau.
- **Sortie** : Le tableau `tab` est trié en ordre croissant.
- **Complexité temporelle** : O(n²) dans le pire des cas, mais peut être plus rapide si le tableau est déjà partiellement trié (O(n) dans le meilleur des cas).
- **Description** : L'algorithme compare les éléments adjacents dans le tableau et les échange si nécessaire, répétant cette opération jusqu'à ce que le tableau soit trié. Un indicateur `swapped` est utilisé pour vérifier si des échanges ont été effectués, permettant ainsi de stopper l'algorithme plus tôt si le tableau est déjà trié.

---

### 3. Tri par insertion (Insertion Sort)
```c
void sort(int *tab, int N)
{
    for (int i = 1; i < N; i++)
    {
        int val = tab[i];
        int pos = i;
        
        while (pos > 0 && tab[pos - 1] > val)
        {
            pos--;
        }
        
        insert(tab, i , pos, val);
    }
}
```
- **But de l'algorithme** : Trier un tableau en insérant les éléments un à un dans leur position correcte.
- **Entrée** :
  - `tab` : Tableau d'entiers à trier.
  - `N` : Taille du tableau.
- **Sortie** : Le tableau `tab` est trié en ordre croissant.
- **Complexité temporelle** : O(n²) dans le pire des cas, mais O(n) si le tableau est déjà trié.
- **Description** : L'algorithme construit progressivement une sous-liste triée. À chaque itération, il insère l'élément à sa position correcte dans cette sous-liste, en déplaçant les éléments plus grands.

---

### 4. Tri pair-impair (Odd-Even Sort)
```c
void oddEvenSort(int* tab, int size)
{
    int sorted = 0;
    
    while (sorted == 0)
    {
        sorted = 1;

        for (int i = 0; i < size - 1; i += 2)
        {
            if (tab[i] > tab[i + 1])
            {
                swap(&tab[i], &tab[i + 1]);
                sorted = 0;
            }
        }

        for (int i = 1; i < size - 1; i += 2)
        {
            if (tab[i] > tab[i + 1])
            {
                swap(&tab[i], &tab[i + 1]);
                sorted = 0;
            }
        }
    }
}
```
- **But de l'algorithme** : Trier un tableau en utilisant une approche basée sur les échanges entre éléments pairs et impairs.
- **Entrée** :
  - `tab` : Tableau d'entiers à trier.
  - `size` : Taille du tableau.
- **Sortie** : Le tableau `tab` est trié en ordre croissant.
- **Complexité temporelle** : O(n²) dans le pire des cas.
- **Description** : L'algorithme effectue des comparaisons et des échanges entre éléments pairs et impairs du tableau jusqu'à ce que le tableau soit trié.

---

### 5. Tri à peigne (Comb Sort)
```c
void combSort(int* tab, int size)
{
    int gap = size;
    int sorted = 0;
    
    while (gap > 1 || sorted == 0)
    {
        gap = (int)(gap / 1.3);
        
        if (gap < 1)
        {
            gap = 1;
        }
        sorted = 1;
    
        for (int i = 0; i + gap < size; i++)
        {
            if (tab[i] > tab[i + gap])
            {
                swap(&tab[i], &tab[i + gap]);
                sorted = 0;
            }
        }
    }
}
```
- **But de l'algorithme** : Trier un tableau en utilisant un "gap" (écart) qui diminue progressivement, permettant d'effectuer des comparaisons sur des éléments distants et de rapprocher les éléments à leur position correcte.
- **Entrée** :
  - `tab` : Tableau d'entiers à trier.
  - `size` : Taille du tableau.
- **Sortie** : Le tableau `tab` est trié en ordre croissant.
- **Complexité temporelle** : O(n²) dans le pire des cas, mais beaucoup plus rapide que le tri à bulles pour des tableaux de grande taille.
- **Description** : Le tri à peigne est une amélioration du tri à bulles. Il utilise un écart qui diminue au fur et à mesure des itérations, permettant de comparer des éléments plus éloignés et d'éviter de revenir sur des éléments déjà triés.

---

### 6. Tri cocktail (Cocktail Sort)
```c
void cocktailSort(int* tab, int size)
{
    int swapped = 1;
    
    while (swapped == 1)
    {
        swapped = 0;
        
        for (int i = 0; i < size - 2; i++)
        {
            if (tab[i] > tab[i + 1])
            {
                swap(&tab[i], &tab[i + 1]);
                swapped = 1;
            }
        }
        
        for (int i = size - 2; i > 0; i--)
        {
            if (tab[i] > tab[i + 1])
            {
                swap(&tab[i], &tab[i + 1]);
                swapped = 1;
            }
        }
    }
}
```
- **But de l'algorithme** : Trier un tableau en effectuant des passes bidirectionnelles (de gauche à droite et de droite à gauche).
- **Entrée** :
  - `tab` : Tableau d'entiers à trier.
  - `size` : Taille du tableau.
- **Sortie** : Le tableau `tab` est trié en ordre croissant.
- **Complexité temporelle** : O(n²) dans le pire des cas.
- **Description** : Le tri cocktail est une variante du tri à bulles. Il effectue des passes dans les deux directions : d'abord de gauche à droite, puis de droite à gauche, jusqu'à ce que le tableau soit trié.

```
