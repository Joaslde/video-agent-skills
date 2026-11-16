# video-agent-skills

Des skills Claude Code gratuits pour trouver tes idées, écrire tes scripts, monter, traduire et publier tes vidéos : formats courts (Reels Instagram, TikTok, YouTube Shorts) et vidéos YouTube longues.

C'est la boîte à outils que j'utilise pour faire tourner mon compte Instagram [@joas_lde](https://www.instagram.com/joas_lde/), et que je montre dans ma série « Créer du contenu avec l'IA ».

Pas d'appli, pas de serveur, pas d'abonnement. Les skills expliquent à Claude comment travailler, et `short-editing` embarque son propre moteur de rendu (Node, Chrome, ffmpeg, et whisper.cpp pour les mots), entièrement sur ton ordinateur : macOS, Windows et Linux.

En option :
- [Treg](https://treg.to) pour auditer ton Instagram et publier sur YouTube, Instagram et TikTok ;
- une clé ElevenLabs pour traduire ;
- Codex pour générer des images.

## Par où commencer

Trois étapes jusqu'à ta première vidéo montée :

1. **Installe** les skills (voir plus bas), puis ouvre Claude Code dans le dossier de ton projet.
2. Lance **`/studio-setup`**. Il vérifie tes outils, prépare le moteur de rendu, écrit ton `voice.md` et adapte le style par défaut à toi (7 questions rapides : look, couleur, polices, sous-titres, rythme, mot à commenter sur Instagram, logos de tes outils), avec un aperçu sur tes propres images. Environ 15 minutes, une seule fois.
3. Filme une prise (téléphone, webcam ou caméra), mets-la dans `video-agent/takes/`, puis lance **`/short-editing`**. Tu récupères la vidéo montée dans `video-agent/edits/short-<slug>/output/`, avec les sous-titres en `.srt` et le texte du post.

Tu ne sais pas quel skill utiliser ? Tape `/editing <ce que tu veux>` : il choisit pour toi.

## Les skills

| Skill | À quoi il sert |
|---|---|
| `/editing` | La porte d'entrée. Dis ce que tu veux (« monte ma dernière prise », « mes scripts de la semaine », « publie-la ») : il choisit le bon skill et reprend la vidéo en cours. |
| `/studio-setup` | À lancer en premier. Installe et vérifie les outils, crée le dossier `video-agent/`, écrit ton `voice.md`, règle ton style par défaut et, si tu veux, connecte Treg, ElevenLabs et Codex. |
| `/insta-audit` | Connecte ton Instagram via Treg et l'audite : tes derniers reels avec leurs vraies stats (vues, temps de visionnage, enregistrements, partages), ce qui surperforme par rapport à ta propre médiane, les premières secondes de tes meilleurs et de tes pires reels, et les 3 changements à faire. |
| `/studio-script` | Une semaine de scripts dans ta voix : 3 hooks par script, notés, le minutage vérifié, des notes visuelles, puis un passage qui retire les tics d'IA. Aussi `viral`, `hook <sujet>` et `humanize <texte>`. |
| `/outliers` | Les reels qui ont explosé chez tes concurrents, mesurés par rapport à la médiane de leur propre compte (3 fois ou plus, reels sponsorisés exclus). Les 5 meilleurs deviennent des scripts dans ta voix. Via Treg, environ 0,001 dollar la page de reels. |
| `/short-editing` | Une prise brute devient une vidéo finie : silences coupés, sous-titres, éléments à l'écran au mot près, hook avec effets sonores, appel à commenter, voix à -14 LUFS, fichier `.srt` et texte du post. |
| `/steal` | Mesure le style de montage d'un reel (coupes, sous-titres, musique, zooms) pour l'appliquer à tes propres prises. |
| `/broll` | Range tes propres plans de coupe en bibliothèque pour que Claude retrouve le bon plan en une recherche. |
| `/clips` | Une vidéo longue (la tienne, un podcast, un live) devient plusieurs vidéos courtes montées. |
| `/short-translate` | Ta prise dans une autre langue, avec ta propre voix clonée (ElevenLabs, ta clé). |
| `/vox` | Une photo devient une animation en collage papier, façon documentaire. |
| `/codex-images` | Miniatures, couvertures et images générées avec Codex (ton abonnement ChatGPT). |
| `/publish` | Publie sur YouTube, Instagram et TikTok via Treg. Rien ne part sans ton accord. Sans Treg, il te prépare un kit prêt à poster. |

## Installation

Dans le dossier de ton projet :

```bash
npx skills add Joaslde/video-agent-skills -a claude-code
```

Ajoute `-g` pour les installer dans tous tes projets.

Ou colle `https://github.com/Joaslde/video-agent-skills` dans Claude Code et demande-lui d'installer ces skills.

Ou copie-les à la main. Windows (PowerShell) :

```powershell
git clone https://github.com/Joaslde/video-agent-skills.git
New-Item -ItemType Directory -Force .claude\skills | Out-Null
Copy-Item -Recurse -Force video-agent-skills\skills\* .claude\skills\
```

macOS et Linux :

```bash
git clone https://github.com/Joaslde/video-agent-skills.git
mkdir -p .claude/skills
cp -r video-agent-skills/skills/* .claude/skills/
```

Ensuite, dans Claude Code : `/studio-setup`.

## Le déroulé

```text
/studio-setup          une fois : outils, moteur, voice.md, ton style, comptes
/insta-audit           ce qui marche sur ton Instagram
/outliers              ce qui a explosé chez tes concurrents, et 5 scripts
/studio-script         les scripts de la semaine
                       tu filmes, tu mets les prises dans video-agent/takes/
/short-editing         chaque prise devient une vidéo montée
/publish               YouTube, Instagram, TikTok
```

## Outils

| Outil | Pour quoi | Coût |
|---|---|---|
| Node 20+, git | le moteur de rendu | gratuit |
| ffmpeg | coupes, son, conversions | gratuit |
| yt-dlp et deno | vues, sous-titres et transcriptions YouTube | gratuit |
| Chrome et whisper.cpp | le rendu et le minutage des mots (environ 0,6 Go, installés au premier montage) | gratuit |
| Treg (optionnel) | audit Instagram, publication, chiffres des autres comptes | tes propres comptes gratuits, les autres environ 0,001 dollar par appel |
| ElevenLabs (optionnel) | la traduction, avec ta clé | ton abonnement ElevenLabs |
| Codex (optionnel) | les images | ton abonnement ChatGPT |

## Limites honnêtes

- Une seule famille de mise en page, volontairement : tu changes les couleurs, les polices, les sous-titres et le son, pas la structure.
- Les sous-titres automatiques se trompent sur les noms et les chiffres. Vérifie-les.
- Sans Treg, la veille se limite à YouTube et la publication est manuelle.
- La traduction ne synchronise pas les lèvres.
- Les images générées doivent être vérifiées (le texte peut contenir des fautes).
- Ne télécharge et ne coupe que des vidéos qui t'appartiennent ou dont tu as les droits.

## Me suivre

- Instagram : [@joas_lde](https://www.instagram.com/joas_lde/)
- GitHub : [Joaslde](https://github.com/Joaslde)

## Licence

MIT, voir [LICENSE](LICENSE).
