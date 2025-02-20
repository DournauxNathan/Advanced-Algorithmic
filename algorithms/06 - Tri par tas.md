## Tri par Tas (Heap Sort)

Le tri par tas est un algorithme basé sur la structure de données appelée tas (heap), qui est un arbre binaire complet avec la propriété que chaque parent est plus grand que ses enfants (pour un tas max).

### 1. Vérification des Tas
```c
int isHeap(Array tab)
{
    int n = tab.size();
    
    for (int i = 0; i < n / 2; i++)
    {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        
        if (left < n && tab[i] < tab[left]) 
        {
            return 0;
        }
        
        if (right < n && tab[i] < tab[right]) 
        {
            return 0;
        }
    }
    
    return 1;
}
```
- **But de l'algorithme** : Vérifier si un tableau représente un tas valide.
- **Entrée** :
  - `tab` : Tableau à vérifier.
- **Sortie** : `1` si le tableau est un tas valide, sinon `0`.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : Cette fonction vérifie si le tableau respecte la propriété du tas en s'assurant que chaque parent est plus grand que ses enfants. Elle parcourt les éléments jusqu'à la moitié du tableau (car les éléments après la moitié sont les feuilles du tas).

---

### 2. Insertion dans un Tas
```c
void insertHeap(Array tab)
{
    int i = tab.size() - 1;
    int parent = (i - 1) / 2;

    while (i > 0 && tab[parent] < tab[i])
    {
        tab.swap(i, parent);

        i = parent;
        parent = (i - 1) / 2;
    }
}
```
- **But de l'algorithme** : Insérer un élément dans un tas en respectant la propriété du tas max.
- **Entrée** :
  - `tab` : Tableau représentant un tas sur lequel on insère un nouvel élément.
- **Sortie** : Le tableau après insertion.
- **Complexité temporelle** : O(log n), où n est la taille du tableau.
- **Description** : Cette fonction insère un nouvel élément à la fin du tableau, puis remonte cet élément dans le tas pour rétablir la propriété du tas max. Elle compare l'élément inséré à son parent et échange si nécessaire, répétant l'opération jusqu'à ce que la propriété du tas soit respectée.

---

### 3. Supprimer la Racine d'un Tas
```c
void removeRootHeap(Array tab)
{
    int n = tab.size();

    if (n <= 1) return;

    tab.swap(0, n - 1);
    n--;

    int i = 0;
    while (true)
    {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        int largest = i;

        if (left < n && tab[left] > tab[largest]) {
            largest = left;
        }

        if (right < n && tab[right] > tab[largest]) {
            largest = right;
        }

        if (largest == i) break;

        tab.swap(i, largest);
        i = largest;
    }
}
```
- **But de l'algorithme** : Supprimer la racine du tas tout en rétablissant la propriété du tas.
- **Entrée** :
  - `tab` : Tableau représentant un tas.
- **Sortie** : Le tas après suppression de la racine.
- **Complexité temporelle** : O(log n), où n est la taille du tableau.
- **Description** : Cette fonction échange la racine (le plus grand élément dans un tas max) avec le dernier élément du tableau, puis réduit la taille du tas et restaure la propriété du tas en déplaçant l'élément échangé vers la position correcte.

---

### 4. Tri par Tas (Heap Sort)
```c
void heapSort(Array tab)
{
    for(int i = 1; i < tab.size(); i++)
    {
        insertHeap(tab.subArray(0,i+1));
    }
    
    for(int i = tab.size(); i > 0; i--)
    {
        removeRootHeap(tab.subArray(0,i));
    }
}
```
- **But de l'algorithme** : Trier un tableau en utilisant la structure du tas.
- **Entrée** :
  - `tab` : Tableau à trier.
- **Sortie** : Un tableau trié.
- **Complexité temporelle** : O(n log n), où n est la taille du tableau.
- **Description** : L'algorithme de tri par tas construit d'abord un tas à partir des éléments du tableau, puis extrait successivement la racine (le plus grand élément dans un tas max), et réorganise le tas pour garantir la propriété du tas à chaque extraction. Cela permet de trier les éléments en place.
