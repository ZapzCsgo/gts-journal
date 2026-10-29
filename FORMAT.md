# Format d'un article

## index.json (racine)

```json
{
  "posts": [
    { "date": "2026-10-29", "title": "Titre en français", "category": "culture", "cover": "cover.svg" }
  ]
}
```

- Le plus récent en premier. On ajoute en tête, on ne supprime jamais.
- `category` : `societe` | `culture` | `tech` | `sport` | `economie` | `meteo` | `insolite` | `politique`.
- `cover` : le nom d'un fichier du dossier de l'article.

## posts/AAAA-MM-JJ/post.json

`AAAA-MM-JJ` est la date de publication. L'actualité racontée est celle de la veille.

```json
{
  "date": "2026-10-29",
  "newsDate": "2026-10-28",
  "category": "culture",
  "title": "Titre accrocheur en français",
  "summary": { "fr": "Résumé en 2 phrases.", "en": "2-sentence summary." },
  "sources": [{ "name": "NHK News Web Easy", "url": "https://..." }],
  "images": [
    { "file": "cover.svg", "alt": "Description de l'image en français", "caption": "Légende courte en français" }
  ],
  "levels": {
    "N5": {
      "title": "{京都|きょうと}で…",
      "paragraphs": ["…", "…"],
      "vocab": [{ "word": "{紅葉|こうよう}", "meaning": { "fr": "feuilles d'automne", "en": "autumn leaves" } }],
      "quiz": [{ "question": "…", "choices": ["…", "…", "…"], "answer": 0, "explain": { "fr": "…", "en": "…" } }]
    },
    "N4": { "…": "même forme" },
    "N3": { "…": "même forme" },
    "N2": { "…": "même forme" },
    "N1": { "…": "même forme" }
  }
}
```

## Règles

- **Les 5 niveaux sont obligatoires**, et chacun est vraiment écrit à son niveau (grammaire et vocabulaire du JLPT correspondant), pas une simple coupe du même texte.
  - N5 : 3 à 5 phrases courtes, forme です/ます, kanji N5 seulement.
  - N4 : 5 à 7 phrases.
  - N3 : 2 paragraphes.
  - N2 : 3 paragraphes.
  - N1 : 3 à 4 paragraphes, ton de presse.
- **Furigana** : `{漢字|よみ}` sur chaque kanji au-dessus du niveau choisi (en N5, sur tous les kanji). Le site affiche ou masque les furigana selon le réglage de l'élève.
- **Vocabulaire** : 5 à 8 mots clés par niveau.
- **Quiz** : 3 questions de compréhension par niveau. `answer` est l'index (à partir de 0) de la bonne réponse.
- **Images** : 1 à 3 par article. Ce sont des illustrations ou des schémas qui montrent les faits (carte, chiffre clé, petite scène), en SVG de préférence, sinon WebP ou PNG.
  - Moins de 300 Ko chacune.
  - **Jamais de photo de presse ni d'image copiée d'un site** (droits d'auteur).
  - `alt` est obligatoire.
- **Ton** : fun et bienveillant, comme un petit journal d'école. Pas de sujet violent ou choquant (pas de crime, d'accident mortel, de guerre ni de polémique politique clivante). S'il n'y a que ça, prendre une actualité culture, société ou insolite.
- **Texte français** : pas de tiret cadratin (—).
- Chaque article cite au moins une source réelle (`sources`).
