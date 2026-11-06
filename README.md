# Boutique Diayma
## Réponses au TD

### Question 2 : projets de la solution
La solution `Diayma.sln` contient un seul projet : `Diayma` (fichier `P2FixAnAppDotNetCode\Diayma.csproj`).

### Question 3 : version du SDK .NET
Le projet cible `netcoreapp2.0` (champ `TargetFramework` du fichier `Diayma.csproj`), donc le SDK .NET Core 2.0.

### Question 4 : installation du SDK
Le SDK .NET Core 2.1.818 était déjà installé sur ma machine (commande `dotnet --list-sdks`). Il permet de compiler et d'exécuter un projet `netcoreapp2.0`, donc aucune installation supplémentaire n'a été nécessaire.

### Question 6 : 2 bugs
### Bug 1 : total du panier incorrect
- **Action** : ajouter 3 fois la Clé USB (1 000,00 €) au panier, puis ouvrir la page Panier.
- **Attendu** : Total = 3 000,00 €. Le résumé en haut de page affiche aussi 3 000,00 €.
- **Obtenu** : Total = 1 000,00 € (la ligne du sous-total affiche bien 3 000,00 €).
  Le résumé en haut affiche « 3 item(s) 1 000,00 € ».
- **Cause probable** : le calcul du total n'utilise pas la quantité de chaque ligne.

### Bug 2 : message d'erreur non traduit (CartEmpty)
- **Action** : avec un panier vide, cliquer sur « Passer la commande », remplir le formulaire
  (Test / Rue 1 / Dakar / Sénégal), puis cliquer sur « Terminer la commande ».
- **Attendu** : un message lisible, par exemple « Votre panier est vide ».
- **Obtenu** : le texte brut `CartEmpty` s'affiche en rouge au-dessus du formulaire.
  Le formulaire de commande s'ouvre aussi alors que le panier est vide.
- **Cause probable** : la clé `CartEmpty` n'a pas de texte associé dans les fichiers
  de ressources de la langue en cours.

  ## Question 8 : Parcours du code avant l'affichage des produits

Points d'arrêt posés : CartSummaryViewComponent (l.12), ProductController (l.15),
OrderController (l.17), CartController (l.15), Startup (l.20).

| # | Namespace | Classe | Méthode | Ligne | Mode utilisé |
|---|-----------|--------|---------|-------|--------------|
| 1 | P2FixAnAppDotNetCode | Startup | Startup(IConfiguration) | 20 | F5 (continuer) |
| 2 | P2FixAnAppDotNetCode.Controllers | ProductController | ProductController(IProductService, ILanguageService) | 15 | F10 |
| 3 | P2FixAnAppDotNetCode.Controllers | ProductController | Index() | 21 | F11 |
| 4 | P2FixAnAppDotNetCode.Models.Services | ProductService | GetAllProducts() | 25 à 29 | F10 puis F11 |
| 5 | P2FixAnAppDotNetCode.Models.Repositories | ProductRepository | GetAllProducts() | 42 à 45 | F10 |
| 6 | P2FixAnAppDotNetCode.Models.Services | ProductService | GetAllProducts() (retour, ToList) | 29 | F10 |
| 7 | P2FixAnAppDotNetCode.Controllers | ProductController | Index() (retour) | 21 puis 22 | Maj+F11 puis F10 |
| 8 | P2FixAnAppDotNetCode.Components | CartSummaryViewComponent | CartSummaryViewComponent(ICart) | 12 | F5 (continuer) |

### Choix des modes
- **Pas à pas détaillé (F11)** : pour entrer dans `GetAllProducts()` et voir ce que
  fait le service, puis le repository.
- **Pas à pas principal (F10)** : pour avancer ligne par ligne sans entrer dans le
  code interne de .NET (LINQ : Where, OrderBy, ToList).
- **Pas à pas sortant (Maj+F11)** : pour quitter `ProductService` et remonter dans
  `ProductController.Index()` une fois son rôle compris.

### Résumé du déroulement
L'application démarre (`Startup`). La requête `GET /` crée `ProductController`, qui appelle
`Index()`. Celle-ci demande les produits à `ProductService`, qui interroge
`ProductRepository`. Le repository garde les produits en stock (Stock > 0), les trie par nom
et renvoie 9 produits. La liste remonte jusqu'à `Index()`, qui appelle `View(products)`.
Pendant l'affichage de la vue, le composant `CartSummaryViewComponent` est créé (résumé du
panier en haut de la page), puis la page d'accueil avec les 9 produits s'affiche.

## Question 9 : Exécutable Windows
Commande utilisée :

    dotnet publish -c Release -r win-x64 -o C:\Users\HP\Desktop\Diayma-Publish

Pour lancer l'application : dézipper le dossier, ouvrir un `cmd` dans le dossier
et taper `Diayma.exe`, puis ouvrir http://localhost:5000 dans le navigateur.
Le dossier complet est nécessaire (le .exe seul ne suffit pas).

## Question 10 : Lien de l'exécutable
https://drive.google.com/file/d/1G5PkMLXaUFjcpjxhRLpW_DzU6YMKcKtl/view?usp=sharing