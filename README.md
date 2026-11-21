# LeSacAOrdo IDE

© 2026 LESACA Julien — Tous droits réservés.

_Prescriptions infirmières & courriers — avec gestion du remplacement_

Application web installable (PWA), dérivée de LeSacAOrdo (Ordonnancev5), pour
rédiger des **ordonnances infirmières** et des **courriers simples**, et les
enregistrer en PDF. Tout est calculé dans le navigateur : aucune donnée n'est
transmise.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | L'application entière : interface, modèles, mise en page A4. |
| `manifest.webmanifest` | Nom, icônes, couleurs, mode autonome. |
| `sw.js` | Service worker : fonctionnement hors connexion. |
| `icon-*.png`, `logo-lesacaordo.png` | Icônes. |
| `lib/html2canvas.min.js`, `lib/jspdf.umd.min.js` | Bibliothèques (licence MIT) qui fabriquent le PDF. |

Aucun logo institutionnel, aucune signature ni aucun numéro RPPS de tiers n'est
embarqué : chaque infirmier(ère) saisit sa propre identité.

## Ce qui change par rapport à Ordonnancev5

- **Profil de l'infirmier(ère)**, saisi une fois et conservé sur l'appareil :
  civilité (accord « infirmier / infirmière »), NOM, Prénom, **RPPS**, qualité
  imprimée, n° Assurance Maladie (facultatif), adresse professionnelle,
  téléphone, courriel, ville.
- **Signature en autonomie** : à dessiner au doigt, ou à importer depuis une
  photo (fond clair rendu transparent, recadrage automatique). Elle reste dans le
  stockage du navigateur de l'appareil ; le bouton *Effacer mon profil* la
  supprime.
- **Contrôle du RPPS** : 11 chiffres et clé de Luhn. Un numéro douteux est
  signalé, jamais bloqué.
- **Ordonnances** (une par catégorie) : produits de santé (pansements,
  dispositifs médicaux, substituts nicotiniques), vaccination, examens de
  biologie. Composeur de ligne de pansement.
- **Courrier simple** : destinataire libre (bloc d'adresse), formule d'appel,
  objet, six modèles (transmission au médecin traitant, demande de
  renouvellement, suivi de plaie, signalement, fin de prise en charge, courrier
  administratif), formule de politesse.
- **Remplacement** (voir ci-dessous).
- **Contrôle des mentions** : liste en direct de ce qui manque sur le document.
- Supprimés : en-tête SMHEP, signataires, ordonnance sécurisée, imagerie,
  kinésithérapie, certificats médicaux — hors du champ infirmier ou propres au
  service d'origine.

## Mentions imprimées sur l'ordonnance

L'article **R. 5132-3 du code de la santé publique** fixe les mentions de toute
prescription : nom, qualité, identifiant (RPPS), adresse professionnelle et
coordonnées du prescripteur, signature, date ; nom, prénoms, sexe, âge du
patient, et sa taille et son poids si nécessaire ; désignation du produit,
posologie, durée ou quantité, renouvellement éventuel.
Sources : [Légifrance, art. R. 5132-3](https://www.legifrance.gouv.fr/codes/id/LEGIARTI000006915532/2007-04-26) ;
[Vidal, règles juridiques de rédaction des ordonnances](https://www.vidal.fr/infos-pratiques/regles-generales-de-prescription-et-de-delivrance-regles-juridiques-de-redaction-des-ordonnances-id16178.html) ;
[CNOM, Gérer mes ordonnances](https://www.conseil-national.medecin.fr/medecin/exercice/gerer-ordonnances).

L'application imprime donc : identité, qualité, RPPS et coordonnées du
prescripteur ; date ; identité, date de naissance et âge (calculé à la date du
document), sexe, taille et poids facultatifs du patient ; lignes de
prescription ; renouvellement ; signature.

## Ce que l'infirmier(ère) peut prescrire

La liste réglementaire est fixée par l'**arrêté du 26 juin 2026** fixant la
liste des produits de santé et examens complémentaires que les infirmiers
diplômés d'État sont autorisés à prescrire ou à renouveler (JO du 27 juin 2026) :
[Légifrance](https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000054321926) ;
[analyse du SNPI](https://syndicat-infirmier.com/Arrete-prescription-infirmiere-26-juin-2026.html).

**Limite à connaître** : le texte intégral de l'arrêté n'a pas pu être lu lors
du développement (Légifrance refuse les accès automatisés). Les modèles de
l'application sont donc des **trames de rédaction** avec des « xx » à compléter,
**pas une liste d'autorisations**. Des sources secondaires indiquent notamment
une durée initiale de 7 jours pour les pansements et une obligation d'inscrire
la prescription au dossier patient ou au DMP ; ces points sont à vérifier dans
le texte avant usage. Les conditions propres aux vaccins (âges, déclaration
d'activité, formation) figurent en annexe de l'arrêté.

## Remplacement

Cochez *J'exerce en remplacement…* puis renseignez le titulaire : nom, prénom,
RPPS, n° Assurance Maladie, adresse et téléphone du cabinet, dates du
remplacement. Ces données sont conservées sur l'appareil pour la durée du
remplacement.

Ce qui est imprimé :

- **l'auteur réel de la prescription** : vos nom et prénom, votre qualité avec
  la mention « remplaçant(e) », **votre RPPS** (le prescripteur est celui qui
  signe ; R. 5132-3 exige son identifiant) ;
- **le cabinet du titulaire** : son nom, son RPPS et son n° Assurance Maladie,
  étiquetés comme tels, son adresse et son téléphone — coordonnées auxquelles
  le patient et le pharmacien joignent le cabinet ;
- la période de remplacement ;
- sous la signature : « Prénom NOM, infirmière remplaçante de Mme X ».

Deux présentations au choix : mentions explicites (« En remplacement de… »),
ou nom du titulaire **barré** avec votre nom à côté, qui reproduit l'usage des
ordonnances pré-imprimées : le remplaçant barre le nom du titulaire et inscrit
le sien avec sa qualité de remplaçant
([URPS Infirmière PACA](https://www.urps-infirmiere-paca.fr/tout-savoir-sur-le-remplacement/) ;
[Ordre des médecins des Yvelines, guide du remplacement](https://www.cdyom.org/wp-content/uploads/2025/04/Guide-du-remplacement-v2025.pdf)).

Le contrôle des mentions signale une **date de document hors de la période de
remplacement**.

**Point non tranché par les sources** : quel RPPS doit figurer en cas de
remplacement. Un conseil départemental de l'Ordre des médecins indique celui du
remplacé ([CDOM 49](https://conseil49.ordre.medecin.fr/formalites-avant-un-remplacement)),
d'autres sources celui de l'auteur. C'est pourquoi l'application imprime
**les deux, chacun étiqueté**. Faites valider ce choix par votre conseil
départemental de l'Ordre infirmier.

Rappels du code de déontologie (art. R. 4312-83 et suivants du CSP, à
vérifier sur Légifrance) : contrat de remplacement transmis au conseil
départemental de l'Ordre ; le titulaire cesse toute activité infirmière
pendant le remplacement, sauf urgence
([Légifrance, art. R. 4312-84](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000033495980) ;
[Ordre national des infirmiers, modèles de contrat](https://www.ordre-infirmiers.fr/faq-juridique)).

## Mise en ligne et installation

Identiques à LeSacAOrdo : déposer tous les fichiers et le dossier `lib` à la
racine d'un hébergement `https://` (GitHub Pages par exemple), ouvrir l'adresse
dans Chrome (Android) ou Safari (iOS), puis *Installer l'application* /
*Sur l'écran d'accueil*. L'application fonctionne ensuite hors connexion.

Ne déposez jamais de donnée de patient dans le dépôt.

## Enregistrer en PDF

**PDF → Enregistrer le PDF** produit `aaaammjj_ordonnance-IDE_NOM_Prenom.pdf`
(ou `_courrier_`). Le PDF contient une image de chaque page (≈ 290 ppp).
*Imprimer* reste disponible dans la même fenêtre.

## Sécurité de la signature

La signature numérisée est stockée en clair dans le navigateur de l'appareil.
Quiconque accède à l'appareil déverrouillé peut l'apposer. Verrouillez votre
téléphone ; décochez *Apposer la signature* pour signer à la main.

## Publier une mise à jour

1. Modifiez `index.html`.
2. Dans `sw.js`, incrémentez `const VERSION = 'lesacaordoide-v1';`.
3. Remplacez les deux fichiers sur l'hébergement.

## Responsabilité

Les modèles sont des trames sans posologie pré-remplie. Le contenu, sa
conformité au champ de prescription infirmier et le respect des règles du
remplacement relèvent de l'infirmier(ère) qui signe.
