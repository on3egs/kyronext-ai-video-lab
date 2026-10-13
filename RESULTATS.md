# Résultats synthétiques — BY MANIX

## Critère principal

Femme assise au siège conducteur → les deux jambes entrent dans l’habitacle → portière fermée seulement après l’entrée des pieds → voiture et cadrage stables.

**Verdict actuel : NON VALIDÉ.** Les erreurs physiques observées entraînent le refus du clip, même lorsque son MP4 se décode sans erreur.

## Historique des familles de modèles

| Famille | Formats/résolutions observés | Résultat principal |
|---|---|---|
| LTX-2 19B FP8 | Smoke test et montages de 30 s en scènes | Vidéo locale obtenue; dérive visuelle du véhicule dans les versions rapportées. Pas une validation de la scène femme/Pontiac. |
| HunyuanVideo 1.5 I2V distillé | 384×208, ~5 s natifs par plan | Pipeline exploitable; changement d’apparence et mouvement incorrect pour la jambe/portière. Montage 30 s fait de six plans séparés. |
| SANA-Video 2.0 5B | Smoke test 256×256; clips natifs jusqu’à 1280×736, ~8,04 s | Génération locale réussie. Les montages 30/60 s ralentis/interpolés n’ont pas rendu l’action physique cohérente; variante à personnage doublé refusée. |
| Wan 2.1 FLF2V 14B Q5_K_M | 512×288 | Résultat dégradé, rejeté. |
| Wan 2.2 Animate 14B Q5_K_M | 512×288, 49 images, 3,063 s | Identité et voiture plus stables sur quelques seeds; détails de bottes et action insuffisants. |
| Interpolation optique CPU | 512×288, 3,063 s | Démonstration 2D limitée; ne remplace pas une génération vidéo temporelle. |

## Prototypes récents conservés en local

- `Femme_Pontiac_WanAnimate_3s_PROTO_512x288.mp4` — véritable sortie Wan 2.2; progrès partiel, non final.
- `Femme_Pontiac_transition_3s_PROTO_INTERPOLATION.mp4` — mouvement des jambes interpolé sur composition fixe; non final.

Ils ne sont pas inclus dans ce dépôt brouillon. Les originaux et journaux détaillés restent dans l’archive locale de campagne.

## Règle de présentation

Ne pas confondre :

1. **Moteur opérationnel** : un MP4 local a été produit.
2. **Montage techniquement valide** : durée, codec et décodage sont conformes.
3. **Action visuellement réussie** : chaque image respecte la continuité et la physique demandées.

Seul le troisième point valide la scène. Il n’est pas atteint.
