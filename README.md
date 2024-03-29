##LIEN TP
https://github.com/l3-miage-cl-ihm/e-s-de-composants-angular-tu-2023-2024-l3miage-osmanm
https://github.com/l3-miage-cl-ihm/gestion-de-matrices-l3-miage-2023-2024-l3miage-osmanm
https://github.com/l3-miage-cl-ihm/todolist-en-angular-rxjs-l3miage-osmanm
https://github.com/l3-miage-cl-ihm/reversi-en-angular-l3miage-osmanm


[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=13712203&assignment_repo_type=AssignmentRepo)
# L3 Miage - TP signaux

## Configuration de votre github

Nous allons configurer votre github pour lui faire générer le site correspondant à votre projet.
Pour cela, nous nous appuierons sur les github pages et les github actions. 
A chaque fois que vous pousserez une nouvelle version de votre code sur le dépôt, il sera compilé via une github action et le résultat de la compilation sera mis en ligne sur github pages.

Rendez-vous à l'adresse de votre dépôt github, puis cliquez sur le bouton `Settings` en haut à droite.
Dans le menu à gauche, cliquez sur `Pages`, puis configurer comme suit :

* Source : `Deploy from a branch`
* Branch : `gh-pages`  /  `root`
* Puis cliquez sur `Save`

## Configuration du fichier package.json

Modifier le script associé à la commande `build`, remplacez `l3m-tp-signals-2023-2024` par le nom de votre dépôt (devrait être de la forme `l3m-tp-signals-2023-2024-GITHUBID` avec `GITHUBID` votre identifiant github).

Cette configuration est nécessaire pour que l'application puisse fonctionner une fois déployer sur votre github pages.

## Le sujet

Vous allez mettre en oeuvre des signaux dans le cadre d'une application Angular.
Il n'est pas nécessaire de connaitre Angular pour faire ce TP, cependant vous verrez un peu de syntaxe Angular, ne vous affolez pas, vous n'en avez pas besoin pour réaliser ce TP.

Vous devrez éditer un seul fichier : **`src/app/app.component.ts`**.

Dans ce fichier, vous trouverez une classe `AppComponent` qui contient des méthodes `question01`, `question02`, etc.
Ce sont ces méthodes qu'il vous faudra compléter. Chaque méthode est précédé par un commentaire qui explique ce qui est attendu.

### Important

Lorsque vous modifierez des signaux primaires dans le code, faite le en passant par la méthode `this.ds.process`.
En effet, afin de laisser le temps aux signaux de se propager, nous avons mis en place cette méthode qui temporise l'exécution des modifications. Sans cela, toutes les modifications seraient prises en compte instantanément et la valeur des signaux ne serait liée qu'aux dernières valeurs affectées aux signaux primaires.

Par exemple, si vous avez un signal primaire a qui produit des nombres, alors vous pourrez le modifier comme suit :

```typescript
this.ds.process(
    () => a.set(2) , // Une première demande de modification
    () => a.set(10), // Une deuxième demande de modification
    () => a.set(20)  // etc.
);
```

##EXEMPLE PROMESSE
1 son apres l autre 

function jouerSon(url: string, cb: () => void): void { 

    console.log(`Début de la lecture du son ${url}`); 

    setTimeout(() => { 

        console.log(`Fin de la lecture du son ${url}`); 

        cb(); // Signale la fin de la lecture du son actuel 

    }, 500 + Math.random() * 1000); // Durée simulée de la lecture 

} 

  

function jouerListeSonsSeq(urls: string[], cb: () => void): void { 

    let index = 0; // Pour suivre l'index du son en cours de lecture 

  

    // Fonction récursive pour jouer le son à l'index actuel 

    const jouerSuivant = () => { 

        if (index < urls.length) { 

            jouerSon(urls[index], () => { 

                index++; // Préparer l'index pour le prochain son 

                jouerSuivant(); // Récursion pour passer au son suivant 

            }); 

        } else { 

            cb(); // Tous les sons ont été joués, appeler le callback final 

        } 

    }; 

  

    jouerSuivant(); // Commencer à jouer depuis le premier son 

} 

  

// Exemple d'utilisation 

const urls = ['son1.mp3', 'son2.mp3', 'son3.mp3']; 

jouerListeSonsSeq(urls, () => { 

    console.log('Tous les sons ont été joués !'); 

}); 

Orchestre 

 

function jouerSon(url: string, cb: () => void): void { 

    console.log(`Début de la lecture du son ${url}`); 

    setTimeout(() => { 

        console.log(`Fin de la lecture du son ${url}`); 

        cb(); // Signale la fin de la lecture du son actuel 

    }, 500 + Math.random() * 1000); // Durée simulée de la lecture 

} 

  

function jouerListeSonsSimultanément(urls: string[], cb: () => void): void { 

    if (urls.length === 0) { 

        cb(); // Si la liste est vide, on appelle le callback directement 

        return; 

    } 

  

    let sonsTerminés = 0; // Compteur pour suivre le nombre de sons terminés 

  

    // Fonction de callback interne pour un seul son 

    const sonTerminé = () => { 

        sonsTerminés++; // Incrémenter le compteur à chaque fin de son 

        if (sonsTerminés === urls.length) { 

            cb(); // Si tous les sons sont terminés, appeler le callback final 

        } 

    }; 

  

    // Jouer tous les sons en parallèle 

    urls.forEach((url) => { 

        jouerSon(url, sonTerminé); 

    }); 

} 

  

// Exemple d'utilisation 

const urls = ['tuba.mp3', 'piano.mp3', 'violons.mp3']; 

jouerListeSonsSimultanément(urls, () => { 

    console.log('Tous les sons ont été joués en parallèle !'); 

}); 
