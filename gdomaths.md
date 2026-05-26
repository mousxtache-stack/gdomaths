**Introduction**

Bonjour à tous. Il y a un adage bien connu des concessionnaires automobiles qui dit : "Dès que vous sortez une voiture neuve du garage, elle a déjà perdu 20 % de sa valeur". Cette réalité économique frappe la plupart des acheteurs. Une voiture est un bien de consommation qui se déprécie avec le temps. 

Mais cette perte de valeur n'est ni aléatoire ni linéaire. Elle suit une logique mathématique précise. C’est ce qui m’a amené à me poser la problématique suivante : **Comment modéliser et prévoir la perte de valeur marchande d’un véhicule au fil des années ?**

Pour répondre à cette question, nous allons d'abord partir de la collecte de données réelles pour établir un premier modèle discret. Ensuite, nous affinerons ce modèle avec des fonctions continues, ce qui nous amènera à calculer ce qu'on appelle le "temps de demi-vie" du véhicule. Enfin, nous confronterons notre modèle mathématique à la réalité du marché grâce aux limites et aux probabilités.

**Partie 1 : Constat et données**

Commençons par les faits. En observant le marché de l'occasion, les experts estiment qu'après la forte décote de la première année, une voiture perd en moyenne 15 % de sa valeur chaque année par rapport à l'année précédente. 

Imaginons que j'achète une voiture neuve à 20 000 euros. 
Au bout d'un an, elle ne perd pas 15 % du prix initial, mais 15 % de sa valeur actuelle. Ce mécanisme de baisse en pourcentage successif doit immédiatement nous faire penser à un outil mathématique bien précis : les suites.

**Partie 2 : Modélisation avec les suites et les exponentielles**

Pour modéliser cette situation, définissons une suite $(V_n)$ qui représente la valeur de la voiture après $n$ années. 
Diminuer une valeur de 15 %, cela revient à la multiplier par $1 - \frac{15}{100}$, soit $0,85$.
On a donc la relation : 

$V_{n+1} = V_n \times 0,85$. 

Nous sommes face à une **suite géométrique** de premier terme $V_0 = 20 000$ et de raison $q = 0,85$. 
Grâce au cours, je peux exprimer la valeur du véhicule pour n'importe quelle année $n$ avec la formule explicite : 
$V_n = 20 000 \times 0,85^n$.


Cependant, ce modèle discret a un défaut. Une voiture ne perd pas soudainement 15 % de sa valeur le 31 décembre à minuit ! La perte de valeur est un phénomène continu : elle se déprécie chaque mois, chaque jour, chaque kilomètre.

Il est donc plus pertinent de passer d'une suite définie sur les entiers, à une fonction continue définie sur l'ensemble des réels positifs. Le prolongement naturel d'une suite géométrique dans le monde continu, c'est la fonction exponentielle.

On cherche une fonction du temps $t$ de la forme : $V(t) = V_0 \times e^{kt}$, où $k$ est une constante réelle.
Pour que mon modèle continu corresponde à mon modèle discret, il faut que la valeur au bout d'un an, $V(1)$, soit égale à $V_0 \times 0,85$.
Donc : 

$e^k = 0,85$. 

Pour isoler $k$, j'utilise la fonction logarithme népérien, qui est la fonction réciproque de l'exponentielle.
J'obtiens : 

$k = \ln(0,85)$, ce qui donne environ $-0,162$.

Mon modèle final est donc la fonction : 

$V(t) = 20 000 \times e^{-0,162t}$.

Puisque $k$ est négatif, nous avons bien une fonction exponentielle décroissante.

**Partie 3 : Le temps de demie-vie**

Maintenant que nous avons un modèle solide, exploitons-le. Il y a une question que tout acheteur se pose : *"Au bout de combien de temps ma voiture aura-t-elle perdu la moitié de sa valeur ?"*

En physique nucléaire, le temps nécessaire pour que la moitié des noyaux radioactifs se désintègrent s'appelle le temps de demi-vie. En mathématiques, c'est exactement le même principe. Alors calculons le temps de demi-vie, noté $T_{1/2}$, de notre voiture.

Mathématiquement, on cherche l'instant $t$ tel que : 

$V(t) = \frac{V_0}{2}$.

On pose l'équation :

$V_0 \times e^{-0,162t} = 0,5 \times V_0$.

On simplifie par $V_0$ des deux côtés, il reste : 

$e^{-0,162t} = 0,5$.

À nouveau, j'applique le logarithme népérien :

$-0,162t = \ln(0,5)$.

Or, une propriété fondamentale du logarithme nous dit que $\ln(0,5)$ c'est $\ln(\frac{1}{2})$, soit $-\ln(2)$.
On obtient donc $t = \frac{-\ln(2)}{-0,162}$, ce qui donne environ **4,27 années**.

La conclusion est sans appel : tous les 4 ans et 3 mois environ, la voiture voit sa valeur divisée par 2 ! Au bout de 4 ans, notre voiture de 20 000 € n'en vaut plus que 10 000 €. Au bout de 8 ans et demi, elle n'en vaudra plus que 5 000 €. 


**Partie 4 : Les limites du modèle face à la réalité**


Mais ce modèle mathématique exponentiel, aussi élégant soit-il, correspond-il parfaitement à la réalité ? 

La première limite de ce modèle continu, c'est sa limite mathématique justement. Si l'on calcule la limite de $e^{-0,162t}$ quand $t$ tend vers plus l'infini, on trouve $0$. Selon notre équation, la valeur de la voiture finirait par s'annuler totalement. Pourtant, dans la réalité, même une voiture hors d'usage conserve une "valeur résiduelle", comme le prix de la ferraille. Notre modèle devrait donc plutôt tendre vers une asymptote horizontale strictement positive.

Mais la plus grande limite de notre fonction, c'est qu'elle est déterministe. Elle suppose que la dépréciation est une certitude absolue. Or, la vie d'une voiture est intimement liée au hasard ! 
C'est ici que les probabilités entrent en jeu pour rendre notre modèle beaucoup plus réaliste. La valeur de revente sur le marché de l'occasion dépend d'événements aléatoires : un accident, une rayure sur un parking, une panne moteur.

On peut alors décider d'améliorer notre modèle en considérant la valeur de la voiture, non plus comme un nombre certain, mais comme une variable aléatoire que l'on va appeler $X$.

Prenons l'exemple des accidents. On appelle $Y$ la variable aléatoire qui compte le nombre d'accidents subis par la voiture sur une durée de $n$ années. 
Si l'on estime que la probabilité d'avoir un accident dans l'année est de 5 % (soit $p = 0,05$), et que les années sont indépendantes les unes des autres, alors $Y$ suit une loi binomiale de paramètres $n$ et $p=0,05$.

On peut imaginer que chaque accident fait perdre 10 % supplémentaires à la valeur de la voiture, ce qui revient à multiplier son prix par $0,9$. 
La valeur finale de notre voiture, notre variable aléatoire $X$, devient alors l'association de notre modèle exponentiel de base et de notre loi binomiale. 
Son expression serait : $X = V(n) \times 0,9^Y$.

Grâce à cette modélisation probabiliste, je peux calculer deux choses fondamentales :
D'abord, la probabilité de revendre ma voiture à un prix intact, en calculant $P(Y = 0)$, c'est-à-dire la probabilité de n'avoir eu aucun accident.
Mais surtout, je peux calculer l'Espérance mathématique de ma variable $X$, notée $E(X)$. Dans le contexte de mon sujet, cette espérance représente le prix de revente moyen espéré sur le marché, en prenant en compte le risque d'accident. C'est d'ailleurs exactement ce type de croisement entre fonctions et probabilités que les assureurs automobiles utilisent au quotidien pour fixer le prix de nos contrats !

**Conclusion**

Pour conclure, répondre à la question *"Comment votre voiture perd-elle de la valeur ?"* nécessite de faire appel à plusieurs branches des mathématiques. Les suites et la fonction exponentielle nous offrent un cadre prédictif extrêmement puissant, capable de calculer un temps de demi-vie précis. Cependant, l'étude des limites et l'introduction des probabilités nous rappellent que les mathématiques appliquées modélisent le monde, mais doivent toujours s'adapter à la complexité de la réalité matérielle et économique.

Je vous remercie de votre attention.

