Gestion des inscriptions – Projet Web

    

Bienvenue dans le projet Gestion des inscriptions pour l'Ecole 221. Cette application web simplifie la gestion des inscriptions, des classes, des professeurs et des étudiants avec des statistiques claires et une gestion efficace des demandes d'inscription.

✏️ Description

Cette application permet au Responsable Pédagogique (RP), aux Attachés de Classe, aux Professeurs et aux Étudiants de collaborer efficacement sur les tâches liées aux inscriptions scolaires.

Principales fonctionnalités

Responsable Pédagogique (RP) :

🖊️ Création et gestion des classes (libellé, filière, niveau).

🔧 Ajout et gestion des professeurs (nom complet, grade) et de leurs modules.

🔐 Assignation des modules aux professeurs.

📊 Liste des classes et modules d’un professeur.

Attaché de Classe :

✍️ Gestion des inscriptions/réinscriptions des étudiants (année scolaire).

📝 Liste des étudiants inscrits par classe et par année scolaire.

🛂 Gestion et suivi des demandes d'annulation ou de suspension des inscriptions des étudiants.

Étudiant :

❓ Formulation des demandes d'annulation/suspension d'inscription (motif, date).

🔍 Consultation et filtrage de ses demandes par état.

Statistiques :

🔢 Effectif de l'école par année.

👩‍👧 Répartition par genre (école/classe).

🔢 Effectif des étudiants ayant annulé ou suspendu leur inscription (par année).

📊 Technologies utilisées

Langage backend : PHP

Base de données : JSON (fichier local)

Frameworks frontend : HTML, CSS, JavaScript

🛠️ Implémentation de la base de données JSON

L'application utilise un fichier JSON comme base de données. Les données sont manipulées via des fonctions PHP encapsulées dans une classe Convert.php. Voici les principales méthodes disponibles :

Fonctions principales

1. Lecture des données JSON (🔍)

function fromJsonToArray(string $key = null): array {
    $json = file_get_contents(DB);
    $arrayData = json_decode($json, true);
    return $key == null ? $arrayData : $arrayData[$key];
}

Description : Convertit le fichier JSON en tableau PHP.

Paramètre :

$key : Clé spécifique à récupérer (optionnel).

Retour : Tableau contenant les données JSON.

2. Ajout de données (➕)

function fromArrayToJson(string $key, array $newData) {
    $arrayData = fromJsonToArray();
    $arrayData[$key][] = $newData;
    $json = json_encode($arrayData);
    file_put_contents(DB, $json);
}

Description : Ajoute de nouvelles données dans le fichier JSON.

Paramètres :

$key : Clé à laquelle les nouvelles données seront ajoutées.

$newData : Données à ajouter.

3. Mise à jour des données (🔄)

function fromArrayToJsonUpdate(string $key, string $key2, int $id, array $newData) {
    $arrayData = fromJsonToArray();
    foreach ($arrayData[$key] as &$data) {
        if ($data["id"] == $id) {
            foreach ($newData as $value) {
                $data[$key2] = array_merge($data[$key2], $value);
            }
        }
    }
    $json = json_encode($arrayData);
    file_put_contents(DB, $json);
}

Description : Met à jour une entité spécifique dans le fichier JSON.

Paramètres :

$key : Clé principale (exemple : "professeurs").

$key2 : Sous-clé à mettre à jour (exemple : "modules").

$id : Identifiant unique de l'entité.

$newData : Nouvelles données à insérer.

🖌️ Diagrammes à produire

Diagramme de contexte : 🌐 Vue d’ensemble des interactions entre les acteurs.

Diagramme de cas d’utilisation : 🔍 Précise les fonctionnalités par acteur.

Diagramme de package : 📦 Organisation du système en modules cohérents.

Diagramme de classe : 🔬 Modélisation des entités (classes, relations).

✨ Points forts

🔧 Utilisation de JSON comme base de données pour simplifier le développement.

🔄 Manipulation optimisée des données via des fonctions PHP claires et réutilisables.

🔐 Gestion multi-acteurs avec un système d’authentification.

📊 Statistiques détaillées pour un suivi précis.

🚀 Lancement du projet

🔄 Clonez le projet :

git clone https://github.com/votre-repo/gestion-inscriptions.git

🎮 Assurez-vous que PHP 8.0+ est installé sur votre machine.

🔧 Placez le fichier JSON dans le répertoire db/ et modifiez la constante DB dans le fichier Convert.php pour pointer vers ce fichier.

Lancez un serveur local PHP :

php -S localhost:8000

Accédez à l’application via http://localhost:8000.

