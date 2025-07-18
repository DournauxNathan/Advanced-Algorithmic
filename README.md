# Algorithmie Avancée

## Description
Ce repository contient une collection d'algorithmes de base en langage C, couvrant diverses structures de données et techniques classiques en algorithmique. Les algorithmes sont organisés de manière modulaire, chaque section ayant des fonctions qui illustrent leur application et leur utilisation.

## Table des matières
- [Introduction](#introduction)
- [Structures de données](#structures-de-données)
  - [Pile](#pile)
  - [File](#file)
  - [Listes chaînées](#listes-chaînées)
- [Algorithmes de tri](#algorithmes-de-tri)
  - [Tri Fusion](#tri-fusion)
  - [Tri Rapide](#tri-rapide)
  - [Tri par Tas](#tri-par-tas)
- [Applications](#applications)
  - [Calculette (Pile)](#application-de-la-pile-calculette)
  - [Listes triées et manipulation](#listes-triées-et-manipulation)
- [Arbres](#arbres)
  - [Arbres Binaires](#arbres-binaires)
  - [Parcours d’Arbres](#parcours-darbres)
  - [Arbres Binaires de Recherche (BST)](#arbres-binaires-de-recherche-bst)
  - [Arbres AVL](#arbres-avl)
  - [Arbres Préfixes (Trie)](#arbres-préfixes-trie)

## Introduction
Ce repository est destiné à servir de référence et d'exemple pour différents algorithmes et structures de données couramment utilisés en programmation.

## Structures de données

### Pile
*Structure de type LIFO (Last In First Out)*

Fonctionnalités :
- Vérification pile vide / pleine
- Empilement / dépilement
- Affichage

### File
*Structure de type FIFO (First In First Out)*

Fonctionnalités :
- Vérification file vide / pleine
- Enfilement / défilement
- Affichage

### Listes chaînées
Les listes chaînées permettent une gestion dynamique de mémoire et une insertion efficace.

Fonctionnalités :
- Insertion / suppression en tête ou en fin
- Recherche par valeur
- Affichage
- Fusion de listes
- Inversion de liste
- Détection de doublons
- Tests de circularité et de palindromes

## Algorithmes de tri

### Tri Fusion
Tri récursif basé sur la division du tableau puis fusion.

### Tri Rapide
Tri récursif basé sur un pivot et une partition.

### Tri par Tas
Tri basé sur une structure de tas binaire max ou min.

## Applications

### Application de la Pile : Calculette
Évaluation d'expressions arithmétiques postfixées via une pile.

### Listes triées et manipulation
Utilisation des listes pour stocker des valeurs triées, avec opérations d’insertion ordonnée, suppression et fusion.

## Arbres

### Arbres Binaires
Implémentation d’un arbre binaire avec :
- Calcul de la taille (`treeSize`)
- Calcul de la hauteur (`treeHeight`)
- Nombre de feuilles (`leafsCount`)
- Vérification d’arbre complet (`isFull`)
- Inversion d’arbre (`reverseTree`)

### Parcours d’Arbres
- Parcours préfixé (préordre)
- Parcours infixé (inordre)
- Parcours postfixé
- Parcours en largeur (BFS)
- Versions itératives avec pile ou file

### Arbres Binaires de Recherche (BST)
Arbres binaires avec propriété de tri :
- Recherche (`contains`)
- Insertion (`insert`)
- Suppression (`remove`)
- Recherche de valeur maximale (`getMaxNode`)

### Arbres AVL
Arbres binaires de recherche auto-équilibrés :
- Calcul du déséquilibre (`getBalance`)
- Rotations gauche / droite
- Insertion et suppression équilibrées (`insert`, `remove`)
- Mise à jour de la hauteur

### Arbres Préfixes (Trie)
Arbres spécialisés pour représenter des ensembles de mots :
- Insertion de mot (`insert`)
- Recherche d’un mot (`contains`)
- Affichage de tous les mots (`display`)
- Comptage de mots (`wordCount`)
- Taille de l’arbre (`treeSize`)