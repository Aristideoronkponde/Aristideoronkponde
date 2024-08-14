1. Créez un nouveau projet AngularSi vous n'avez pas encore Angular CLI installé, installez-le d'abord :npm install -g @angular/cliEnsuite, créez un nouveau projet :ng new projet-mot-de-passe
cd projet-mot-de-passe2. Créez un composant pour le formulaire de connexionCréez un composant dédié au formulaire de connexion :ng generate component login-form3. Créez le formulaire de connexionDans le fichier login-form.component.html, créez un formulaire avec les champs "Nom d'utilisateur" et "Mot de passe", ainsi qu'un bouton d'envoi :<form (ngSubmit)="onSubmit()" #loginForm="ngForm">
  <div>
    <label for="username">Nom d'utilisateur</label>
    <input type="text" id="username" name="username" [(ngModel)]="username" required>
  </div>

  <div>
    <label for="password">Mot de passe</label>
    <input type="password" id="password" name="password" [(ngModel)]="password" required (input)="checkPassword()">
  </div>

  <ul>
    <li [class.valid]="passwordLengthValid">Minimum 8 caractères</li>
    <li [class.valid]="passwordUppercaseValid">Au moins une majuscule</li>
    <li [class.valid]="passwordLowercaseValid">Au moins une minuscule</li>
    <li [class.valid]="passwordNumberValid">Au moins un chiffre</li>
  </ul>

  <button type="submit" [disabled]="!isFormValid()">Envoyer</button>
</form>4. Ajoutez la logique pour valider le mot de passeDans le fichier login-form.component.ts, ajoutez la logique pour valider le mot de passe en temps réel :import { Component } from '@angular/core';

@Component({
  selector: 'app-login-form',
  templateUrl: './login-form.component.html',
  styleUrls: ['./login-form.component.css']
})
export class LoginFormComponent {
  username: string = '';
  password: string = '';

  passwordLengthValid: boolean = false;
  passwordUppercaseValid: boolean = false;
  passwordLowercaseValid: boolean = false;
  passwordNumberValid: boolean = false;

  checkPassword(): void {
    this.passwordLengthValid = this.password.length >= 8;
    this.passwordUppercaseValid = /[A-Z]/.test(this.password);
    this.passwordLowercaseValid = /[a-z]/.test(this.password);
    this.passwordNumberValid = /\d/.test(this.password);
  }

  isFormValid(): boolean {
    return this.passwordLengthValid && this.passwordUppercaseValid &&
           this.passwordLowercaseValid && this.passwordNumberValid;
  }

  onSubmit(): void {
    if (this.isFormValid()) {
      localStorage.setItem('password', this.password);
      alert('Félicitations, mot de passe enregistré!');
      this.triggerAnimation();
    }
  }

  triggerAnimation(): void {
    // Implémentez ici une animation, par exemple en changeant la classe CSS d'un élément
  }
}5. Stylez le composantAjoutez du CSS pour indiquer quand les règles du mot de passe sont respectées dans login-form.component.css :.valid {
  color: green;
}

.invalid {
  color: red;
}6. Animation après soumissionAjoutez une animation dans votre fichier CSS ou utilisez une librairie d'animations Angular comme @angular/animations pour féliciter l'utilisateur après la soumission du formulaire. Exemple simple avec CSS :@keyframes successAnimation {
  0% { opacity: 0; transform: scale(0.5); }
  100% { opacity: 1; transform: scale(1); }
}

.success {
  animation: successAnimation 0.5s ease-in-out;
}Dans votre méthode triggerAnimation, vous pouvez ajouter une classe pour déclencher cette animation :triggerAnimation(): void {
  const formElement = document.querySelector('form');
  if (formElement) {
    formElement.classList.add('success');
  }
}7. Persistance des données avec localStorageLe mot de passe est sauvegardé dans le localStorage lorsque le formulaire est soumis. Vous pouvez également récupérer le mot de passe sauvegardé lors de l'initialisation du composant pour pré-remplir le champ mot de passe si besoin :ngOnInit(): void {
  const savedPassword = localStorage.getItem('password');
  if (savedPassword) {
    this.password = savedPassword;
    this.checkPassword();
  }
 }8. Testez et ajustezLancez l'application pour tester votre formulaire :ng serveVisitez http://localhost:4200 pour voir le formulaire en action. Assurez-vous que toutes les fonctionnalités fonctionnent comme prévu.9. Bonus : Ajoutez des tests unitairesVous pouvez également ajouter des tests unitaires pour vérifier que les fonctionnalités fonctionnent correctement en utilisant Jasmine et Karma (intégrés dans Angular).Avec ces étapes, vous devriez avoir un formulaire de connexion fonctionnel avec validation dynamique du mot de passe, sauvegarde locale et animation après la soumission                                      1. Créez un nouveau projet AngularSi vous n'avez pas encore Angular CLI installé, installez-le d'abord :npm install -g @angular/cliEnsuite, créez un nouveau projet :ng new projet-mot-de-passe
cd projet-mot-de-passe2. Créez un composant pour le formulaire de connexionCréez un composant dédié au formulaire de connexion :ng generate component login-form3. Créez le formulaire de connexionDans le fichier login-form.component.html, créez un formulaire avec les champs "Nom d'utilisateur" et "Mot de passe", ainsi qu'un bouton d'envoi :<form (ngSubmit)="onSubmit()" #loginForm="ngForm">
  <div>
    <label for="username">Nom d'utilisateur</label>
    <input type="text" id="username" name="username" [(ngModel)]="username" required>
  </div>

  <div>
    <label for="password">Mot de passe</label>
    <input type="password" id="password" name="password" [(ngModel)]="password" required (input)="checkPassword()">
  </div>

  <ul>
    <li [class.valid]="passwordLengthValid">Minimum 8 caractères</li>
    <li [class.valid]="passwordUppercaseValid">Au moins une majuscule</li>
    <li [class.valid]="passwordLowercaseValid">Au moins une minuscule</li>
    <li [class.valid]="passwordNumberValid">Au moins un chiffre</li>
  </ul>

  <button type="submit" [disabled]="!isFormValid()">Envoyer</button>
</form>4. Ajoutez la logique pour valider le mot de passeDans le fichier login-form.component.ts, ajoutez la logique pour valider le mot de passe en temps réel :import { Component } from '@angular/core';

@Component({
  selector: 'app-login-form',
  templateUrl: './login-form.component.html',
  styleUrls: ['./login-form.component.css']
})
export class LoginFormComponent {
  username: string = '';
  password: string = '';

  passwordLengthValid: boolean = false;
  passwordUppercaseValid: boolean = false;
  passwordLowercaseValid: boolean = false;
  passwordNumberValid: boolean = false;

  checkPassword(): void {
    this.passwordLengthValid = this.password.length >= 8;
    this.passwordUppercaseValid = /[A-Z]/.test(this.password);
    this.passwordLowercaseValid = /[a-z]/.test(this.password);
    this.passwordNumberValid = /\d/.test(this.password);
  }

  isFormValid(): boolean {
    return this.passwordLengthValid && this.passwordUppercaseValid &&
           this.passwordLowercaseValid && this.passwordNumberValid;
  }

  onSubmit(): void {
    if (this.isFormValid()) {
      localStorage.setItem('password', this.password);
      alert('Félicitations, mot de passe enregistré!');
      this.triggerAnimation();
    }
  }

  triggerAnimation(): void {
    // Implémentez ici une animation, par exemple en changeant la classe CSS d'un élément
  }
}5. Stylez le composantAjoutez du CSS pour indiquer quand les règles du mot de passe sont respectées dans login-form.component.css :.valid {
  color: green;
}

.invalid {
  color: red;
}6. Animation après soumissionAjoutez une animation dans votre fichier CSS ou utilisez une librairie d'animations Angular comme @angular/animations pour féliciter l'utilisateur après la soumission du formulaire. Exemple simple avec CSS :@keyframes successAnimation {
  0% { opacity: 0; transform: scale(0.5); }
  100% { opacity: 1; transform: scale(1); }
}

.success {
  animation: successAnimation 0.5s ease-in-out;
}Dans votre méthode triggerAnimation, vous pouvez ajouter une classe pour déclencher cette animation :triggerAnimation(): void {
  const formElement = document.querySelector('form');
  if (formElement) {
    formElement.classList.add('success');
  }
}7. Persistance des données avec localStorageLe mot de passe est sauvegardé dans le localStorage lorsque le formulaire est soumis. Vous pouvez également récupérer le mot de passe sauvegardé lors de l'initialisation du composant pour pré-remplir le champ mot de passe si besoin :ngOnInit(): void {
  const savedPassword = localStorage.getItem('password');
  if (savedPassword) {
    this.password = savedPassword;
    this.checkPassword();
  }
}8. Testez et ajustezLancez l'application pour tester votre formulaire :ng serveVisitez http://localhost:4200 pour voir le formulaire en action. Assurez-vous que toutes les fonctionnalités fonctionnent comme prévu.9. Bonus : Ajoutez des tests unitairesVous pouvez également ajouter des tests unitaires pour vérifier que les fonctionnalités fonctionnent correctement en utilisant Jasmine et Karma (intégrés dans Angular).Avec ces étapes, vous devriez avoir un formulaire de connexion fonctionnel avec validation dynamique du mot de passe, sauvegarde locale et animation après la soumission  
