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

## Interface

La page utilise maintenant un fond original de KITT, un léger effet scanner rouge et un parallax discret au défilement. Les animations respectent le réglage système de réduction des mouvements. Un compteur de visiteurs réel nécessite un service de mesure configuré; aucun chiffre de fréquentation fictif n’est affiché.

## Périmètre

Ce dépôt ne contient ni poids de modèles, ni photo source personnelle, ni journal brut, ni configuration privée de KYRONEXT. Il contient maintenant une sélection de vidéos générées lors des essais, leurs affiches extraites des vidéos, ainsi que les deux images de référence de la scène. Les montages et extraits sont explicitement signalés; ils ne représentent pas tous les essais. Les mesures décrivent cet AGX et ces essais, pas des benchmarks universels.

## Hébergement

Page statique publiée avec GitHub Pages. Elle ne contacte pas l’AGX, n’ouvre aucun port et n’a pas besoin d’accéder au site KYRONEXT. GitHub Pages peut servir un site depuis un dépôt public avec GitHub Free. Une adresse `github.io` est utilisée; aucun DNS KYRONEXT n’est modifié. [Documentation GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
