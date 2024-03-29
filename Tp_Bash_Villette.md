 # TP2 - Bash

 ## Exercice 1. Variables d’environnement

 ### 1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
 Pour trouver dans quels dossier bash trouve les commandes, on tape:
 </br><code>printenv PATH</code></br>
 Puis la commande affiche tout les dossiers comprenant des commandes bash</br>

### 2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?
La variable d'environnement est: %HOME%. </br>

### 3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.
La variable **LANG** indique quelle langue est utilisée par les logiciels pour communiquer avec l'utilisateur.</br>
La variable **PWD** contient le chemin vers le repertoire courant de l'interpréteur de commande. </br>
La variable **OLDPWD** contient le chemin vers le repertoire courant précédant. </br>
La variable **SHELL** indique ou se situe l'interpreteur shell par défaut. </br>
La variable **_** indique dans quel repertoire se situe la commande tapée précédemment. </br>

### 4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.
Pour créer une variable MY_VAR, il faut taper la commande:
</br><code>VAR="Linuxien"</code></br>
Puis pour vérifier qu'elle existe il faut taper:
</br><code>echo $VAR</code></br>

### 5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.
La commande bash permet d'ouvrir un nouveau shell.</br>
Ainsi la Variable MY_VAR n'existe plus puisqu'elle n'est pas permanente et est effective que pour la session courante.</br>

### 6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.
Pour transformer la variable MY_VAR en une variable d'environnement il faut ajouter la commande avec:
</br><code>export VAR="Linuxien"</code></br>
Puis après avoir tapé la commande bash, et essayé d'afficher la Variable MY_VAR on obtient bel et bien sa valeur.</br>
Vu que la variable MY_VAR est une variable d'environnement, elle est connu de tout les shells.</br>

### 7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.
Pour créer une variable NOMS ayant pour contenu vos noms de binômes séparés par un espace, il faut taper la commande:
</br><code>NOMS="Gaetan Remi"</code></br>
Puis il suffit de taper la commande:
</br><code>echo $NOMS</code></br>

### 8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.
On crée une commande BONJOURBINOME:
</br><code>export BONJOURBINOME="Bonjour à vous deux, $Noms !"</code></br>
ou l'on peut utiliser juste un echo à la place de export BONJOURBINOME=.

### 9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?
La commande unset permet de supprimer la variable tandis qu'avec une valeur vide la variable est utilisable mais en valeur nulle. </br>

### 10. Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)
Afin d'écrire la commande ci-dessus, il faut taper:
</br><code>echo '$HOME='"$HOME"</code></br>
ou
</br><code>echo "\$HOME=$HOME"</code></br>

## Exercice 2. Contrôle de mot de passe

Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au
contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par
l’utilisateur ne doit pas s’afficher.</br>

Creer le dossier script:
<code>mkdir script</code></br>
Le placer dans le PATH:
<code>PATH=$PATH:~/script</code></br>
Ecrire le script:
<code>nano testpwd.sh</code></br>

```bash
#!/bin/bash
PASSWORD="LeroyJenkins"
read -p 'Saisissez un mot de passe: ' -s mdp 
if [ "$mdp" = "$PASSWORD" ]; then
    echo "Le mot de passe est identique!"
else
    echo "Le mot de passe n'est pas le meme que celui d'origine"
fi
```
Pour quitter il faut faire une Ctrl+s pour sauvegarder puis Ctrl+x pour quitter.
Ensuite pour tester le script il faut le rendre executable avec la commande:
<code>chmod u+x testpwd.sh</code></br>
Et le tester avec la commande:
<code>./testpwd.sh</code></br>

## Exercice 3. Ecrivez un script qui prend un paramètre et utilise la fonction is_number() pour vérifier que ce paramètre est un nombre réel et affichera un message d'erreur dans le cas contraire.
Ecrire le script:
<code>nano TestNbr.sh</code></br>
```bash
#!/bin/bash
function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
 return 1
else
 return 0
fi
}

if [[ is_number $1 = 0 ]]; then
 echo "$1 est un nombre réel ."
else
 echo "$1 n'est pas un nombre réel."
fi
```
## Exercice 4. Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”,bas où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement).

Ecrire le script:
<code>nano VerifUser.sh</code></br>
```bash
#!/bin/bash
INPUT_USER=$1
FILENAME="${0##*/}"
USERS=$(cut -d: -f1 /etc/passwd)
if [ -z "$VAR_USER" ]; then
 echo "Utilisation: $FILENAME nom_utilisateur"
else
 EXIST=0
 for user in  $USERS
 do
  if [ "$user" = "$VAR_USER" ]; then
   echo "L'utilisateur $VAR_USER existe deja."
   EXIST=1
  fi
 done
 if [ $EXIST -eq 0 ]; then
  echo "Aucun utilisateur comme $VAR_USER n'est renseigné."
 fi
 fi
```

## Exercice 5. Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que l’utilisateur saisit toujours un entier naturel).
Ecrire le script:
<code>nano Factorielle.sh</code></br>
```bash
#!/bin/bash
fact() { 
 n=$1 
 if [ $n -eq 0 ]; then 
  echo 1 
 else 
  echo $(( n * `fact $(( n - 1 ))` )) 
 fi 
} 
echo `fact $1`
```

## Exercice 6. Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner. Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM). = Juste prix
Ecrire le script:
<code>nano JustePrix.sh</code></br>
```bash
#!/bin/bash
NOMBRE=$(( ( RANDOM % 100 )  + 1 ))
VAR_NB=-1
echo "Essaye de trouver un nombre entre 1 et 100 !"
while [ $NOMBRE != $VAR_NB ]
do
 echo $NOMBRE
 read VAR_NB
 if [ $NOMBRE -lt $VAR_NB ]; then
  echo "Raté, essaye encore!! Il est plus petit :)"
 elif [ $NOMBRE -gt $VAR_NB ]; then
  echo "Et non c'est raté ! Il est plus grand :)"
 fi
done
echo "Waow master mind !"
```
## Exercice 7. Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres sont bien des entiers.

...



