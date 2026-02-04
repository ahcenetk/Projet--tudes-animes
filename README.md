# 🎬 études animes : Mon Algorithme Anti-Hype

Salut ! Voici **études animes**.
C'est un projet Data que j'ai monté parce que j'en avais marre des classements d'animés classiques (type MyAnimeList) où la "Hype" l'emporte toujours sur la qualité réelle.

J'ai voulu voir ce qui se passait si on notait les animés de manière **mathématique** et pas juste émotionnelle.


## Le Problème

Actuellement, une série comme *Black Clover* peut avoir une note globale super élevée (8.1/10) juste parce qu'elle est populaire, alors qu'elle a des épisodes catastrophiques (Régularité de 3.0/10 dans mon analyse).

Mon objectif : **Créer un score qui punit l'instabilité.**


## Ma Solution (L'Algorithme)

J'ai codé une formule pondérée sur Python pour re-noter 59 animés. Voici la recette exacte que j'ai utilisée :

$$Score = (0.5 \times Note\ Globale) + (0.4 \times Régularité) + (0.1 \times Bonus\ Fini)$$

* **50% Note Globale** : Je respecte quand même l'avis des fans.
* **40% Régularité** : C'est le cœur du système. Je calcule l'écart-type entre le meilleur et le pire épisode. Si c'est les montagnes russes, la note chute.
* **10% Statut "Fini"** : Un petit bonus pour récompenser les histoires qui ont une vraie fin (contrairement aux séries en pause éternelle).



##  Comment est rangé le projet ?

* `animes.csv` : Les données brutes (doublons, infos manquantes...).
* `dataset_etClassement.ipynb` : Le moteur. C'est ici que je nettoie tout et que j'applique la formule.
* `animes_calcules_complet.csv` : Le résultat final avec les nouvelles notes.
* `Rapport_etVisualisation.ipynb` : Les graphiques pour comprendre les résultats.



##  Ce que les chiffres révèlent (Vraies Stats)

En appliquant mon algo, la réalité a frappé :

1.  **Chute des notes** : La moyenne est passée de **8.32** (Note Publique) à **7.17** (Mon Score). Mon système est beaucoup plus sévère.
2.  **Le Vrai Top 1** : C'est **Your Lie in April** qui gagne (Score: 7.96). Pourquoi ? Parce qu'en plus d'être bon (Note 8.6), il est ultra régulier (8.9/10 en stabilité) et il est fini.
3.  **Le "Piège"** : Des séries comme *Boruto* se font détruire par l'algo (Score final : 5.6) à cause d'une trop grande différence de qualité entre les épisodes fillers et les canons.


## Lancer le projet chez toi

Tu veux voir si ton animé préféré survit à mon algo ?

1.  Clone le repo :
    ```bash
    git clone [https://github.com/ahcenetk/Projet--tudes-animes]
    ```
2.  Installe les outils :
    ```bash
    pip install pandas seaborn matplotlib wordcloud
    ```
3.  Lance les notebooks dans l'ordre (d'abord le nettoyage, ensuite la visu).

---

**Ahcene TERKOUCHE**
*Projet Data Science 2026 - études animes*
