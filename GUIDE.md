# Guide — site Quarto

## 1. Quarto est installé

Quarto 1.10.18 est installé dans `~/.local/opt/quarto`, avec un lien dans
`~/.local/bin/quarto`. La ligne suivante a été ajoutée à `~/.zshrc` :

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Ouvre un nouveau terminal (ou fais `source ~/.zshrc`) puis vérifie :

```bash
quarto --version
```

*Pourquoi pas Homebrew ?* `brew install --cask quarto` fonctionne aussi, mais
l'installateur `.pkg` demande ton mot de passe administrateur. Si tu préfères
cette version, lance la commande toi-même dans un terminal ; tu pourras ensuite
supprimer `~/.local/opt/quarto` et la ligne ajoutée à `~/.zshrc`.

## 2. Prévisualiser en local

Depuis le dossier du site :

```bash
quarto preview
```

Le navigateur s'ouvre sur `localhost:4200` et **se rafraîchit tout seul** à chaque
sauvegarde d'un fichier `.qmd`. C'est la boucle de travail principale : tu édites,
tu regardes, tu recommences. Aucun besoin de publier pour voir le résultat.

Pour générer le site sans le serveur de prévisualisation :

```bash
quarto render
```

Le HTML se retrouve dans `_site/` (dossier ignoré par Git, c'est normal).

## 3. Publier sur GitHub Pages

Créer un dépôt GitHub nommé `alainguay.github.io`, puis :

```bash
git init
git add .
git commit -m "Migration du site vers Quarto"
git branch -M main
git remote add origin https://github.com/TON-COMPTE/alainguay.github.io.git
git push -u origin main
```

Dans **Settings → Pages** du dépôt, choisir la branche `gh-pages` comme source.

Ensuite, deux façons de publier, au choix :

- **Manuelle** : `quarto publish gh-pages` depuis ton terminal. Simple, tu contrôles
  quand ça part.
- **Automatique** : le fichier `.github/workflows/publish.yml` déjà inclus fait le
  rendu et la publication à chaque `git push`. Tu n'as plus qu'à pousser tes
  modifications.

Commence par la méthode manuelle le temps de te familiariser ; le workflow
automatique attendra.

## 4. Ce qu'il reste à faire

Chercher `À COMPLÉTER` dans les `.qmd` — il en reste trois.

**`teaching.qmd`**
Les descriptions officielles des deux cours (ECO7036 et ECO9036) sont reprises du
répertoire UQAM. Il manque la session la plus récente et les plans de cours :
dépose les PDF dans `files/` sous les noms `eco7036-plan.pdf` et
`eco9036-plan.pdf`, puis décommente les lignes prévues.

**`working-papers.qmd`**
Co-auteurs et statut du papier sur la malédiction des ressources.

**`data.qmd`**
La page affiche pour l'instant un encadré « matériel disponible sur demande ».
Un modèle d'entrée est en commentaire dans le fichier, prêt à décommenter.

**`_quarto.yml`**
Le favicon est commenté. Dépose `files/favicon.png` (32×32 px) et décommente
la ligne si tu en veux un.

## 5. Corrections et compléments apportés

Le contenu vient du site Weebly, avec ces corrections :

| Site Weebly | Corrigé |
|---|---|
| « DissagregationMethods Based on MIDASA Regression » | Disaggregation Methods Based on MIDAS Regression |
| « Jouranl of Economic Dynamics and Control » | Journal of… |
| « Review of Economic and Dynamics » | Review of Economic Dynamics |
| « with A. ambler » | with Steve Ambler |
| « Inference Indirect and Calibration of… Model » | Indirect Inference and Calibration of… Models |
| Métadonnées SEO au nom d'Etienne Lalé sur 3 pages | métadonnées propres à chaque page |
| Lien « Published version » de *Structural Change Tests for GEL Criteria* pointant vers un DOI de *Communications in Algebra* | lien retiré, à retrouver |
| Lien « Published version » de l'article JEDC 2014 pointant vers l'article JEDC 2012 | lien corrigé, à vérifier |
| Prénoms d'auteurs en initiales | prénoms complets (meilleur pour la recherche) |
| « SVARs in the Frequency Domain », *forthcoming 2023* | Structural VAR Models in the Frequency Domain, *Journal of Econometrics* 236 (2023), article 105466, + lien vers la version publiée |
| Working paper « Non-Gaussian Factor Models via Tensor SVD », sans référence | A Spectral Framework for Non-Gaussian SVARs, CIRANO 2026s-02 (mars 2026) |
| « Dynamic Identification in VARs », TSE WP 1384 (2022) | NBER Working Paper 32598 (2024), la version courante |
| Pages Data et Teaching vides (« Click here to edit ») | descriptions officielles des cours, encadré sur la page Data |

Vérifie quand même les deux liens « Published version » signalés plus haut : j'ai
corrigé celui de 2014 d'après le numéro de volume, mais un clic de ta part vaut
mieux qu'une déduction de la mienne.

**Les PDF ne dépendent plus de Weebly.** Les 22 fichiers hébergés sur
`alainguay.weebly.com` ont été téléchargés dans `files/` sous des noms lisibles
(`svar-frequency-domain-ms.pdf` plutôt que `revision_2_ms2022134.pdf`) et tous les
liens pointent maintenant sur des chemins relatifs. Les deux CV aussi. Le site est
autonome : tu peux fermer le compte Weebly quand tu veux, plus rien n'en dépend.

## 6. Pour aller plus loin, plus tard

- **Bibliographie automatique** : Quarto peut générer la liste de publications
  depuis un `.bib` avec l'extension `quarto-ext/academicons` et un template de
  citation. Utile si tu maintiens déjà un `.bib` pour LaTeX — un seul endroit à
  mettre à jour.
- **Notebooks Python** : un fichier `.qmd` peut contenir des blocs de code Python
  exécutés au rendu. Pratique pour publier une figure ou une note méthodologique
  reproductible directement sur le site.
- **Nom de domaine** : si tu veux `alainguay.ca` plutôt que
  `alainguay.github.io`, il suffit d'acheter le domaine et d'ajouter un fichier
  `CNAME`. GitHub Pages fournit le certificat HTTPS gratuitement.
- **Garder Weebly en ligne quelque temps** : même si le nouveau site n'en dépend
  plus, laisse les deux coexister le temps que Google réindexe.
