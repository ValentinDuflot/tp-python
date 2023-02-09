```python
import pprint as pprint
import csv as csv

# on ouvre le fichier et crée un dictionnaire avec ses informations
input_file = csv.DictReader(open(r"D:\USERS\Documents\obs\python\titanic_survival.csv"))

# Moyenne d'âge des passagers (~30 ans)
# ce code est trop simple pour requérir des commentaires supplémentaires
sommeAge = 0;
sommePassagers = 0;
for row in input_file:
	if row["age"] != "" : # verification que l'age est non nul
	    sommeAge += float(row["age"])
	    sommePassagers += 1
print(sommeAge/sommePassagers)


#Pourcentage de survie par classe de passager (~62% pour la première classe, ~43% pour la deuxième classe, ~26% pour la troisième)
# on définit les variables pour le nombre de sauvés et le nombre de personnes totales, pour les trois classes
compteur_classe_un = 0
compteur_survi_un = 0
compteur_classe_deux = 0
compteur_survi_deux = 0
compteur_classe_trois = 0
compteur_survi_trois = 0

# on balaye la liste des passagers, on compte le nombre par classe et le nombre de survivants par classe
for row in input_file:
	if int(row["pclass"]) == 1:
		compteur_classe_un += 1
		if int(row["survived"]) == 1 :
			compteur_survi_un += 1
	if int(row["pclass"]) == 2:
		compteur_classe_deux += 1
		if int(row["survived"]) == 1 :
			compteur_survi_deux += 1
	if int(row["pclass"]) == 3:
		compteur_classe_trois += 1
		if int(row["survived"]) == 1 :
			compteur_survi_trois += 1

# on affiche les resultats demandés
print( "pour la première classe " , (compteur_survi_un / compteur_classe_un)*100 , "% de survie")
print( "pour la deuxième classe " , (compteur_survi_deux / compteur_classe_deux)*100 , "% de survie")
print( "pour la troisième classe " , (compteur_survi_trois / compteur_classe_trois)*100 , "% de survie")

#Le bateau de sauvetage ayant sauvé le plus de passagers (bateau n°13 avec 39 passagers sauvés)

# ajout d'une occurence dans un dictionnaire(liste), après vérification de non-nullité
def ajout_occurence(nom,liste) :
	if nom != "" :
		if nom not in liste:
			liste[nom] = 1
		else:
			liste[nom] += 1

# liste contenant les informations sur les canots de sauvetage.
liste = dict();

# pour chaque personne sauvée, on sauvegarde sur quel canot de sauvetage elle était
for row in input_file:
	if int(row["survived"]) == 1 :
		ajout_occurence(row['boat'],liste)

# on balaye la liste des canots pour trouver celui qui a sauvé le plus de monde
meilleur_canot = ""
performance_meilleur_canot = 0;
for element, valeur in liste.items() :
	if performance_meilleur_canot == 0 : # pour sauvegarder dans les variables de comparaison une première valeur
		meilleur_canot = element
		performance_meilleur_canot = valeur;
	if valeur > performance_meilleur_canot :
		meilleur_canot = element
		performance_meilleur_canot = valeur;
		

# et on l'affiche.
print(meilleur_canot , " avec " , performance_meilleur_canot , " sauvés.")



```