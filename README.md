# Hackaton 2

Ce projet implémente un **pipeline automatisé de contenu GenAI** (*Generative AI Content Pipeline*). Il permet de générer du texte, de le résumer, d'en évaluer la qualité automatiquement et de filtrer les contenus éthiquement douteux. Le script effectue une analyse comparative (benchmark) de différentes combinaisons de modèles légers adaptés aux ressources CPU.

---

## 📋 Contexte du Projet

Ce projet répond au défi **"Generative AI Content Pipeline With Workflow Automation"**.

### Objectif Global
Construire un pipeline de bout en bout qui :
1.  Génère du texte ou des images.
2.  Vérifie la qualité du contenu.
3.  Applique un filtrage éthique.
4.  Fonctionne sur des ressources modestes (CPU).

### Workflow Implémenté
1.  **Prompt :** Extrait du dataset IMDB.
2.  **Génération :** Utilisation de modèles Transformers légers (`distilgpt2`, `t5-small`).
3.  **Contrôle Qualité :** Résumé automatique + Vérification sémantique.
4.  **Filtre Éthique :** Détection de mots-clés interdits.
5.  **Output :** Visualisation graphique des performances (Temps vs Qualité).

---

## ⚙️ Architecture Technique

Le script `main.py` exécute une **analyse comparative** de 6 combinaisons de modèles différentes.

### 1. Modèles Utilisés
Le code teste toutes les permutations entre :
* **Génération (Gen) :** `distilgpt2`, `t5-small`, `google/flan-t5-small`
* **Résumé (Sum) :** `t5-small`, `google/flan-t5-small`

### 2. Pipeline de Traitement (`MultiModelPipeline`)
Pour chaque item, le pipeline suit ces étapes :

1.  **Génération Adaptative :** Détection automatique du type de tâche (`text-generation` ou `text2text-generation`) selon le modèle.
2.  **Résumé Automatique :** Synthèse du texte généré pour vérification.
3.  **Métriques de Qualité (Auto-Eval) :**
    * **Sémantique :** Calcul de similarité cosinus entre le *Prompt* et le *Résumé* via `SentenceTransformer` (`all-MiniLM-L6-v2`).
    * **Diversité :** Ratio de mots uniques pour éviter les répétitions en boucle.
    * **Longueur :** Vérification de la consistance du texte.
4.  **Filtre Éthique :** Rejet si présence de mots bannis (ex: "hate", "violence").

---

## 🚀 Installation et Démarrage

### Prérequis
* Python 3.8 ou supérieur
* Connexion Internet (pour le téléchargement initial des modèles Hugging Face)

### Installation des dépendances

```bash
pip install torch transformers sentence-transformers datasets matplotlib numpy scikit-learn

## 👥 Auteurs

Mehdi Al-Ajhoury Emmanuel Mussche
