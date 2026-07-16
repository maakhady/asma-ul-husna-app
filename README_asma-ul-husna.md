# Asma-ul-Husna — PWA d'apprentissage avec IA générative

Application web progressive (PWA) d'apprentissage quotidien des 99 noms d'Allah, conçue pour un parcours à deux. Chaque jour, l'application présente un nom avec une leçon complète et un quiz de révision, tous deux **générés dynamiquement par l'API Claude d'Anthropic**.

## Fonctionnalités

- Parcours d'apprentissage progressif : un nom par jour, avec suivi de la progression et mode révision des jours complétés
- Leçons générées par IA : pour chaque nom, l'API Claude produit une explication du sens spirituel, une synthèse des points clés et une réflexion d'application quotidienne
- Quiz de récapitulatif : trois questions à choix multiples générées automatiquement à partir du contenu de la leçon du jour
- Mode hors-ligne résilient : en cas d'échec de l'appel API, un contenu de secours local est affiché afin de ne jamais interrompre la session d'apprentissage

## Intégration de l'IA

L'application illustre plusieurs bonnes pratiques d'intégration d'un LLM dans un produit :

- **Sorties structurées** : les prompts système imposent une réponse au format JSON strict (schéma explicite, sans texte parasite), ce qui permet de mapper directement la réponse du modèle sur les composants de l'interface
- **Parsing défensif** : la réponse est nettoyée (suppression des balises Markdown éventuelles) puis parsée, avec gestion des erreurs
- **Dégradation gracieuse** : chaque appel est encapsulé dans un try/catch avec un contenu de repli, garantissant le fonctionnement de l'application même sans connexion à l'API
- **Contrôle du ton et du périmètre** : le prompt système cadre précisément le registre, la longueur et le format des contenus générés

## Stack technique

| Couche | Technologies |
|---|---|
| Frontend | HTML, CSS, JavaScript (vanilla, fichier unique) |
| IA | API Anthropic (modèle Claude Sonnet), prompts structurés JSON |
| Déploiement | Netlify |

## Architecture et évolution prévue

La version actuelle appelle l'API directement depuis le client. La prochaine étape est la migration vers une **fonction serverless Netlify** faisant office de proxy : la clé API reste côté serveur, le client appelle un endpoint interne (`/.netlify/functions/ask-claude`), ce qui permet un déploiement public sécurisé sans exposition de secrets.

## Lancement local

Ouvrir `index.html` dans un navigateur. Les appels à l'API nécessitent une clé Anthropic valide (voir la section Architecture ci-dessus pour l'approche recommandée en production).

## Auteure

**Mame Khady Laye DIAW** — Développeuse Full-Stack, Dakar
[GitHub](https://github.com/maakhady) · [LinkedIn](https://linkedin.com/in/mamekhady)
