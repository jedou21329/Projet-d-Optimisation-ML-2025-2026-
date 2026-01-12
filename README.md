# Mini-projet d’Optimisation – Algorithmes Déterministes, Stochastiques et Proximaux

> **Auteur** : Jedou Mohamed Bebacar (Matricule : C30824)  
> **Filière** : Master SSD – Statistique et Sciences de Données   
> **Université** : Université de Nouakchott Al Aasriya  
> **Date** : Janvier 2026  

---

## Objectif du projet

Ce mini-projet compare trois familles d’algorithmes d’optimisation sur un problème concret de **classification binaire** :

1. **Méthodes déterministes** : Descente de Gradient (GD) vs Gradient Conjugué (CG)  
2. **Méthodes stochastiques modernes** : SGD, RMSProp, Adam  
3. **Méthodes proximales (non lisses)** : ISTA vs FISTA avec régularisation L1  

L’objectif est d’analyser la **vitesse de convergence**, la **stabilité** et l’**impact de la régularisation** à la lumière des théorèmes des Chapitres 1 à 4 du cours d’optimisation.

---

##  Jeu de données

- **Nom** : `Breast Cancer Wisconsin (Diagnostic)`  
- **Source** : Bibliothèque `scikit-learn`  
- **Taille** : 569 échantillons × 30 features  
- **Cible** : Binaire (`-1` = maligne, `+1` = bénin)  
- **Features** : Mesures morphologiques de noyaux cellulaires (moyennes, erreurs-types, pires valeurs)  
- **Qualité** : Aucune valeur manquante, légèrement déséquilibré (63% bénin)

---

## Prétraitement

1. **Encodage de la cible** : `{0, 1}` → `{-1, +1}`  
2. **Standardisation** : Toutes les features sont centrées et réduites (`μ ≈ 0`, `σ = 1`)  
   → Nécessaire pour une régularisation équitable et une convergence stable.

---

## Méthodes implémentées (100 % manuelles)

| Phase | Algorithmes | Caractéristiques |
|------|------------|------------------|
| **Phase 1** | GD, CG | Déterministes, fortement convexes, pas fixe / backtracking |
| **Phase 2** | SGD (fixe/décroissant), RMSProp, Adam | Stochastiques, adaptation du pas, momentum |
| **Phase 3** | ISTA, FISTA | Non lisses, régularisation L1, seuil doux, parcimonie |

> Aucune boîte noire utilisée (`scipy.optimize.minimize` remplacé par des implémentations manuelles).

---

## Résultats clés

- **CG** converge **~30× plus vite** que GD (75 vs 2000 itérations).  
- **Adam** domine les autres optimiseurs stochastiques en stabilité et rapidité.  
- **FISTA** accélère **5×** la convergence par rapport à ISTA.  
- La **régularisation L1** permet une **sélection automatique de variables** :  
  - Pour `λ = 1e-2` → 11 features sur 30 sont nulles.  
  - Pour `λ = 1e-1` → 24 features sont nulles.

---


