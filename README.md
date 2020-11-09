# algoplus
Exercice d'algo - Module avancé

 
# Tri par insertion


C'est le tri du joueur de cartes. On fait comme si les éléments à trier étaient donnés un par un, le premier élément constituant, à lui tout seul, une liste triée de longueur 1. On range ensuite le second élément pour constituer une liste triée de longueur 2, puis on range le troisième élément pour avoir une liste triée de longueur 3 et ainsi de suite...
Le principe du tri par insertion est donc d'insérer à la nième itération le nième élément à la bonne place.
PROCEDURE tri_Insertion ( TABLEAU a[0:n-1])
  POUR i VARIANT DE 1 A n-1 FAIRE
    POUR k VARIANT DE i A 1 && a[k] < a[k-1] FAIRE
      ECHANGER a[k] ET a[k-1] ;
    FIN POUR ; 
  FIN POUR ;
FIN PROCEDURE ;


# Tri par sélection

Le principe du tri par sélection/échange (ou tri par extraction) est d'aller chercher le plus petit élément du vecteur pour le mettre en premier, puis de repartir du second élément et d'aller chercher le plus petit élément du vecteur pour le mettre en second, etc...
PROCEDURE tri_Selection ( TABLEAU a[0:n-1])
  POUR i VARIANT DE 0 A n - 2 FAIRE
    TROUVER a[j] LE PLUS PETIT ELEMENT DE a[i + 1:n];
    ECHANGER a[j] ET a[i];
  FIN POUR ; 
FIN PROCEDURE;


# Tri à bulles

Le principe du tri à bulles (bubble sort ou sinking sort) est de comparer deux à deux les éléments e1 et e2 consécutifs d'un tableau et d'effecteur une permutation si e1 > e2. On continue de trier jusqu'à ce qu'il n'y ait plus de permutation.
PROCEDURE tri_Bulle ( TABLEAU a[0:n-1])
  passage ← 0
  REPETER
    permut ← FAUX
    POUR i VARIANT DE 0 A n - 2 - passage FAIRE
      SI a[i] > a[i+1] ALORS
        echanger a[i] ET a[i+1]
        permut ← VRAI
      FIN SI
    FIN POUR
    passage ← passage + 1
  TANT QUE permut = VRAI
FIN PROCEDURE ;

# Tri de Shell

Donald L. Shell proposa, en 1959, une variante du tri par insertion. Ce tri consiste à trier séparément des sous-suites de la table, formées par les éléments répartis de h en h. Empiriquement, Shell propose la suite d'incréments vérifiant h1 = 1, hn+1 = 3hn+1 en réalisant les tris du plus grand intervalle possible vers le plus petit.
PROCEDURE tri_Insertion ( TABLEAU a[0:n-1], gap, debut)
  POUR i VARIANT DE debut A n-1 AVEC UN PAS gap FAIRE
    POUR k VARIANT DE i A 1 && a[k] < a[k-1] FAIRE
      ECHANGER a[k] ET a[k-1] ;
    FIN POUR ; 
  FIN POUR ;
FIN PROCEDURE ;
 
 
PROCEDURE tri_Shell ( TABLEAU a[0:n-1])
  POUR gap DANS (6,4,3,2,1) FAIRE
    POUR debut VARIANT DE 0 A gap - 1 FAIRE
      tri_Insertion(a, gap, debut);
    FIN POUR;
  FIN POUR;
FIN PROCEDURE;



# Tri par fusion

Il s’agit à nouveau d’un tri suivant le paradigme diviser pour régner. Le principe du tri fusion (ou tri par interclassement) en est le suivant :
On divise en deux moitiés la liste à trier (en prenant par exemple, un élément sur deux pour chacune des listes).
On trie chacune d’entre elles.
On fusionne les deux moitiés obtenues pour reconstituer la liste triée.

PROCEDURE Fusion ( TABLEAU gauche[0:ng-1], TABLEAU droite[0:nd-1])
  TABLEAU resultat
  ig=0, id = 0;
  TANTQUE ig < ng ET id < nd FAIRE
    SI gauche[ig] <= droite[id] ALORS
      AJOUTER gauche[ig] A LA FIN DE resultat
      INCREMENTER ig
    SINON
      AJOUTER droite[id] A LA FIN DE resultat
      INCREMENTER id
    FIN SI
  FIN TANTQUE
  AJOUTER LES ELEMENTS RESTANTS DE gauche A LA FIN DE resultat
  AJOUTER LES ELEMENTS RESTANTS DE doite A LA FIN DE resultat
FIN PROCEDURE
 
PROCEDURE tri_Fusion ( TABLEAU a[0:n-1])
FAIRE
    SI TAILLE(a)<=1 RENVOYER a
    gauche = partie_gauche de a
    droite = partie_droite de a
    gauche = tri_Fusion gauche
    droite = tri_Fusion droite
    RENVOYER Fusion (gauche, droite)
FIN PROCEDURE




# Tri rapide



Le tri rapide - aussi appelé "tri de Hoare" (du nom de son inventeur Tony Hoare) ou "tri par segmentation" ou "tri des bijoutiers" ou, en anglais "quicksort" - est certainement l’algorithme de tri interne le plus efficace.
Le principe de ce tri est d’ordonner le vecteur T.(0)..T.(n) en cherchant dans celui-ci une clé pivot autour de laquelle réorganiser ses éléments. Il est souhaitable que le pivot soit aussi proche que possible de la clé relative à l’enregistrement central du vecteur, afin qu’il y ait à peu près autant d’éléments le précédant que le suivant, soit environ la moitié des éléments du tableau. Dans la pratique, comme dans la démo ci-dessous, on prend souvent le dernier élément du tableau.
On permute ceux-ci de façon à ce que pour un indice j particulier tous les éléments dont la clé est inférieure à pivot se trouvent dans T.(0)...T.(j) et tous ceux dont la clé est supérieure se trouvent dans T.(j+1)...T.(n). On place ensuite le pivot à la position j.
On applique ensuite le tri récursivement à, sur la partie dont les éléments sont inférieurs au pivot et sur la partie dont les éléments sont supérieurs au pivot.
Procedure tri_rapide (tableau [1:n], gauche, droit )
DEBUT
  (* mur marque la separation entre les elements plus petits et ceux plus grands que pivot*)
  mur ← gauche;
  (* On prend comme pivot l element le plus a droite *)
  pivot ← tableau[droit];  
  placer a gauche de mur tout les elements plus petits
  placer a droite de mur tout les element plus grands
  (* On place correctement le pivot *)
  placer le pivot a la place de mur
  (* On poursuit par recursivite *)
  SI (gauche<mur-1) ALORS tri_rapide(tableau,gauche,mur-1);
  SI (mur+1<droit) ALORS tri_rapide(tableau,mur,droit);
FIN;

3-9-7-1-6-2-8-4-5

