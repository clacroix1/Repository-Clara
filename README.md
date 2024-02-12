# Repository-Clara
#faire un formulaire avec le destinataire, le select, ensuite on crée un script PHP qui va permettre la création et l'envoie des tickets, puis on pourra passer sur la suppression des tickets, et finalement gestion des mots de passe oubliés, ... language utilés : PhP, CSS, html, ...

<?php
// Initialisation des variables
$name = "";
$mail = "";
$date = "";
$display = false; // Ajout d'une variable pour gérer l'affichage des erreurs

// Récupération des données du formulaire
if ($_SERVER["REQUEST_METHOD"] == "GET") {
    $name = $_GET['name'];
    $mail = $_GET['mail'];
    $date = $_GET['date'];

    // Vérification des données des champs obligatoires
    if (isset($_GET['name']) && isset($_GET['mail']) && isset($_GET['date'])) {

        // Vérification du format du mail
        $regex_mail = '/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/';
        if (!preg_match($regex_mail, $_GET['mail'])) {
            $display = true;
        } else {
            $mail = $_GET['mail'];
        }

        // Vérification du format de la date
        $regex_date = "/^[0-9]{4}-[0-9]{2}-[0-9]{2}$/";
        if (!preg_match($regex_date, $_GET['date'])) {
            $display = true;
        } else {
            $date = $_GET['date'];
        }

        // Tout est ok
        if (!$display) {
            echo "Les informations saisies sont correctes<br />";
        } else {
            echo "Les informations saisies sont incorrectes<br />";
        }
    }
}

// Utilisation des données
echo "Nom: $name<br>";
echo "Mail: $mail<br>";
echo "Date de naissance: $date<br>";

if ($display) {
    // Le formulaire que vous utilisez
    ?>
    <form action="cible.php" method="get">
        <label for='idName'>Name</label>
        <input type='text' name='name' id='idName'/>

        <label for='idLogin'>Mail</label>
        <input type='email' name='mail' id='idLogin' required="required"/>

        <label for='idDate'>Date de naissance</label>
        <input type='date' name='date' id='idDate'/>

        <br/>
        <input type='submit' value='Valider'/>
    </form>
    <?php
}
?>

