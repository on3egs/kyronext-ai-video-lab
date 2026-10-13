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

## Échantillons visuels publiés

La [page de présentation](index.html) contient des lecteurs vidéo et des affiches générées depuis les fichiers réels. Les noms ci-dessous décrivent le contenu public :

- `media/ltx2_19b_30s_montage.mp4` — LTX-2 19B, montage d’essai 30 s, 256×256.
- `media/wan22_ti2v_5b_30s_reference.mp4` — Wan 2.2 TI2V 5B, vidéo de référence voiture, 30 s, 1024×576.
- `media/sana_video2_5b_femme_8s_native.mp4` — SANA Video 2.0 5B, sortie native, 8,04 s, 1280×736.
- `media/sana_video2_5b_extrait_defaut_48-60s.mp4` — extrait de 12 s du montage interpolé de 60 s; ce n’est pas une sortie native de 12 s.
- `media/sana_video_2b_smoke_1s.mp4` — smoke test SANA-Video 2B, 1,06 s.
- `media/hunyuan15_i2v_femme_5s.mp4` — HunyuanVideo 1.5 I2V, 5,04 s, 384×208.
- `media/wan21_flf_14b_jambes_5s.mp4` — Wan 2.1 FLF2V 14B, 5,06 s.
- `media/wan22_animate_14b_jambes_3s.mp4` — Wan 2.2 Animate 14B, 3,06 s.
- `media/interpolation_cpu_jambes_3s.mp4` — comparaison d’interpolation 2D CPU, pas une génération vidéo IA.

Les deux images de référence et les affiches correspondantes sont aussi publiées. Les journaux bruts, les poids et les autres médias de campagne restent dans l’archive locale. Chaque média est étiqueté selon sa nature afin de ne pas faire passer un montage pour une génération native.

## Règle de présentation

Ne pas confondre :

1. **Moteur opérationnel** : un MP4 local a été produit.
2. **Montage techniquement valide** : durée, codec et décodage sont conformes.
3. **Action visuellement réussie** : chaque image respecte la continuité et la physique demandées.

Seul le troisième point valide la scène. Il n’est pas atteint.
