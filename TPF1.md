
```python
from quote import quote
from pprint import pprint
from collections import OrderedDict

#A l'aide du package `quote`, obtenable avec `pip`, extraire 30 citations d'un des écrivains présents dans la liste suivante.
search = 'Arthur Schopenhauer'
result = quote(search, limit=30)
#pprint(result)

# Fonctions utilisées pour les concepteurs d'inventaires
def affichage_decroissant(liste) : # affiche une liste, classée de manière décroissante par rapport à ses valeurs (pas ses clés)
	pprint(sorted(liste.items(), key=lambda x:x[1], reverse=True))

# ajout d'une occurence dans un dictionnaire(liste), après vérification de non-nullité
def ajout_occurence(nom,liste) :
	if nom != "" :
		if nom not in liste:
			liste[nom] = 1
		else:
			liste[nom] += 1

# copie des éléments d'un dictionnaire source vers un dictionnaire cible, à condition que leur valeur soit supérieure à 5
def copier_elements_sup_a_cinq(source,cible) :
	for element , valeur in source.items() :
		if valeur >= 5:
			cible[element] = valeur

#Concevoir un inventaire des titres de livres classés par fréquence d'apparition dans le résultat en ordre décroissant.

# création de la liste récipiendaire des informations sur les titres de livre, et remplissage
liste = dict()
for element in result :
	ajout_occurence(element["book"],liste)
# affichage de cette liste
affichage_decroissant(liste)

#Dresser un inventaire des mots classés par ordre décroissant de présence dans les citations. Ne pas afficher les mots présents moins de 5 fois.

# création de la liste récipiendaire des informations sur les citations, section des citations en mots exploitables, et remplissage		
liste = dict()
for element in result :
	mots = element["quote"].split()
	for mot in mots :
		ajout_occurence(mot,liste)

# création de la liste contenant les mots apparaissant au moins cinq fois, et copie de ces informations depuis la liste liste le cas échéant
liste_epuree = dict();
copier_elements_sup_a_cinq(liste,liste_epuree)
# affichage de cette liste.
affichage_decroissant(liste_epuree)



```