# pdo1
<?php
require '_connec.php';
$pdo = new PDO(DSN, USER, PASS);

$query     = 'SELECT * FROM friend';
$statement = $pdo->query($query);
$friends    = $statement->fetchAll(PDO::FETCH_ASSOC);

$firstname = trim($_POST['firstname']);
$lastname = trim($_POST['lastname']);
$query = 'INSERT INTO friend (firstname, lastname) VALUES (:firstname, :lastname)';
$statement = $pdo->prepare($query);
$statement->bindValue(':firstname', $firstname, PDO::PARAM_STR);
$statement->bindValue('lastname', $lastname, PDO::PARAM_STR);
$statement->execute();

?>

<!DOCTYPE html>
<html lang="fr">
    <body>
        <form action="" method="POST">
            <div>
                <label for="firstname">Nom :</label>
                <input type="text" id="firstname" name="firstname" required>
            </div>
            <div>
                <label for="lastname">Prénom :</label>
                <input type="text" id="lastname" name="lastname" required>
            </div>
            <button>Ajouter</button>
        </form>
        <ul>
            <?php foreach ($friends as $friend): ?>
                <li> <?= $friend["firstname"] . ' ' . $friend["lastname"] ?> </li>

            <?php endforeach; ?>
        </ul>
    </body>
</html>
