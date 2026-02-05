# études animes : Mon Algorithme Anti-Hype

Salut ! Voici **études animes**.
C'est un projet Data que j'ai monté parce que j'en avais marre des classements d'animés classiques (type MyAnimeList) où la "Hype" l'emporte toujours sur la qualité réelle.

J'ai voulu voir ce qui se passait si on notait les animés de manière **mathématique** et pas juste émotionnelle.

##  La Technique

Pour réaliser ce projet, je n'ai pas voulu sortir une usine à gaz. J'ai choisi les outils standards et efficaces de la Data Science en Python.

Voici comment j'ai utilisé chaque brique :

 Outil , À quoi ça m'a servi concrètement ? 

**Pandas** 
**Le Cerveau.** C'est lui qui fait tout le travail de l'ombre : nettoyer les lignes vides (`dropna`), calculer les écarts-types pour la *Régularité* et appliquer ma formule de scoring sur tout le dataset. 
 **Seaborn** 
 **Les Yeux.** Indispensable pour voir ce que les chiffres cachent. C'est grâce à lui que j'ai pu croiser 4 informations sur le même graphique (le Scatter Plot "Popularité vs Qualité"). 
**Matplotlib**  
**Le Cadre.** Je l'utilise en duo avec Seaborn pour gérer les détails techniques : titrer les graphiques, régler la taille des images et les sauvegarder proprement en PNG. |
**Jupyter** 
**L'Atelier.** Tout le code a été écrit et testé dans des Notebooks. C'est parfait pour voir le résultat de chaque ligne de code instantanément (surtout pour les tableaux). 
**WordCloud**  
**Le Bonus.** Une petite librairie spécialisée pour analyser le texte. Je l'ai utilisée pour générer le nuage de mots et voir quels genres dominent le marché (Spoiler : c'est l'Action). 



## Le Problème

Actuellement, une série comme *Black Clover* peut avoir une note globale super élevée (8.1/10) juste parce qu'elle est populaire, alors qu'elle a des épisodes catastrophiques (Régularité de 3.0/10 dans mon analyse).

Mon objectif : **Créer un score qui punit l'instabilité.**


## Ma Solution (L'Algorithme)

J'ai codé une formule pondérée sur Python pour re-noter 59 animés. Voici la recette exacte que j'ai utilisée :

$$Score = (0.5 \times Note\ Globale) + (0.4 \times Régularité) + (0.1 \times Bonus\ Fini)$$

* **50% Note Globale** : Je respecte quand même l'avis des fans.
* **40% Régularité** : C'est le cœur du système. Je calcule l'écart-type entre le meilleur et le pire épisode. Si c'est les montagnes russes, la note chute.
* **10% Statut "Fini"** : Un petit bonus pour récompenser les histoires qui ont une vraie fin (contrairement aux séries en pause éternelle).

###  Le Détail des Calculs (Sous le capot)

Pour ceux qui veulent comprendre la logique technique, voici comment j'ai construit mes indicateurs clés dans le script Python :

**1. Calcul de la Régularité**
J'ai d'abord calculé l'écart brut entre le meilleur et le pire épisode.
 
 $$Ecart = Note_Meilleur_Ep - Note_Pire_Ep$$

Ensuite, j'ai transformé cet écart en une note positive sur 10.

$$Régularité = 10 - Ecart$$

> *Exemple : Si l'écart est de 0 (parfait), la régularité est de 10/10. Si l'écart est énorme (9 points), la régularité chute à 1/10.*

**2. Détection de la "Hype" (Surcotage)**
Je compare la note globale (réputation) avec la moyenne réelle des épisodes extrêmes.
 
 $$Différence_Hype = Note_Globale - ({Note_Meilleur_Ep + Note_Pire_Ep}/2)$$

> *Si ce chiffre est élevé (> 1.0), cela signifie que l'animé est "surcoté" par la réputation par rapport à sa qualité technique réelle.*

**3. Normalisation (Logarithme)**
Pour comparer équitablement des séries de 12 épisodes avec des monstres comme One Piece, j'utilise le logarithme népérien sur le nombre d'épisodes pour l'affichage graphique.



##  Comment est rangé le projet ?

* `animes.csv` : Les données brutes (doublons, infos manquantes...).
* `dataset_etClassement.ipynb` : Le moteur. C'est ici que je nettoie tout et que j'applique la formule.
* `animes_calcules_complet.csv` : Le résultat final avec les nouvelles notes.
* `Rapport_etVisualisation.ipynb` : Les graphiques pour comprendre les résultats.
* `Rendu_FINAL.ipynb` : le notebook final dataset et classement + le rapport eda et les graphhiques



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
