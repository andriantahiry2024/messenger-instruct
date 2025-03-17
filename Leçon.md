# Leçons apprises lors du développement de l'application Messenger Clone

## Leçons techniques

### Next.js
1. **Directive 'use client'** : Toujours ajouter la directive `'use client'` au début des fichiers qui utilisent des hooks React (useState, useEffect, createContext, etc.) ou des fonctionnalités spécifiques au client dans Next.js.

2. **Métadonnées** : Ne jamais exporter des métadonnées depuis un composant marqué avec `'use client'`. Créer plutôt un fichier séparé pour les métadonnées.

3. **Structure des composants** : Séparer clairement les composants client des composants serveur pour éviter les erreurs de compilation.

4. **Problème de providers dans Next.js App Router** : Dans l'architecture App Router de Next.js, les providers de contexte doivent être encapsulés dans un composant client (`'use client'`) séparé qui sera ensuite importé dans le fichier layout racine. Ne pas mettre les providers directement dans le layout.

5. **Chemins d'importation** : Si l'alias `@` n'a pas été configuré lors de l'installation de Next.js, utiliser des chemins relatifs (`./` ou `../`) pour les importations. Éviter d'utiliser `@/` qui nécessite une configuration particulière dans tsconfig.json ou jsconfig.json.

6. **Hydration** : Les erreurs d'hydratation se produisent lorsque le HTML généré côté serveur ne correspond pas à ce que React essaie de rendre côté client. Pour résoudre ce problème, utiliser un montage différé avec un état `mounted` et `useEffect`, et ajouter l'attribut `suppressHydrationWarning` à l'élément HTML. Éviter d'utiliser des valeurs variables comme `Date.now()` ou `Math.random()` lors du rendu initial.

### Tailwind CSS
1. **Configuration personnalisée** : Toujours créer un fichier `tailwind.config.js` complet lorsque des classes personnalisées sont utilisées.

2. **Classes personnalisées** : Vérifier que toutes les classes utilisées dans le code sont définies dans la configuration Tailwind. Les classes comme `border-border` nécessitent une définition dans le thème.

3. **Thème sombre** : Configurer correctement les variantes sombres avec la syntaxe `dark:` et s'assurer que le mode sombre est activé dans la configuration.

4. **Classes standard** : Utiliser les classes Tailwind standard comme `border-gray-300` au lieu de `border-gray-200` si elles ne sont pas explicitement définies dans la configuration. Vérifier que les classes de couleur utilisées font partie des couleurs standard de Tailwind ou sont définies dans le thème personnalisé.

5. **Définition explicite des couleurs** : Même les couleurs standard de Tailwind comme `gray-300` doivent être explicitement définies dans le thème si la configuration utilise un thème personnalisé qui remplace les valeurs par défaut. Toujours définir toutes les couleurs utilisées dans le fichier `tailwind.config.js`.

6. **Préférer les classes standard aux classes personnalisées** : Même si des classes personnalisées comme `border-border` sont définies dans la configuration, il est parfois préférable d'utiliser des classes standard comme `border-gray-200` pour éviter des problèmes de compilation, surtout si la configuration personnalisée n'est pas correctement chargée.

7. **Utilisation de safelist** : Pour s'assurer que certaines classes Tailwind sont toujours disponibles même si elles ne sont pas directement utilisées dans le code, les ajouter à la `safelist` dans la configuration Tailwind.

8. **Simplification des classes** : En cas de problèmes récurrents avec des classes de couleur spécifiques, utiliser des classes plus simples comme `border-0` au lieu de classes avec des couleurs spécifiques.

9. **Éviter les classes personnalisées pour les cas d'utilisation courants** : Pour les éléments de base comme `bg-background` ou `text-foreground`, utiliser directement des classes standards comme `bg-white dark:bg-gray-900` et `text-gray-900 dark:text-gray-100` pour éviter les problèmes de compilation et améliorer la compatibilité.

10. **Safelist exhaustive** : En cas de problèmes persistants, créer une safelist exhaustive qui inclut toutes les classes utilisées dans l'application, organisées par catégorie (bordures, textes, backgrounds, etc.) pour garantir qu'aucune classe ne sera ignorée par le compilateur.

11. **Conversion en CSS vanilla pour les composants problématiques** : En dernier recours, si les problèmes avec Tailwind persistent malgré les solutions ci-dessus, convertir les définitions de style en CSS vanilla standard. Les classes personnalisées peuvent rester dans l'approche CSS-in-JS, mais sans utiliser la syntaxe @apply de Tailwind.

12. **Réduction de la complexité de la configuration Tailwind** : Si de nombreux problèmes surviennent, simplifier considérablement la configuration Tailwind en ne gardant que les fonctionnalités essentielles et en évitant les thèmes et couleurs personnalisés.

13. **Ne jamais utiliser @apply avec des classes non définies** : La directive `@apply border-border` ne fonctionnera pas si `border-border` n'est pas explicitement défini dans la configuration Tailwind. Éviter d'utiliser `@layer base` avec des classes personnalisées non définies.

14. **Styles personnalisés conventionnels** : Pour améliorer le design d'une interface, créer des classes CSS personnalisées avec des noms descriptifs (comme `.auth-container`, `.auth-title`, etc.) et les appliquer dans les composants React plutôt que d'utiliser uniquement des classes utilitaires Tailwind.

### Axios
1. **Types d'intercepteurs** : Utiliser `InternalAxiosRequestConfig` au lieu de `AxiosRequestConfig` pour les intercepteurs de requête dans les versions récentes d'Axios.

2. **Gestion des erreurs** : Implémenter des intercepteurs de réponse pour gérer les erreurs de manière cohérente.

### Socket.IO
1. **Initialisation** : Initialiser Socket.IO après l'authentification pour garantir que les connexions sont authentifiées.

2. **Nettoyage** : Toujours nettoyer les écouteurs d'événements Socket.IO dans le hook useEffect pour éviter les fuites de mémoire.

### PowerShell
1. **Opérateurs de chaînage** : Dans PowerShell, utiliser le point-virgule `;` au lieu de `&&` pour chaîner les commandes. Par exemple, `cd dossier ; npm run dev` au lieu de `cd dossier && npm run dev`.

## Bonnes pratiques

1. **Vérification du répertoire** : Toujours vérifier le répertoire courant avant d'exécuter des commandes npm ou autres commandes de terminal.

2. **Gestion des erreurs** : Implémenter une gestion des erreurs robuste avec des messages d'erreur clairs pour faciliter le débogage.

3. **Tests progressifs** : Tester chaque fonctionnalité individuellement avant de les intégrer ensemble pour identifier rapidement les problèmes.

4. **Documentation** : Maintenir une documentation à jour des erreurs rencontrées et des solutions appliquées pour référence future.

5. **Approche hybride CSS/Tailwind** : Lorsque des problèmes récurrents surviennent avec des frameworks CSS comme Tailwind, envisager une approche hybride qui utilise CSS vanilla pour les composants de base et Tailwind pour les utilitaires moins problématiques.

6. **Conception responsive** : Assurer que l'interface utilisateur s'adapte correctement à différentes tailles d'écran en utilisant des conteneurs responsives et des médias queries.

7. **Expérience utilisateur** : Soigner l'apparence visuelle de l'application en utilisant des effets subtils (ombres, transitions, animations) pour améliorer l'expérience utilisateur.

## Erreurs spécifiques et solutions

1. **Erreur de classe Tailwind `border-border`** :
   - Erreur : La classe `border-border` n'était pas définie dans la configuration Tailwind.
   - Solution : Création du fichier `tailwind.config.js` avec les définitions de couleurs personnalisées et modification de `globals.css` pour utiliser des classes standard (`border-gray-200 dark:border-gray-700`).

2. **Erreur de classe Tailwind `border-gray-200`** :
   - Erreur : La classe `border-gray-200` n'était pas reconnue par Tailwind.
   - Solution : Remplacement par `border-gray-300` qui est une classe standard de Tailwind et déjà utilisée ailleurs dans l'application.

3. **Erreur de classe Tailwind `border-gray-300`** :
   - Erreur : La classe `border-gray-300` n'était pas reconnue par Tailwind malgré son statut de classe standard.
   - Solution : Ajout explicite de la palette de couleurs `gray` dans le fichier `tailwind.config.js` et utilisation de la classe `border-border` qui était déjà définie dans la configuration.

4. **Erreur de classe Tailwind `border-border` (après ajout des couleurs)** :
   - Erreur : Même après avoir défini les couleurs gray, la classe `border-border` n'était toujours pas reconnue.
   - Solution : Revenir à l'utilisation de la classe standard `border-gray-200` qui est maintenant correctement définie dans la configuration.

5. **Erreurs persistantes de classes de bordure** :
   - Erreur : Malgré nos tentatives, les erreurs de classe Tailwind pour les bordures persistent.
   - Solution : Simplification radicale en utilisant `border-0` au lieu de classes avec des couleurs, et ajout d'une `safelist` dans `tailwind.config.js` pour s'assurer que les classes de bordure sont toujours disponibles, et définition explicite de toutes les couleurs utilisées.

6. **Erreur de classe Tailwind `bg-background`** :
   - Erreur : La classe personnalisée `bg-background` n'est pas reconnue malgré sa définition dans la configuration.
   - Solution : Remplacement par des classes standards `bg-white dark:bg-gray-900` et extension de la safelist pour inclure toutes les classes utilisées dans l'application.

7. **Erreur de classe Tailwind `bg-white`** :
   - Erreur : Même après avoir défini explicitement `white` dans les couleurs et l'avoir ajouté à la safelist, la classe n'est toujours pas reconnue.
   - Solution : Conversion complète des styles Tailwind en CSS vanilla dans `globals.css` et simplification drastique de la configuration Tailwind.

8. **Erreur d'exécution npm dans le mauvais répertoire** :
   - Erreur : Tentative d'exécution de `npm run dev` dans le répertoire racine au lieu du répertoire client.
   - Solution : Navigation vers le bon répertoire (`cd messenger-clone/client`) avant d'exécuter la commande.

9. **Erreur de syntaxe PowerShell** :
   - Erreur : Utilisation de `&&` pour chaîner les commandes dans PowerShell, ce qui n'est pas supporté.
   - Solution : Utilisation du point-virgule `;` pour chaîner les commandes, par exemple `cd messenger-clone/client ; npm run dev`.

10. **Erreur de directive 'use client'** :
    - Erreur : Les composants utilisant des hooks React nécessitent la directive 'use client'.
    - Solution : Ajout de la directive au début des fichiers concernés.

11. **Erreur de type Axios** :
    - Erreur : Les types AxiosRequestConfig ne sont plus compatibles avec les intercepteurs.
    - Solution : Utilisation de InternalAxiosRequestConfig pour les intercepteurs.

12. **Erreur d'exportation de métadonnées** :
    - Erreur : Next.js ne permet pas d'exporter des métadonnées depuis un composant client.
    - Solution : Déplacement des métadonnées dans un fichier séparé.

13. **Erreur 'useAuth doit être utilisé à l'intérieur d'un AuthProvider'** :
    - Erreur : Le hook useAuth est appelé dans un composant mais le AuthProvider n'est pas correctement initialisé.
    - Solution : Création d'un composant `ClientProvider.tsx` avec la directive 'use client' qui encapsule les providers (AuthProvider et ConversationProvider) et utilisation de ce composant dans le layout principal au lieu d'appliquer directement les providers. Cela garantit que les contextes sont correctement initialisés dans un environnement client.

14. **Erreur d'hydratation** :
    - Erreur : "Hydration failed because the server rendered HTML didn't match the client."
    - Solution : 
      1. Ajouter l'attribut `suppressHydrationWarning` à l'élément HTML racine.
      2. Utiliser un état `mounted` avec `useEffect` pour différer le rendu jusqu'à ce que le composant soit monté côté client.
      3. Afficher un placeholder ou retourner null pendant le chargement initial.
      4. Éviter les fonctions générant des valeurs aléatoires ou dépendantes du contexte lors du rendu initial.
      5. S'assurer que le formatage des dates est identique côté serveur et client. 