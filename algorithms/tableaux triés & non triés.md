## Algorithmes de Manipulation de Tableaux

Cette section contient plusieurs algorithmes permettant de manipuler des tableaux d'entiers dans différentes situations. Les algorithmes abordent des opérations classiques sur des tableaux, telles que la recherche de valeurs spécifiques, la comparaison entre tableaux, et la fusion de tableaux triés.

### Algorithmes inclus :

1. **Minimum dans un tableau** : Ces fonctions permettent de trouver le minimum dans un tableau, tant pour les tableaux non triés que triés, en exploitant les propriétés de ces types de tableaux pour optimiser la recherche.

2. **Vérification d'égalité entre tableaux** : Ces algorithmes comparent deux tableaux pour déterminer s'ils sont égaux, avec une distinction entre les tableaux triés et non triés.

3. **Recherche de valeur dans un tableau** : Le premier algorithme utilise une recherche linéaire pour détecter la présence d'une valeur dans un tableau non trié, tandis que le second utilise une recherche binaire optimisée pour un tableau trié.

4. **Fusion de tableaux triés** : Cet algorithme fusionne deux tableaux déjà triés en un seul tableau trié, garantissant ainsi un temps d'exécution optimal en utilisant une approche de type "fusion" de l'algorithme de tri fusion.

Chaque algorithme est présenté avec son code source en C, accompagné d'une description détaillée de son but, des entrées et sorties, ainsi que de la complexité temporelle associée. L'objectif est de rendre ces algorithmes réutilisables pour la manipulation efficace des tableaux dans divers contextes.

---

### 1. Minimum - Trouver le minimum d'un tableau non trié
```c
int minimum(int *array, int N)
{
    if (N <= 0)
    {
        return 0;    
    }

    int min = array[0];
    
    for (int i = 0; i < N; i++)
    {
        if (array[i] < min)
        {
            min = array[i];
        }
    }
    
    return min;
}
```
- **But de l'algorithme** : Trouver et retourner le minimum des valeurs d'un tableau non trié.
- **Entrée** : 
  - `array` : Tableau d'entiers.
  - `N` : Taille du tableau.
- **Sortie** : Retourne la valeur minimale du tableau.
- **Complexité temporelle** : O(n), où n est la taille du tableau.
- **Description** : Cette fonction parcourt le tableau pour trouver la valeur minimale parmi les éléments.

---

### 2. Minimum - Trouver le minimum d'un tableau trié
```c
int minimum(int *array, int N)
{
    if (N <= 0)
    {
        return 0;    
    }
    
    return array[0];
}
```
- **But de l'algorithme** : Trouver et retourner le minimum des valeurs d'un tableau trié.
- **Entrée** : 
  - `array` : Tableau d'entiers trié.
  - `N` : Taille du tableau.
- **Sortie** : Retourne la première valeur du tableau (minimum).
- **Complexité temporelle** : O(1), car le tableau est trié et le minimum se trouve toujours à la première position.
- **Description** : Dans un tableau trié, le premier élément est toujours le minimum. La fonction retourne directement cet élément.

---

### 3. Equals - Tester l'égalité de deux tableaux non triés
```c
int equals(int *tab, int *tab2, int N)
{
    if (N <= 0)
    {
        return 0;
    }

    for(int i = 0; i < N; i++)
    {
        int value = tab[i];
        int countTab1 = 0;
        int countTab2 = 0;
        
        for (int j = 0; j < N; j++)
        {
            if(tab[j] == value)
            {
                countTab1++;
            }
            
            if(tab2[j] == value)
            {
                countTab2++;
            }
        }
        
        if (countTab1 != countTab2)
        {
            return 0;
        }
    }
    
    return 1;
}
```
- **But de l'algorithme** : Tester l'égalité de deux tableaux non triés.
- **Entrée** :
  - `tab` : Premier tableau d'entiers.
  - `tab2` : Deuxième tableau d'entiers.
  - `N` : Taille des deux tableaux.
- **Sortie** : Retourne 1 si les tableaux sont égaux, 0 sinon.
- **Complexité temporelle** : O(n²), où n est la taille des tableaux (car on compare chaque élément avec tous les autres).
- **Description** : Cette fonction compare les éléments de deux tableaux en comptant les occurrences de chaque valeur dans les deux tableaux. Si les comptes sont égaux pour chaque valeur, les tableaux sont considérés comme égaux.

---

### 4. Equals - Tester l'égalité de deux tableaux triés
```c
int equals(int *tab, int *tab2, int N)
{
    for (int i = 0; i < N; i++)
    {
        if (tab[i] != tab2[i])
        {
            return 0;  
        }
    }
    
    return 1;
}
```
- **But de l'algorithme** : Tester l'égalité de deux tableaux triés.
- **Entrée** : 
  - `tab` : Premier tableau d'entiers trié.
  - `tab2` : Deuxième tableau d'entiers trié.
  - `N` : Taille des deux tableaux.
- **Sortie** : Retourne 1 si les tableaux sont égaux, 0 sinon.
- **Complexité temporelle** : O(n), où n est la taille des tableaux.
- **Description** : Dans le cas de tableaux triés, les éléments doivent correspondre à la même position dans les deux tableaux pour que les tableaux soient considérés comme égaux.

---

### 5. Contains - Détecter si une valeur est présente dans un tableau non trié
```c
int contains(int *tab, int N, int val)
{
    int start = 0;
    int end;
    int middle;
    
    for(int i = start; i <= N; i++)
    {
        middle = (start + end) / 2;
        
        if(tab[i] == val)
        {
            return 1;
        }
        
        if(val < tab[i]){
            end = middle + 1;
        }
        else
        {
            end = middle - 1;
        }
    }
    
    return 0;
}
```
- **But de l'algorithme** : Détecter si une valeur est présente dans un tableau non trié.
- **Entrée** : 
  - `tab` : Tableau d'entiers.
  - `N` : Taille du tableau.
  - `val` : Valeur à rechercher dans le tableau.
- **Sortie** : Retourne 1 si la valeur est présente, 0 sinon.
- **Complexité temporelle** : O(n), où n est la taille du tableau (recherche linéaire).
- **Description** : Cette fonction parcourt chaque élément du tableau pour vérifier si la valeur recherchée est présente.

---

### 6. Contains - Détecter si une valeur est présente dans un tableau trié
```c
int contains(int *tab, int N, int val)
{
    int start = 0;
    int end = N;
    int middle;
    
    while (start <= end)
    {
        middle = (start + end) / 2;
        if(tab[middle] == val)
        {
            return 1;
        }
        
        if(val < tab[middle])
        {
            end = middle - 1;
        }
        else
        {
            start = middle + 1;
        }
    }
    return 0;
}
```
- **But de l'algorithme** : Détecter si une valeur est présente dans un tableau trié.
- **Entrée** : 
  - `tab` : Tableau d'entiers trié.
  - `N` : Taille du tableau.
  - `val` : Valeur à rechercher dans le tableau.
- **Sortie** : Retourne 1 si la valeur est présente, 0 sinon.
- **Complexité temporelle** : O(log n), où n est la taille du tableau (recherche binaire).
- **Description** : Cette fonction utilise la recherche binaire pour vérifier si la valeur existe dans un tableau trié.

---

### 7. Merge - Fusionner deux tableaux triés
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
- **Sortie** : Retourne un nouveau tableau trié contenant tous les éléments des deux tableaux d'entrée.
- **Complexité temporelle** : O(n), où n est la taille combinée des deux tableaux.
- **Description** : Cette fonction fusionne deux tableaux triés en comparant leurs éléments un par un et en insérant le plus petit dans le tableau fusionné. 

---
