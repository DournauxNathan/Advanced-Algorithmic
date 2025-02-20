# Algorithmie Avancée

## Description
Ce repository contient une collection d'algorithmes de base en langage C, couvrant diverses structures de données et techniques classiques en algorithmique. Les algorithmes sont organisés de manière modulaire, chaque section ayant des fonctions qui illustrent leur application et leur utilisation.

## Table des matières
- [Introduction](#introduction)
- [Structures de données](#structures-de-données)
  - [Pile](#pile)
  - [File](#file)
- [Algorithmes de tri](#algorithmes-de-tri)
  - [Tri Fusion](#tri-fusion)
  - [Tri Rapide](#tri-rapide)
  - [Tri par Tas](#tri-par-tas)
- [Application de la Pile : Calculette](#application-de-la-pile-calculette)
- [Licence](#licence)

## Introduction
Ce repository est destiné à servir de référence et d'exemple pour différents algorithmes et structures de données couramment utilisés en programmation. Il couvre des structures telles que la pile, la file, ainsi que des algorithmes de tri comme le tri fusion, tri rapide et tri par tas.

## Structures de données

### Pile
Une **pile** est une structure de données de type LIFO (Last In, First Out), où le dernier élément ajouté est le premier à être retiré. Les opérations principales incluent l'insertion (empilement), le retrait (dépilement), et la vérification de l'état de la pile.

#### Fonctionnalités :
- Vérifier si la pile est vide
- Vérifier si la pile est pleine
- Empiler un élément
- Dépiler un élément
- Afficher les éléments de la pile

### File
Une **file** est une structure de données de type FIFO (First In, First Out), où le premier élément ajouté est le premier à être retiré. Les opérations de base incluent l'enfiler (ajout à la fin) et défiler (retrait du début).

#### Fonctionnalités :
- Vérifier si la file est vide
- Vérifier si la file est pleine
- Enfiler un élément
- Défiler un élément
- Afficher les éléments de la file

## Algorithmes de tri

### Tri Fusion
Le **tri fusion** (Merge Sort) est un algorithme de tri basé sur la technique du "diviser pour régner". Il divise récursivement le tableau en sous-tableaux plus petits, trie chacun d'eux et les fusionne dans un tableau trié.

### Tri Rapide
Le **tri rapide** (Quick Sort) est un algorithme de tri qui choisit un pivot pour partitionner le tableau et trie récursivement les deux sous-parties.

### Tri par Tas
Le **tri par tas** (Heap Sort) trie les éléments en construisant un tas à partir du tableau et en extrayant l'élément maximal ou minimal pour les ajouter dans le tableau trié.

## Application de la Pile : Calculette
Une **calculette** est implémentée en utilisant une pile pour évaluer des expressions arithmétiques simples (addition, soustraction, multiplication). Elle parcourt la chaîne de caractères représentant l'expression et applique les opérations sur les éléments empilés.
