<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/a7a70adc-a8a6-4192-bf9f-718cf5fba2bd" />
Projet C++ : Classe CompteBancaire

Exercice de programmation orientée objet en C++ : gestion d'un compte bancaire avec mémoire dynamique, règle de cinq et historique des opérations.

Description

La classe CompteBancaire représente un compte avec les attributs suivants :

Attribut	Type	Description
numero	std::string	Numéro du compte
solde	double	Solde courant
historique	std::string*	Tableau dynamique des opérations
capacite	std::size_t	Taille allouée du tableau
nbOps	std::size_t	Nombre d'opérations enregistrées
Fonctionnalités
Constructeur par défaut et constructeur paramétré (le solde initial négatif est refusé).
Constructeur de copie (copie profonde) et constructeur de déplacement.
Opérateurs d'affectation par copie et par déplacement (règle de cinq).
Destructeur libérant le tableau dynamique avec delete[].
deposer(double), retirer(double) et afficher().
Historique des opérations avec agrandissement automatique (la capacité double quand le tableau est plein).
Montants formatés avec 2 décimales.
Notions illustrées
Gestion de la mémoire dynamique (new[] / delete[]).
Copie profonde et sémantique de déplacement (std::move, noexcept).
Règle de cinq : destructeur, constructeur de copie, constructeur de déplacement, deux operator=.
État valide d'un objet déplacé : historique = nullptr, capacite = 0. L'agrandissement gère le cas capacite == 0.
Structure du projet
CompteBancaire/
├── src/
│   └── compte.cpp     # Classe + main de test
└── README.md
Compilation et exécution
En ligne de commande (g++)
bash
g++ -std=c++17 -Wall -Wextra -pedantic src/compte.cpp -o compte
./compte
Avec Eclipse CDT
File → New → C++ Project → Hello World C++ Project.
Coller le code dans src/compte.cpp.
Activer C++17 : Project → Properties → C/C++ Build → Settings → GCC C++ Compiler → Dialect, puis choisir ISO C++17.
Project → Build All (Ctrl+B), puis Run → Run (Ctrl+F11).
Exemple d'utilisation
cpp
CompteBancaire c1("FR123456", 500.0);
c1.deposer(200);
c1.retirer(150);
c1.afficher();

CompteBancaire c2 = c1;             // copie
CompteBancaire c3 = std::move(c1);  // déplacement
Résultat attendu (extrait)
Compte FR123456 - Solde : 550.00
Historique des operations :
  Creation du compte avec solde 500.00
  Depot de 200.00
  Retrait de 150.00
Problèmes fréquents
Problème	Solution
std::move non reconnu	Ajouter #include <utility>.
std::size_t non reconnu	Ajouter #include <cstddef>.
Crash (double free) après c2 = c1;	Il manque operator= : sans lui, le pointeur est copié et libéré deux fois.
Écriture hors tableau après un déplacement	agrandirHistorique() doit gérer capacite == 0.
Montants affichés 500.000000	Utiliser ostringstream avec std::fixed et setprecision(2) à la place de std::to_string.
Améliorations possibles
Remplacer le tableau dynamique par std::vector<std::string> (règle de zéro : plus besoin de gérer la mémoire à la main).
Lever des exceptions (std::invalid_argument) au lieu d'afficher sur std::cerr.
Ajouter la date de chaque opération.
Ajouter une méthode virement(CompteBancaire&, double).
Auteur

Nom : à compléter Filière : INFO, Licence, Semestre 3 Module : à compléter
