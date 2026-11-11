# Classification de Discours Politiques - Corpus DEFT 2009

---

## Description du projet
Ce projet s'inscrit dans le cadre d'une tâche de Traitement Automatique du Langage (TAL). L'objectif principal est de prédire l'appartenance politique d'un député européen (parti politique) à partir de la transcription de ses interventions au Parlement européen (Corpus DEFT 2009).

Le projet explore et compare deux approches de représentation textuelle couplées à un classifieur Séparateur à Vaste Marge (SVM) :
1. **Une approche Baseline** basée sur la fréquence pondérée des mots (TF-IDF).
2. **Une approche thématique** basée sur l'extraction de sujets latents via l'algorithme LDA (Latent Dirichlet Allocation).

## Technologies et Bibliothèques
* **Langage :** Python
* **Machine Learning & NLP :** `scikit-learn` (Pipelines, SVM, LDA, Vectorizers)
* **Traitement linguistique :** `spaCy` (modèle français `fr_core_news_md` pour la gestion des mots vides)

## Méthodologie

### 1. Prétraitement des données
Une étape cruciale du projet, en particulier pour l'approche thématique, a été la constitution d'un dictionnaire de mots vides (*stop-words*) robuste. 
Outre les mots outils standards fournis par `spaCy`, une méthode d'analyse fréquentielle automatisée a été mise en place pour détecter et filtrer le "bruit institutionnel" propre au corpus (ex: *monsieur, président, commission, parlement*).

### 2. Modèle Baseline : TF-IDF + SVM
* Vectorisation des textes avec `TfidfVectorizer` pour extraire la signature lexicale et rhétorique des discours.
* Classification avec un SVM (noyau linéaire).
* **Performances :** F1-Macro d'environ 0.41, prouvant la capacité du modèle à capter le vocabulaire idéologique.

### 3. Modèle Thématique : LDA + SVM
* Extraction de thèmes latents (Topic Modeling) avec `LatentDirichletAllocation` (testé avec 5, 10, 15 et 30 thèmes).
* Les discours sont représentés comme des vecteurs de probabilités thématiques avant d'être classés par le SVM.
* **Exploration des hyperparamètres :** Étude de l'impact du nombre de thèmes (`n_components`) et de la distribution des thèmes par document (`doc_topic_prior` / alpha).

---

## Configuration
*`pip install -r requirements.txt`*