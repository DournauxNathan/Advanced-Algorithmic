## Tri Fusion (Merge Sort)

Le tri fusion est un algorithme de tri basé sur le principe "diviser pour régner". Il divise le tableau en sous-tableaux plus petits, trie ces sous-tableaux, puis fusionne les sous-tableaux triés pour obtenir le tableau final trié.

### 1. Algorithme de Tri Fusion
```c
Array mergeSort(Array tab)
{
    if (tab.size() <= 1)
    {
        return tab;
    }

    int mid = tab.size() / 2;

    Array left(mid); 
    Array right(tab.size() - mid);

    for (int i = 0; i < mid; i++) {
        left[i] = tab[i];
    }

    for (int i = mid; i < tab.size(); i++) {
        right[i - mid] = tab[i];
    }

    Array sortedLeft = mergeSort(left);
    Array sortedRight = mergeSort(right);

    return merge(sortedLeft, sortedRight);
}
```
- **But de l'algorithme** : Trier un tableau en divisant le tableau en deux moitiés, en triant récursivement chaque moitié, puis en fusionnant les résultats triés.
- **Entrée** :
  - `tab` : Tableau d'éléments à trier.
- **Sortie** : Un tableau trié dans l'ordre croissant.
- **Complexité temporelle** : O(n log n), où n est la taille du tableau. C'est un des algorithmes les plus efficaces pour trier de grands ensembles de données.
- **Description** : L'algorithme divise le tableau en deux sous-tableaux de taille à peu près égale, trie récursivement chaque sous-tableau et fusionne les sous-tableaux triés pour obtenir un tableau final trié.

---

### 2. Fusion de Tableaux Triés
```c
Array merge(Array a, Array b)
{
    int N = a.size() + b.size(); 
    Array newTab(N); 

    int i = 0, j = 0, k = 0; 

    for (; i < a.size() && j < b.size(); k++)
    {
        if (a[i] < b[j])
        {
            newTab[k] = a[i++];
        } 
        else 
        {
            newTab[k] = b[j++];
        }
    }

    for (; i < a.size(); i++, k++)
    {
        newTab[k] = a[i];
    }

    // Copier les éléments restants de b, s'il y en a
    for (; j < b.size(); j++, k++)
    {
        newTab[k] = b[j];
    }

    newTab.debug();
    
    return newTab;
}
```
- **But de l'algorithme** : Fusionner deux tableaux triés en un seul tableau trié.
- **Entrée** :
  - `a` : Premier tableau trié.
  - `b` : Deuxième tableau trié.
- **Sortie** : Un tableau trié fusionné à partir des deux tableaux d'entrée.
- **Complexité temporelle** : O(n), où n est la somme des tailles des deux tableaux `a` et `b`.
- **Description** : Cette fonction fusionne deux sous-tableaux triés (`a` et `b`) en un seul tableau trié. Elle parcourt les deux tableaux simultanément et place les éléments dans le bon ordre dans le nouveau tableau `newTab`. Si l'un des tableaux est encore partiellement traversé après la fusion des éléments communs, les éléments restants sont copiés directement dans `newTab`.
