# Widget Grist « Export contacts (.vcf) »

Génère un fichier `contacts.vcf` (vCard 3.0) à partir d'une table Grist, importable dans
Contacts (iPhone / Mac) ou sur icloud.com. Tout se passe dans le navigateur : pas de
serveur, aucune donnée modifiée, accès demandé = lecture de la table seulement.

## Installation

Rien à installer ni à copier : il suffit de coller un lien dans Grist.

1. Dans le document Grist : **Ajouter un widget** → **Personnalisé** → table des contacts.
2. Dans le panneau de droite, choisir **URL personnalisée** et coller :
   `https://vctrio.github.io/grist-widget-export-vcf/`
3. Accorder l'accès **« Lire la table sélectionnée »**.
4. Associer les colonnes. Seul **Nom** est obligatoire (y mettre la colonne « nom complet »
   si la table n'a pas de colonne prénom séparée). Téléphones et emails acceptent
   plusieurs colonnes.

Le widget se met à jour automatiquement quand une nouvelle version est publiée ici.

## Utilisation

- **Télécharger les contacts** : exporte tous les contacts sélectionnés (voir filtre ci-dessous).
- **Télécharger le contact sélectionné** : exporte la ligne où se trouve le curseur.
- Les contacts sans téléphone ni email sont signalés (et exportés quand même) ; les
  lignes totalement vides sont ignorées.

Import sur iPhone : ouvrir le `.vcf` (AirDrop, Mail, Fichiers) → « Ajouter tous les
contacts ». Ou sur icloud.com → Contacts → ⚙︎ → Importer une vCard.

## Exporter une partie des contacts (filtre intégré)

1. Dans le panneau de configuration du widget, associer une colonne au champ
   **Critère de filtre** (catégorie, statut, groupe… n'importe quelle colonne).
2. Le widget affiche une case à cocher par valeur, avec le nombre de contacts, plus une
   case « (vide) » pour les contacts sans valeur. Tout est coché par défaut.
3. Décocher / cocher les valeurs voulues (boutons « Tout cocher / Tout décocher ») : le
   compteur indique « X contacts sélectionnés sur Y », puis Télécharger.

- Colonne Liste de choix (plusieurs valeurs par contact) : le contact est retenu dès
  qu'une de ses valeurs est cochée. Dans une colonne texte, les valeurs séparées par `;`
  ou un retour à la ligne sont traitées séparément.
- Pour changer de critère : associer une autre colonne au champ.
- Limites : un seul critère à la fois ; les cases se recochent au rechargement de la page.
- Relier le widget à une autre vue filtrée de la même table ne transmet **pas** les filtres
  (seule la ligne sélectionnée est synchronisée) : utiliser ce filtre intégré.

## Bon à savoir

- Plusieurs valeurs dans une même cellule sont séparées si elles le sont par `;` `,` `/`
  ou un retour à la ligne.
- Téléphone stocké en nombre : le 0 initial perdu est rétabli pour les numéros à 9 chiffres.
- Colonne de type Référence : associer plutôt une colonne formule qui affiche le texte
  (ex. `$Organisme.Nom`), sinon c'est l'identifiant technique qui sort.
- Réimporter le même fichier crée des doublons dans Contacts (pas de fusion automatique).
- Pour ajouter un champ : `FIELDS` (mapping) → `readContact()` → `buildVCard()`.

## Pistes V2

Photo (pièce jointe Grist → PHOTO en base64, nécessite un accès aux pièces jointes),
groupes/catégories, type d'adresse configurable.

## Dépendances

- API officielle des widgets Grist (`grist-plugin-api.js`).
- [Pico CSS](https://picocss.com) v2 (licence MIT), chargé depuis jsDelivr, pour l'interface.

## Licence

MIT — voir le fichier [LICENSE](LICENSE).
