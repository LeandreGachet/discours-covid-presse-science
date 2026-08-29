# Le COVID-19 dans la presse et dans la littérature scientifique

Un même événement, raconté par deux mondes qui ne s'écrivent pas de la même façon. La presse informe vite et prend position ; la recherche publie lentement et se garde de conclure. **Le ton et le vocabulaire divergent-ils, et cet écart bouge-t-il au fil de la pandémie ?**

Projet de Master en traitement automatique du langage, en trinôme.

## Démarche

**Deux corpus déséquilibrés par nature** — plus de **150 000 articles scientifiques** (*COVID-19 Research Papers Dataset*, PubMed via Kaggle) contre environ **7 000 articles de presse** (base CBC). Le déséquilibre n'est pas un défaut à corriger : il décrit le régime de production de chaque monde.

**Prétraitement** — agrégation temporelle par mois et par semaine, suppression des caractères problématiques, normalisation des espaces, retrait des mots outils.

**Représentation sémantique** par le modèle **`all-MiniLM-L6-v2`** (Hugging Face), qui projette chaque texte dans un espace où la proximité vaut proximité de sens.

**Analyse de sentiment** avec VADER, suivie dans le temps sur chacun des deux corpus.

**La mesure centrale : la distance sémantique comme série temporelle.** Un plongement moyen est calculé par mois et par corpus, puis la similarité cosinus entre les deux. On n'obtient plus « la presse et la science parlent différemment » — affirmation invérifiable — mais une courbe qui dit *quand* elles se rapprochent et quand elles s'écartent. C'est le passage d'une intuition à une grandeur mesurable.

**Limites discutées**, avec les prolongements identifiés : comparaison multilingue pour tester si le ton varie selon les pays, détection de désinformation, et remplacement de VADER — construit pour les réseaux sociaux — par un modèle de type BERT.

## Ce que ça produit

Une méthode pour comparer deux discours sur un même sujet sans les lire : deux séries — l'une de ton, l'autre de distance sémantique — qui rendent la comparaison quantifiable et reproductible sur d'autres corpus.

## Contenu

| | |
|---|---|
| `code/analyse_covid.ipynb` | le notebook complet — 24 cellules exécutées |
| `code/notes_de_travail.txt` | les notes de travail et les jeux de données visés |
| `presentation.pptx` | la présentation du projet |



## Sources

[COVID-19 Research Papers Dataset](https://www.kaggle.com/datasets) (PubMed, via Kaggle) · corpus de presse CBC · modèle [all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) (Hugging Face).

## Co-auteurs

Projet réalisé avec Nominoë Thomas et Gaspard Ichas. Publié avec leur accord.

---

**Léandre Gachet** — Master Mathématiques appliquées, statistique, Université de Rennes

## Reproduire

```bash
pip install kagglehub pandas numpy nltk sentence-transformers scikit-learn matplotlib
```

Les corpus sont téléchargés par `kagglehub` depuis le notebook (une authentification Kaggle est nécessaire). Le lexique VADER se récupère via `nltk.download`.
