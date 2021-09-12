# LAB 2
## _Les points à voir :_

- Utilisation des directives
- Les classes avec TypeScript (DTO)
- Mise en relation entre deux composants (Parent et fils)
- Partage des données entre le fils et le parent avec @Input et @Output 
<br/>

## _prérequis :_

- Récuperer le code du LAB1 (https://github.com/ziedzayani17/angular-formation-lab1.git)
<br/>
<br/>

### I. Régrouper les attributs d'un film dans une classe *Movie*
<br/>
<br/>
  
> Une bonne pratique est la séparation entre le modéle et le composant
>
>


**1. Créer un nouveau fichier *movie.dto.ts* dans le répertoire src/app/dto/ et ajouter les attributs**  

**2. Importer la classe dans *movie.component.ts* et déclarer un attribut de type *Movie* dans le composant**  

**3. Création d'un nouveau composant pour lister plusieurs Films**

**Lancer la commande:**
```sh
ng generate component movies
```


 **4. Intégrer ce composant dans *app.component.html* en utilsant le "selector"**
<br>
<br>
### II. Les directive *ngFor* et le décorateur *@Input*
<br>
<br>

**1. Déclarer une liste des movies dans *MoviesComponent*, initialiser la liste dans le constructeur**

**2. Utiliser le directive *ngFor* et le décorateur *@Input* pour afficher une liste de "*MovieComponent*"**
<br/>

> Ajoute *"strictPropertyInitialization": false* dans *compilerOption* dans le fichier *tsconfig.json* pour désactiver l'obligation de l'initialisation des attributs

**3. Utiliser le directive *ngIf* pour afficher ce message *Film récommandé: Ce film dépasse le score de 2000 points*** 

<br>
<br>
### III. Le décorateur *@Output*
<br>
<br>
Utilser le décorateur *@Output* pour envoyer des événement de composant fils vers le composant parent

**1. Déclaration EvenetEmitteur:**
```sh
@Output() readonly myFirstEventEmitter = new EventEmitter<string>();
```

**2. Création de le fonction d'envoi dans MovieComponent, lier cette fonction avec l'événement click sur le nom de film**
```sh
 sendEvent() {
    this.myFirstEventEmitter.emit(`Je suis un événement envoyer par le film :${this.movie.name}`);
  }
```

**3. Dans le composant parent parent, déclare la liste qui va stocker les événements**
```sh
items! : string[];
```

**4. Déclarer la fonction résponsable à ma réception de l'évenement**
```sh
addItem(newItem: string) {
    this.items.push(newItem);
  }
```
**5. Mise en relation entre le parent et le fils pour la gestion des événement**

>Dans *movies.component.html* ajouter *(myFirstEventEmitter)="addItem($event)"*

**6. Afficher la liste des événement *item* dans le composant parent en utilisant le directive *ngFor***

<br>
<br>
### IV. Les pipes
<br>
<br>


**1 Utiliser le pipe date pour formatter la date de sortie d'un film**
>  exemple d'utilisation datePipe : 
*{{today | date:'fullDate'}}*
*{{today | date:'yyyy-mm-dd'}}*

**2. Afficher le nom de film en majiscule avec le pipe**

**3. Formatter le score ds film avec le pipe number**

<br>
<br>
### IV. Pipe dans le code
<br>
<br>

**1. Import pipe**
```sh
import { DatePipe } from '@angular/common'
```

**2. Injecter le pipe dans le constructeur**
```sh
constructor(datePipe: DatePipe) { 
  }
```
>Le pipe doit être ajouté aux providers de ton @NgModule (ou de ton @Component)
pour pouvoir l’injecter et l’utiliser dans ton composant

**3. Ajouter le pipe dans provider**
```sh
@Component({
  selector: 'app-movie',
  templateUrl: './movie.component.html',
  styleUrls: ['./movie.component.css'],
  providers: [DatePipe]
})
```

**4. Appliquer le pipe**
Dans le constructeur ajouter : 
```sh
this.today = this.datePipe.transform( new Date(),'yyyy-MM-dd  hh:mm:ss');
```

## _Utiliser des autres pipes avec des données statique  (currency , percent )_



