


Je vais vous aider à créer ce projet en Angular. Nous allons générer deux nombres aléatoires entre 0 et 9, choisir un opérateur aléatoire parmi `+`, `-`, et `*`, et faire en sorte que le résultat de l'opération ne soit jamais un nombre décimal. Voici le code Angular avec des commentaires détaillés sur chaque ligne pour vous guider :

### 1. Installation d'Angular
Assurez-vous d'avoir Angular CLI installé. Si ce n'est pas le cas, vous pouvez l'installer en utilisant la commande suivante :
```bash
npm install -g @angular/cli
```

### 2. Création d'un nouveau projet Angular
```bash
ng new math-quiz
cd math-quiz
```

### 3. Création d'un composant
Générer un nouveau composant pour gérer l'affichage du quiz :
```bash
ng generate component math-quiz
```

### 4. Code du composant `math-quiz.component.ts`
Remplissez le fichier `math-quiz.component.ts` avec le code suivant :

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-math-quiz',
  templateUrl: './math-quiz.component.html',
  styleUrls: ['./math-quiz.component.css']
})
export class MathQuizComponent implements OnInit {
  // Variables pour stocker les nombres aléatoires et l'opérateur
  number1!: number;
  number2!: number;
  operator!: string;

  // Variable pour stocker le résultat attendu
  expectedResult!: number;

  // Variable pour stocker la réponse de l'utilisateur
  userAnswer!: number;

  // Message pour afficher si la réponse est correcte ou non
  message!: string;

  constructor() { }

  ngOnInit(): void {
    this.generateQuestion();
  }

  // Fonction pour générer une nouvelle question
  generateQuestion(): void {
    // Générer deux nombres aléatoires entre 0 et 9
    this.number1 = Math.floor(Math.random() * 10);
    this.number2 = Math.floor(Math.random() * 10);

    // Choisir un opérateur aléatoire parmi +, -, et *
    const operators = ['+', '-', '*'];
    this.operator = operators[Math.floor(Math.random() * operators.length)];

    // Calculer le résultat en fonction de l'opérateur choisi
    switch (this.operator) {
      case '+':
        this.expectedResult = this.number1 + this.number2;
        break;
      case '-':
        // S'assurer que le résultat n'est pas négatif
        if (this.number1 < this.number2) {
          [this.number1, this.number2] = [this.number2, this.number1];
        }
        this.expectedResult = this.number1 - this.number2;
        break;
      case '*':
        this.expectedResult = this.number1 * this.number2;
        break;
    }

    // Réinitialiser la réponse de l'utilisateur et le message
    this.userAnswer = 0;
    this.message = '';
  }

  // Fonction pour vérifier la réponse de l'utilisateur
  checkAnswer(): void {
    if (this.userAnswer === this.expectedResult) {
      this.message = 'Bonne réponse !';
    } else {
      this.message = 'Mauvaise réponse. Essayez encore !';
    }
  }
}
```

### 5. Code HTML `math-quiz.component.html`
Le code HTML pour afficher l'interface utilisateur :

```html
<div class="quiz-container">
  <h1>{{ number1 }} {{ operator }} {{ number2 }}</h1>
  <p>Donner la réponse :</p>
  <input [(ngModel)]="userAnswer" type="number">
  <button (click)="checkAnswer()">Soumettre</button>
  <p>{{ message }}</p>
</div>
```

### 6. Ajout du `FormsModule` dans `app.module.ts`
Assurez-vous que le `FormsModule` est importé dans le module principal pour que la liaison des données fonctionne correctement :
```typescript
import { FormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    // autres composants
    MathQuizComponent
  ],
  imports: [
    // autres modules
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### 7. Styliser le composant `math-quiz.component.css`
Vous pouvez styliser votre composant en utilisant ce CSS de base :

```css
.quiz-container {
  text-align: center;
  margin-top: 50px;
}

h1 {
  font-size: 2em;
  margin-bottom: 20px;
}

input {
  padding: 10px;
  font-size: 1.2em;
  width: 100px;
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  font-size: 1.2em;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

p {
  font-size: 1.2em;
  margin-top: 20px;
}
```

### 8. Affichage du composant dans l'application principale
Enfin, modifiez le `app.component.html` pour afficher le quiz :
```html
<app-math-quiz></app-math-quiz>
```

### 9. Lancement de l'application
Lancez l'application Angular :
```bash
ng serve
```

Accédez à [http://localhost:4200](http://localhost:4200) pour voir le quiz de mathématiques en action.

Ce projet génère des opérations mathématiques aléatoires, et l'utilisateur peut soumettre sa réponse pour savoir si elle est correcte. J'ai ajouté des commentaires détaillés pour chaque partie du code. Si vous avez besoin de plus d'explications ou de modifications, n'hésitez pas à demander !
