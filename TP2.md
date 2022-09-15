Vincent CHAVES - 3ICS

# TP 2 - Bash

## Exercice 1. Variables d’environnement

### 1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
- Dans :
> /bin
> /usr/bin
> /usr/local/bin

### 2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?
- <code> $HOME </code>

### 3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL.
- La variable LANG détermine la langue que les logiciels utilisent pour communiquer avec l’utilisateur, PWD sert à connaître le chemin du dossier dans lequel on se trouve, OLDPWD sert à connaître le chemin du dossier dans lequel on se trouvait juste avant. SHELL contient l'interpréteur de commande.

### 4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.
<code> MY_VAR="" ; </code>
<code> printenv MY_VAR </code>
<code> echo $MY_VAR </code>

### 5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.
- Oui mais ça ne fait rien car la variable n'est pas une variable d'environnement.

### 6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.
- Ça marche puisque la variable est devenue une variable d'environnement.

### 7. Créer la variable d’environnement NOM ayant pour contenu vos prénom et nom séparés par un espace. Afficher la valeur de NOM pour vérifier que l’affectation est correcte.
- ![image](https://user-images.githubusercontent.com/113091304/190336542-6157ffac-8e7d-4d1c-883d-cff098b8e693.png)

### 8. Ecrivez une commande qui affiche ”Bonjour à vous, prenom nom !” en utilisant la variable NOM.
- ![image](https://user-images.githubusercontent.com/113091304/190337369-3d43a0de-6b08-40f1-bd2b-20001e9d0b1f.png)

### 9. Quelle différence y a-t-il entre donner une valeur vide à une variable d’environnement et l’utilisation de la commande unset ?
- Avec une valeur vide la variable existe quand même, alors que "unset" supprime la variable.

### 10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)
![image](https://user-images.githubusercontent.com/113091304/190338310-0cabc0f6-9ad0-4070-bd45-be1c433b4ece.png)

# Programmation Bash

## Exercice 2. Contrôle de mot de passe

### Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par l’utilisateur ne doit pas s’afficher.

<code> #!/bin/bash

PASSWORD="User@dmin!"
read -s -p "Entrez le mot de passe : " entry_password

if [ "$entry_password" = "$PASSWORD" ] ; then
        echo "Mot de passe correct"
else
        echo "Mot de passe incorrect"
fi
</code>





