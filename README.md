# Reconnaissance de chiffres manuscrits

Classification de chiffres manuscrits de 0 à 9, à partir d'images de 8 × 8 pixels, avec scikit-learn. Le projet compare plusieurs modèles de classification, règle le meilleur et analyse ses erreurs.

Le jeu de données `load_digits` est inclus dans scikit-learn : aucun téléchargement n'est nécessaire.

## Structure

```
reconnaissance de chiffres manuscrits/
├── notebook/
│   └── digits_classification.ipynb   Comparaison des modèles, réglage et évaluation
├── requirements.txt
└── README.md
```

## Démarche

1. Vérification des données : forme, valeurs manquantes, effectifs par chiffre.
2. Séparation stratifiée train/test (80/20). Le test n'est utilisé qu'une fois.
3. Référence : prédire toujours la classe majoritaire.
4. Comparaison de quatre modèles par validation croisée à 5 plis : régression logistique, K plus proches voisins, SVM à noyau RBF, forêt aléatoire.
5. Réglage du SVM (`C` et `gamma`) par validation croisée.
6. Évaluation finale sur le jeu de test.
7. Analyse des erreurs.

## Résultats

| Étape | Accuracy | F1 macro |
|---|---|---|
| Référence (classe majoritaire, test) | 0,100 | 0,018 |
| Meilleur modèle en validation (SVM, C = 1) | 0,981 | — |
| Test final (SVM, C = 1) | 0,975 | 0,975 |

Sur les 360 images de test, le modèle fait 9 erreurs. Les confusions les plus fréquentes sont 8 → 1 et 9 → 7.

## Limites

- Le jeu est petit (360 images de test) : un écart d'un ou deux points n'est pas significatif.
- Les images sont en 8 × 8 pixels, ce qui limite les détails des traits.
- Les données proviennent d'un seul style d'écriture, scanné et régulier. Le modèle n'a pas été évalué sur des écritures libres.

## Installation

```bash
pip install -r requirements.txt
```

## Utilisation

```bash
cd notebook
jupyter notebook digits_classification.ipynb
```

Exécutez les cellules dans l'ordre, ou utilisez *Restart Kernel and Run All*.