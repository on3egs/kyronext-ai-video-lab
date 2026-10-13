# Générer une action crédible sur un Jetson : ce que nos essais ont appris

**BY MANIX — KYRONEXT AI Video Lab — octobre 2026**

## Résumé

Nous voulions réaliser localement une scène de 30 secondes sur un NVIDIA Jetson AGX Orin 32 Go : une femme est assise au siège conducteur d’une Pontiac, fait entrer ses deux jambes dans l’habitacle, puis ferme la portière. Le mouvement devait respecter la géométrie de la voiture et l’ordre réel des gestes.

Nous avons testé plusieurs générateurs vidéo, des réglages allant de petits essais à des clips plus longs, des références d’image, des guides de pose, des masques et des montages. Les moteurs ont effectivement produit des vidéos. Pourtant, le critère principal n’a pas été atteint : sur les rendus examinés, une jambe reste dehors, la portière la recouvre, les jambes fusionnent ou le corps et le véhicule dérivent. Les montages ralentis ou interpolés ne réparent pas ces erreurs.

**Conclusion : échec de la scène demandée, pas échec de l’installation vidéo.** Les moteurs tournent localement; ils ne garantissent pas encore une chorégraphie précise et une géométrie stable sur cette tâche.

## Machine et chaîne utilisée

- Machine : NVIDIA Jetson AGX Orin, mémoire unifiée 32 Go.
- Plateforme logicielle mesurée dans les journaux : JetPack/L4T 6.2.2, CUDA 12.6, PyTorch Jetson 2.8.0+cu126.
- Orchestration : ComfyUI dans un environnement Python isolé sur SSD externe.
- Génération : calcul local sur l’AGX; un seul travail vidéo lourd à la fois.
- Assistant de prompts et orchestration KYRONEXT : Gemma 4 servi localement par Ollama. Il a été temporairement déchargé lorsque nécessaire pour libérer la mémoire, puis restauré et contrôlé. Il n’effectue pas le calcul de diffusion vidéo.
- FFmpeg/ffprobe : assemblage, conversion et vérification technique des fichiers.

La mémoire du Jetson est partagée entre CPU et GPU; les valeurs de RAM disponible ne sont donc pas une mesure indépendante de VRAM. Les mesures d’une campagne décrivent cet appareil et ces réglages seulement.

## Modèles évalués

| Modèle | Essai local | Ce qu’il a montré | Résultat pour l’entrée dans la voiture |
|---|---|---|---|
| SANA-Video 2.0 5B | BF16; smoke test I2V 256×256, 17 images, 2,125 s; essais ultérieurs à 832×480 et 1280×736 | Le pipeline I2V fonctionne. Les clips longs livrés ont été étirés/interpolés depuis environ 8,04 s natifs. | Échec : gestes ambigus, cadrage/personnage qui dérive; une variante présente un personnage en double. |
| HunyuanVideo 1.5 I2V distillé | FP8 scaled converti/émulé en FP16 dans cette configuration; 8 étapes, CFG 1, shift 7; 384×208, environ 5,04 s par clip | Six clips séparés ont été assemblés en un film de 30 s; le fichier est décodable, avec variations visibles entre plans. | Échec : une jambe reste dehors pendant que le torse entre; la portière recouvre la jambe. Un clip d’entrée de 5 s a aussi été refusé après revue. |
| Wan 2.1 FLF2V 14B Q5_K_M | Conditionnement première/dernière image, essais à 512×288 | Le conditionnement de deux images n’a pas empêché les artefacts. | Échec : corruption visuelle et transition incohérente. |
| Wan 2.2 Animate 14B Q5_K_M | BF16, guides de pose/masque, 512×288, 49 images à 16 i/s (3,063 s), 20 étapes | Une variante maintient mieux la voiture et l’identité; un mouvement des jambes apparaît. | Progrès partiel seulement : les bottes se confondent et le mouvement n’est pas assez naturel pour le film final. |
| Interpolation optique CPU | 49 images, 512×288, 3,063 s; composition sur fond fixe | Un essai limité aux jambes évite mieux la dérive du décor. | Prototype partiel, trop subtil et peu détaillé; ce n’est pas une vidéo générée par diffusion. Une variante avec alpha a été rejetée pour transparence/ghosting. |

## Ce que signifie « 30 secondes » dans les résultats

La durée d’un MP4 ne signifie pas que le modèle a inventé autant de mouvement cohérent. Certains essais de 30 ou 60 secondes sont des assemblages de scènes courtes, du ralentissement ou de l’interpolation d’images. Les rapports les identifient explicitement. Une vidéo peut être valide techniquement — H.264, durée et nombre d’images conformes, décodage FFmpeg complet — tout en étant refusée visuellement.

Pour le film de 30 secondes Hunyuan, six générations d’environ 5,04 secondes ont été coupées et assemblées. Pour SANA, les versions longues dérivent de clips natifs d’environ 8,04 secondes. Ce sont des montages de test, pas 30 ou 60 secondes de mouvement inédit.

## Pourquoi la scène est difficile

Le modèle doit respecter en même temps l’identité de la personne, la position assise du bassin, deux jambes qui se déplacent l’une après l’autre, l’occlusion du seuil et du siège, la portière fixée sur sa charnière et le bon ordre de fermeture. Une consigne textuelle seule ne constitue pas une contrainte mécanique. Les références de début et de fin aident, mais ne déterminent pas à elles seules chaque image intermédiaire.

La revue image par image a aussi corrigé une fausse conclusion antérieure : un clip semblait prometteur sur une petite planche de contrôle, mais l’examen à vitesse native a révélé la jambe encore dehors au moment où la porte se ferme. Nous avons donc retiré l’étiquette de réussite et documenté le refus.

## Mesures et limites

- Test SANA de faisabilité à 256×256 : 17 images, 8 FPS, 2,125 s; génération mesurée à 3,51 s hors chargement. Ce n’est pas un benchmark 720p.
- Essais Hunyuan de 5,04 s à 384×208 : environ 280 à 391 secondes selon le plan; le texte encodeur CPU contribue au temps total.
- Essais Wan 2.2 de 3,063 s à 512×288 : selon l’essai, environ 13 minutes de diffusion et décodage isolé. Température maximale relevée sur les zones thermiques accessibles durant cette série : 52,7 °C; minimum de RAM disponible observé : environ 6,9 Gio.
- Dans une campagne Hunyuan séparée, minimum de RAM disponible observé : environ 1,85 Gio. La génération a été limitée et séquencée; ce niveau montre que la marge mémoire était faible.
- Les températures sont celles des zones système accessibles; aucune mesure NVMe n’est revendiquée si le capteur n’a pas fourni de valeur.

Ces chiffres ne permettent pas de comparer directement la qualité des modèles : résolutions, durées, samplers, formats de poids et objectifs variaient.

## Prochaine étape raisonnable

La voie la plus prometteuse est un tournage de référence très court, cadré de côté, où une personne s’assoit, rentre les jambes, puis ferme la porte. Un mouvement réel fournit une trajectoire et des occultations vérifiables qu’une série d’images générées ne garantit pas. L’AGX pourrait ensuite appliquer un transfert de mouvement/identité ou générer des plans de coupe autour de cette action. Une nouvelle génération ne sera déclarée réussie qu’après inspection de toutes les images à vitesse native selon les critères physiques établis.

## Échantillons visuels

Une sélection de vidéos réellement produites, d’affiches extraites de ces vidéos et d’images de référence est maintenant disponible dans la [galerie de la page du projet](index.html). Les légendes donnent résolution et durée et identifient les sorties natives, les montages, l’interpolation CPU et les défauts retenus. Les échantillons illustrent les essais représentatifs; ils ne constituent pas l’archive complète de campagne. Aucun journal brut, poids de modèle ni configuration privée n’est publié.

## État à la publication

- Les moteurs et modèles vidéo ont produit des fichiers localement.
- Plusieurs vidéos de 30/60 secondes existent comme montages d’essai; elles ne prouvent pas une action continue et correcte.
- La scène femme/Pontiac n’a pas atteint les critères de réussite physique.
- Le prototype Wan de 3 secondes le plus stable reste un progrès partiel, pas le résultat final.
- Gemma/KITT a été restauré et son endpoint local a répondu `status: ok` après les essais rapportés.

**Ce rapport documente un échec technique circonscrit avec mesures et essais reproductibles. Il ne prétend pas que la génération vidéo locale sur AGX est impossible.**
