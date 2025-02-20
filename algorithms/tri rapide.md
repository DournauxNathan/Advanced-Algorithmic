## Tri Rapide (Quick Sort)

Le tri rapide est un algorithme de tri diviser pour régner, qui utilise un pivot pour partitionner le tableau en deux sous-tableaux, et trie ensuite récursivement chaque sous-tableau.

### 1. Partition par Pivot
```c
int partition(Array tab, int pivot)
{
    int pivotValue = tab[pivot];
    int N = tab.size();

    // 2. Mettre le Pivot à la fin
    tab.swap(N-1, pivot);

    // Init posFinale à 0
    int posFinale = 0;

    // 3. Pour i allant de 0 à N-1
    for (int i = 0; i < N - 1; i++) 
    {
        // Si val(i) < pivot
        if (tab[i] < pivotValue)
        {
            // Échanger val(i) et posFinale
            tab.swap(posFinale, i);
            posFinale++;
        }
    }

    // 4. On échange le dernier élément et posFinale
    tab.swap(posFinale, N-1);

    return posFinale;
}
```
- **But de l'algorithme** : Partitionner un tableau autour d'un pivot de manière à ce que tous les éléments inférieurs au pivot se trouvent avant lui, et tous les éléments supérieurs se trouvent après lui.
- **Entrée** :
  - `tab` : Tableau d'éléments à partitionner.
  - `pivot` : L'indice de l'élément pivot choisi.
- **Sortie** : La nouvelle position du pivot après la partition.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : La fonction `partition` déplace d'abord le pivot à la fin du tableau, puis parcourt le tableau en échangeant les éléments qui sont plus petits que le pivot avec ceux qui sont plus grands. Enfin, elle place le pivot à sa position correcte dans le tableau et retourne cette position.

---

### 2. Tri Rapide
```c
void quickSort(Array tab)
{
    if (tab.size() <= 1) return;

    int choice = pivotChoice(tab);
    int pivot = partition(tab, choice);

    if (pivot > 0) 
    {
        quickSort(tab.subArray(0, pivot)); 
    }
    if (pivot + 1 < tab.size()) 
    {
        quickSort(tab.subArray(pivot + 1, tab.size())); 
    }
}
```
- **But de l'algorithme** : Trier un tableau en utilisant l'algorithme du tri rapide (Quick Sort).
- **Entrée** :
  - `tab` : Tableau d'éléments à trier.
- **Sortie** : Un tableau trié.
- **Complexité temporelle** : O(n log n) en moyenne, mais O(n²) dans le pire des cas.
- **Description** : L'algorithme de tri rapide choisit un pivot et partitionne le tableau autour de celui-ci. Ensuite, il trie récursivement les sous-tableaux avant et après le pivot. Le choix du pivot peut être fait de différentes manières, par exemple en choisissant le premier élément, le dernier élément, ou un pivot aléatoire.
