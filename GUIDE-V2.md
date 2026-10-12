# Restaurant Cost Analyzer V2

Application en français sans serveur ni dépendance externe. GitHub Pages publie les fichiers à la racine de main. Le README historique est conservé.

- Tableau de bord : CA HT, achats HT, ratio achats/CA et marge sur ingrédients, filtrés par dates.
- Fournisseurs : historique des achats et agrégation HT/TVA/TTC. TVA saisie par l’utilisateur ; arrondi par ligne d’achat.
- Recettes : quantités et coûts dans la même unité, nombre de portions, prix HT, coût par portion et pourcentage de food cost.
- Ventes : quantité entière, prix HT réellement vendu et coût de recette conservé au moment de la saisie.
- Import : CSV UTF-8, point-virgule ou virgule, champs entre guillemets pris en charge. Prévisualisation puis confirmation ; toute ligne invalide bloque le lot. Les imports ajoutent des données et ne dédupliquent pas les transactions.

## Sauvegarde
Les données restent dans localStorage, pour le navigateur et l’adresse du site utilisés. Pas de synchronisation entre appareils. Exportez le JSON régulièrement et avant d’effacer le navigateur. Une restauration JSON V2 vérifiée remplace la totalité des données après confirmation. Les CSV exportés permettent la reprise des achats et ventes ; la sauvegarde JSON préserve les coûts historiques et les recettes.

## CSV
Achats : `date;fournisseur;libelle;ht;tva`

Ventes : `date;recette;quantite;prix_ht` (recette déjà créée, nom exact et unique).

Date : AAAA-MM-JJ. Exemple montant français : `120,50` avec séparateur point-virgule. Taille maximale : 5 Mo.

## Limites des indicateurs
Ratio achats/CA : pas un coût consommé réel sans inventaire des stocks. Marge sur ingrédients : hors personnel, charges, déchets et autres coûts. Les données de la V1 n’étaient pas sauvegardées et ne sont donc pas migrées.

## Vérification
`node tests.cjs` vérifie calculs, dates, validation CSV et intégrité des sauvegardes. Servir le dossier avec un serveur HTTP local pour les tests d’interface.
