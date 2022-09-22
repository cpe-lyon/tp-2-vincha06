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
- <code> MY_VAR="" ; </code>
- <code> printenv MY_VAR </code>
- <code> echo $MY_VAR </code>

### 5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.
- Oui mais ça ne fait rien car la variable est une variable locale qui n'est pas dans le bash.

### 6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.
- Ça marche puisque la variable est devenue une variable d'environnement.

### 7. Créer la variable d’environnement NOM ayant pour contenu vos prénom et nom séparés par un espace. Afficher la valeur de NOM pour vérifier que l’affectation est correcte.
> ![image](https://user-images.githubusercontent.com/113091304/190336542-6157ffac-8e7d-4d1c-883d-cff098b8e693.png)

### 8. Ecrivez une commande qui affiche ”Bonjour à vous, prenom nom !” en utilisant la variable NOM.
> ![image](https://user-images.githubusercontent.com/113091304/190337369-3d43a0de-6b08-40f1-bd2b-20001e9d0b1f.png)

### 9. Quelle différence y a-t-il entre donner une valeur vide à une variable d’environnement et l’utilisation de la commande unset ?
- Avec une valeur vide la variable existe quand même, alors que "unset" supprime la variable.

### 10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)
> ![image](https://user-images.githubusercontent.com/113091304/190338310-0cabc0f6-9ad0-4070-bd45-be1c433b4ece.png)

# Programmation Bash

### Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel. Tous les scripts sont bien entendu à tester. Ajoutez le chemin vers script à votre PATH de manière permanente.
> ![image](https://user-images.githubusercontent.com/113091304/190346467-a0b806ce-1f11-48b7-8e6c-f9bfbb573712.png)

## Exercice 2. Contrôle de mot de passe

### Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par l’utilisateur ne doit pas s’afficher.
- ![image](https://user-images.githubusercontent.com/113091304/190345580-b6654f5d-ce1d-408b-a3d4-5ec661d0d4dc.png)
> ![image](https://user-images.githubusercontent.com/113091304/190350928-c66be2b5-5951-4034-859c-85a85c0b87b8.png)

## Exercice 3. Expressions rationnelles
- ![image](https://user-images.githubusercontent.com/113091304/190360232-4a0a849f-90fe-4571-b4e9-84b6163796ef.png)
> ![image](https://user-images.githubusercontent.com/113091304/190360544-1bd28390-2283-4a6e-b03f-6163ee3b146b.png)

## Exercice 4. Contrôle d’utilisateur
- ![image](https://user-images.githubusercontent.com/113091304/190373963-0f9d50bf-dc3c-49ae-ae70-6f8d00cdfd9b.png)
> ![image](https://user-images.githubusercontent.com/113091304/190373682-4c9b5565-42cc-4341-a8b8-35519674ec62.png)

## Exercice 5. Factorielle
- ![image](https://user-images.githubusercontent.com/113091304/191675264-bc3ac3dc-38dc-42de-94ae-db89732352a9.png)
> ![image](https://user-images.githubusercontent.com/113091304/191675479-1601889f-492b-4695-b5fa-57c9674ee3b8.png)

## Exercice 6. Le juste prix
- ![image](https://user-images.githubusercontent.com/113091304/191679535-d9668db4-10c6-4da7-9b1e-16c7fbced613.png)
> ![image](https://user-images.githubusercontent.com/113091304/191679081-f5994424-2f8b-41b3-81ff-7761109eea85.png)

## Exercice 7. Statistiques
1.
```console
#!/bin/bash
 
error=0
max=0
min=0
moyenne=0

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
        return 1
else
        return 0
fi
}

function max(){
        if { $1 -gt $2}; then
                max=$1
        elif { $3 -gt $1 }; then
                max=$3
        else
                max=$2
        fi
}

function min(){
        if [ $1 -lt $2 ]; then
                min=$1
        elif [ $3 -gt $1 ]; then
                min=$3
        else
                min=$2
        fi
}

function moyenne(){
        moyenne=$((( $1 + $2 + $3 ) / 3 ))
}

min $1 $2 $3
max $1 $2 $3
moyenne $1 $2 $3

while (("$#"));
do
        is_number $1
        if [ $? = 1 ] || [ $1 -gt 100 ] || [ $1 -lt -100 ]; then
                echo "Veuillez saisir des nombres compris entre 100 et -100"
                exit
        fi
        shift
done

echo "Le minimum est $min"
echo "Le maximum est $max"
echo "La moyenne est $moyenne"
```
2.
```console
#!/bin/bash
 
max=0
min=$1
moyenne=0
param=0
count=0
sum=0

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
        return 1
else
        return 0
fi
}

function max(){
        if { $1 -gt $max}; then
                max=$1
        fi
}

function min(){
        if [ $1 -lt $min ]; then
                min=$1
        fi
}





function moyenne(){
        moyenne=$((( $1 + $2 + $3 ) / 3 ))
}

min $1 $2 $3
max $1 $2 $3
moyenne $1 $2 $3

while (("$#"));
do
        is_number $1
        if [ $? = 1 ] || [ $1 -gt 100 ] || [ $1 -lt -100 ]; then
                echo "Veuillez saisir des nombres compris entre 100 et -100"
                exit
        fi
        param=$(( $1 + $param ))
        sum=$param
        min $1
        max $1
        count=$(( $count + 1 ))
        shift
done

function moyenne(){
        moyenne=$(( $sum / $count ))
}

moyenne

echo "Le minimum est $min"
echo "Le maximum est $max"
echo "La moyenne est $moyenne"
```
3.
```console
#!/bin/bash
 
max=0
moyenne=0
param=0
sum=0
tab=()
index=0

read -p "Nombre de notes à entrer ? " nbr

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
        return 1
else
        return 0
fi
}

function tableau(){
        for i in $(seq 1 $nbr)
        do
                read -p "Saisi votre note numéro $i " note
                tab[$index]=$note
                index=$(( $index + 1 ))
        done
 }
 
 tableau
 
 min=${tab[0]}

function max(){
        local index=0
        for l in $(seq l $nbr)
        do
                if [ ${tab[index]} -gt $max ]; then
                        max=${tab[$index]}
                fi
                index=$(( $index + 1 ))
        done
        echo "Le maximum est $max"
}

max

function min(){
        local index=0
        for l in $(seq l $nbr)
        do
                if [ ${tab[index]} -gt $min ]; then
                        min=${tab[$index]}
                fi
                index=$(( $index + 1 ))
        done
        echo "Le maximum est $min"
}


min


function moyenne(){
        local index=0
        for l in $(seq l $nbr)
        do
                param=$(( $param + ${tab[$index]} ))
                sum=$param
                index=$(( $index + 1 ))
        done
        echo "La moyenne est $moyenne "
}

moyenne
```











