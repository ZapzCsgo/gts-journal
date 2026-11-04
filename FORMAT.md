# Format d'un article

## index.json (racine)

```json
{
  "posts": [
    { "date": "2026-10-29", "title": "Titre en français", "category": "culture", "cover": "cover.webp" }
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
    {
      "file": "cover.webp",
      "alt": "Description de la photo en français",
      "caption": "Légende courte en français",
      "credit": "Photo : Cabinet Office du Japon (内閣府) / CC BY 4.0",
      "source": {
        "url": "https://commons.wikimedia.org/wiki/File:Order_of_Culture.png",
        "originalUrl": "https://upload.wikimedia.org/wikipedia/commons/7/72/Order_of_Culture.png",
        "origin": "内閣府, via Wikimedia Commons",
        "author": "内閣府 (Cabinet Office du Japon)",
        "license": "CC BY 4.0",
        "licenseUrl": "https://creativecommons.org/licenses/by/4.0/"
      }
    },
    { "file": "chiffres.svg", "alt": "Schéma des chiffres clés…", "caption": "Légende courte" }
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
- **Images** : 1 à 3 par article.
  - **La une (`images[0]`, aussi `cover` de l'index) est une VRAIE photo** liée au sujet, jamais un dessin généré ni un clipart. Sources autorisées, dans cet ordre :
    1. sites du gouvernement japonais, ministères et agences (`*.go.jp`, 政府標準利用規約, compatible CC BY 4.0, crédit obligatoire, ex. « Photo : Cabinet Office du Japon (内閣府) / CC BY 4.0 ») ;
    2. Wikimedia Commons, licence libre seulement (CC0, domaine public, CC BY, CC BY-SA) : lire la licence et l'auteur sur la page `File:` ;
    3. photos officielles de presse mises à disposition pour diffusion par l'entreprise ou l'organisateur concerné (espace presse, PR TIMES), avec la mention demandée ;
    4. Unsplash ou Pexels (licence du site, crédit de courtoisie au photographe).
  - **Interdit** : photos d'agences et de journaux (Kyodo, Jiji, AFP, Reuters, AP, NHK, Asahi, Yomiuri, Mainichi, Nikkei, Sankei, TBS…, Getty, Aflo), `og:image` des articles de presse, images trouvées sans licence claire, images générées par IA.
  - **Repli** si aucune photo libre du fait lui-même : une photo libre (Wikimedia Commons de préférence) du lieu, de l'objet ou du thème (le palais impérial, une rue de Shibuya, un érable givré, un kit de secours…). Jamais d'image d'agence, jamais de dessin à la place.
  - **Format de la une** : WebP, 16:9 exact (1600×900 de préférence, 1280×720 au minimum), recadrage propre sur le sujet (rien d'important coupé), aucun texte ajouté par-dessus, **moins de 200 Ko**.
  - **Crédit** : champ `credit` (court, affiché discrètement sous l'image : « Photo : Auteur / Licence ») et objet `source` (`url` = page d'origine de l'image, `originalUrl` = fichier d'origine, `origin`, `author`, `license`, `licenseUrl`), obligatoires pour toute photo. Pour CC0 / domaine public, le crédit reste mis par courtoisie. CC BY-SA : notre recadrage reste sous la même licence.
  - **Registre** : chaque photo est aussi ajoutée EN TÊTE de `credits-images.json` (racine) : `date`, `file`, `credit`, `sourcePage`, `originalUrl`, `origin`, `author`, `license`, `licenseUrl`, `modifications`. On n'y supprime jamais rien.
  - Images suivantes (`images[1..]`, facultatives) : schémas ou chiffres clés en SVG, ou une autre photo selon les mêmes règles.
  - Moins de 300 Ko chacune (200 Ko pour la une). `alt` est obligatoire et décrit vraiment l'image.
- **Ton** : fun et bienveillant, comme un petit journal d'école. Pas de sujet violent ou choquant (pas de crime, d'accident mortel, de guerre ni de polémique politique clivante). S'il n'y a que ça, prendre une actualité culture, société ou insolite.
- **Texte français** : pas de tiret cadratin (—).
- Chaque article cite au moins une source réelle (`sources`).
