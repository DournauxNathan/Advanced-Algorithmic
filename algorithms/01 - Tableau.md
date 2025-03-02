## Algorithmes

Cette section présente une série d'algorithmes utilisés pour manipuler des tableaux d'entiers en C. Chaque algorithme est expliqué en détail, accompagné de son code source et d'une description de son fonctionnement, de ses entrées et sorties, ainsi que de sa complexité temporelle.

Les algorithmes inclus dans cette section permettent de réaliser diverses opérations sur les tableaux, telles que l'affichage, l'insertion et la suppression d'éléments, ainsi que l'inversion de l'ordre des éléments.

Chaque algorithme est accompagné d'exemples d'utilisation et d'une analyse de sa performance pour fournir une compréhension complète de son fonctionnement et de son efficacité dans différents scénarios.

Les algorithmes suivants sont inclus :

1. **Display - Afficher un tableau** : Affiche les éléments d'un tableau d'entiers.
2. **Erase - Supprimer un élément du tableau** : Supprime un élément d'un tableau à une position spécifiée.
3. **Insert - Insérer un élément dans le tableau** : Insère un élément à une position donnée dans le tableau.
4. **Invert - Inverser un tableau** : Inverse l'ordre des éléments dans un tableau.

Ces algorithmes peuvent être utilisés pour des tâches de manipulation de tableaux dans divers contextes et sont essentiels pour comprendre les bases de la gestion de données en mémoire.

---
### 1. Display - Afficher un tableau
```c
void display(int* tab, int taille)
{
    for(int i = 0; i < taille; i++) {
        printf("%d ", tab[i]);
    }
}
```
- **But de l'algorithme** : Afficher les éléments d'un tableau d'entiers.
- **Entrée** :
  - `tab` : Tableau d'entiers.
  - `taille` : Taille du tableau (nombre d'éléments dans le tableau).
- **Sortie** : Aucun retour, affiche les éléments du tableau dans la console.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : Cette fonction parcourt un tableau d'entiers et affiche chaque élément séparé par un espace.
---
### 2. Erase - Supprimer un élément du tableau
```c
void erase(int *tab, int N, int position)
{
    for (int i = position; i < N-1; i++){
        tab[i] = tab[i + 1];
    }
}
```
- **But de l'algorithme** : Supprimer un élément à une position donnée dans un tableau.
- **Entrée** : 
  - `tab` : Tableau d'entiers.
  - `N` : Nombre d'éléments dans le tableau.
  - `position` : Index de l'élément à supprimer.
- **Sortie** : Aucun retour, le tableau est modifié directement.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : Cette fonction supprime l'élément à la position spécifiée dans le tableau, puis décale tous les éléments suivants d'une position vers la gauche pour combler l'espace vide.
---
### 3. Insert - Insérer un élément dans le tableau
```c
void insert(int *tab, int N, int position, int value)
{
    for (int i = N-1; i >= position; i--)
    {
        tab[i+1] = tab[i];
    }
    tab[position] = value;
}
```
- **But de l'algorithme** : Insérer une valeur à une position donnée dans un tableau.
- **Entrée** : 
  - `tab` : Tableau d'entiers.
  - `N` : Nombre d'éléments dans le tableau.
  - `position` : Index où la nouvelle valeur doit être insérée.
  - `value` : La valeur à insérer dans le tableau.
- **Sortie** : Aucun retour, le tableau est modifié directement.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : Cette fonction insère une nouvelle valeur à la position spécifiée dans le tableau en décalant les éléments suivants d'une position vers la droite.
---
### 4. Invert - Inverser un tableau
```c
void invert(int *array, int N)
{
    int temp;
    
    for (int i = 0; i < N/2; i++)
    {
        temp = array[i];
        array[i] = array[N-1-i];
        array[N-1-i] = temp;
    }
}
```
- **But de l'algorithme** : Inverser les éléments d'un tableau.
- **Entrée** : 
  - `array` : Tableau d'entiers.
  - `N` : Taille du tableau.
- **Sortie** : Aucun retour, le tableau est modifié directement.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : Cette fonction inverse les éléments du tableau en échappant les valeurs aux positions opposées jusqu'à la moitié du tableau.
