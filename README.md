# KYRONEXT AI Video Lab — retour d’expérience

**BY MANIX**

**Site :** [KYRONEXT AI Video Lab](https://on3egs.github.io/kyronext-ai-video-lab/)

Rapport de tests de génération vidéo IA réalisés localement sur NVIDIA Jetson AGX Orin 32 Go. La page explique le système employé, les familles de modèles testées, les mesures obtenues et les résultats refusés.

> **Résultat honnête :** les moteurs ont généré des clips sur l’AGX, mais la scène précise demandée — une femme qui rentre ses deux jambes dans une Pontiac, puis ferme la portière, dans une vidéo cohérente de 30 secondes — n’a pas passé la validation physique. Les clips longs assemblés ou ralentis sont explicitement distingués d’un mouvement inédit continu.

## Lire le rapport

- [Présentation](index.html)
- [Rapport complet](RAPPORT.md)
- [Résultats et mesures](RESULTATS.md)
- [Sources officielles des modèles](SOURCES.md)

## Périmètre

Ce dépôt ne contient ni poids de modèles, ni photo source, ni vidéo, ni journal brut, ni configuration privée de KYRONEXT. Les échantillons vidéo restent dans l’archive locale. Les mesures décrivent cet AGX et ces essais; elles ne sont pas des benchmarks universels.

## Hébergement

Page statique publiée avec GitHub Pages. Elle ne contacte pas l’AGX, n’ouvre aucun port et n’a pas besoin d’accéder au site KYRONEXT. GitHub Pages peut servir un site depuis un dépôt public avec GitHub Free. Une adresse `github.io` est utilisée; aucun DNS KYRONEXT n’est modifié. [Documentation GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
