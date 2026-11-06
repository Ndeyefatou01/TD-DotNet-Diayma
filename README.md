# Boutique Diayma
## Réponses au TD

### Question 2 : projets de la solution
La solution `Diayma.sln` contient un seul projet : `Diayma` (fichier `P2FixAnAppDotNetCode\Diayma.csproj`).

### Question 3 : version du SDK .NET
Le projet cible `netcoreapp2.0` (champ `TargetFramework` du fichier `Diayma.csproj`), donc le SDK .NET Core 2.0.

### Question 4 : installation du SDK
Le SDK .NET Core 2.1.818 était déjà installé sur ma machine (commande `dotnet --list-sdks`). Il permet de compiler et d'exécuter un projet `netcoreapp2.0`, donc aucune installation supplémentaire n'a été nécessaire.

### Question 5 : 2 bugs
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