Requête SQL


1. Affichez les libellés des machines des fabricants localisés à Marseille

SELECT Libellé, fabricant.Coordonnées FROM `machine` JOIN fabricant ON machine.Id_fabricant = fabricant.n°Fabricant WHERE fabricant.Coordonnées LIKE "%Marseille%";

2. Affichez le nom et le prénom des opérateurs qui sont intervenus sur les machines 217, 245, 236, 287

SELECT operateur.Nom, operateur.Prénom FROM operateur JOIN fichepanne ON operateur.n°Operateur = fichepanne.Id_Operateur WHERE fichepanne.Id_Machine IN (217, 245, 236, 287);

3. Trouvez les types de pannes qui affectent les machines du Fabricant « FFX »

SELECT typepanne.LibelléPanne FROM typepanne JOIN fichepanne ON typepanne.n°TypePanne = fichepanne.Id_TypePanne JOIN machine ON machine.n°Machine = fichepanne.Id_Machine JOIN fabricant ON fabricant.n°Fabricant = machine.Id_fabricant WHERE fabricant.Nom LIKE "FFX"


4. Changez le nom de la Soudeuse X100 qui s’appelle désormais « Soudeuse RMX100 »

UPDATE machine
SET Libellé = 'Soudeuse RMX100'
WHERE Libellé = 'Soudeuse X100';


5. Affichez la liste des fiches de panne du 1 er semestre 2019 pour la machine n° 440

SELECT typepanne.LibelléPanne 
FROM fichepanne
JOIN typepanne ON typepanne.n°TypePanne = fichepanne.Id_TypePanne 
WHERE fichepanne.Id_Machine = 440 
AND fichepanne.DateDébut
BETWEEN "2019-01-01" AND "2019-07-01"

6. Affichez la liste des machines achetées en 2006 ayant été affectées par le type de panne « fuite »

SELECT fichepanne.Id_Machine, typepanne.LibelléPanne 
FROM fichepanne JOIN typepanne 
ON typepanne.n°TypePanne = fichepanne.Id_TypePanne 
JOIN machine ON machine.n°Machine = fichepanne.Id_Machine WHERE machine.DateAchat 
LIKE "2006%" AND typepanne.LibelléPanne = "Fuite";


7. Ajoutez-vous à la liste des opérateur

INSERT INTO operateur ("Nom","Prénom") 
VALUES ("Huin" , "Alexis")

8. Sortir la liste des opérateurs qui ne commentent pas leurs fiches de panne

SELECT operateur.Nom, operateur.Prénom
FROM fichepanne
JOIN operateur ON operateur.n°Operateur = fichepanne.Id_Operateur
WHERE fichepanne.Commentaire = ""
if a = 0 && a = 1

9. Sortir les informations de la machine WXFD144454 : libellé, fabricant, nombre de pannes

SELECT machine.n°Serie, machine.Libellé, fabricant.Nom, 
COUNT(fichepanne.Id_Machine) AS NbPanne 
FROM fichepanne 
JOIN machine ON machine.n°Machine = fichepanne.Id_Machine 
JOIN fabricant ON fabricant.n°Fabricant = machine.Id_fabricant 
WHERE machine.n°Serie = "WXFD144454" 
GROUP BY machine.n°Serie, machine.Libellé, fabricant.Nom;


10. Sortir le n°Fiche, date_début,datecloture,nom operateur, prénom operateur pour les machines des
fabricants « TR.P» et « ORF-FEDEX »

SELECT fichepanne.n°FichePanne, fichepanne.DateDébut, fichepanne.DateCloture, operateur.Nom, operateur.Prénom, fabricant.Nom AS Fabricant 
FROM fichepanne
JOIN operateur ON operateur.n°Operateur = fichepanne.Id_Operateur
JOIN machine ON machine.n°Machine = fichepanne.Id_Machine
JOIN fabricant ON fabricant.n°Fabricant = machine.Id_fabricant
WHERE fabricant.Nom = "TR.P" OR fabricant.Nom = "ORF-FEDEX"

11. Indiquez le nombre de fabricants présent à Lens

SELECT COUNT(fabricant.Coordonnées) AS NmDeFabricant
FROM fabricant
WHERE fabricant.Coordonnées LIKE "%Lens%"


12. Affichez la liste des machines avec l’année d’achat et le nom du fabricant



13. Affichez la liste des fiches non clôturées ( date NULL) sous la forme suivante : n°Fiche Nom opérateur,
prénom operateur, nom fabricant, type de pane


14. Affichez le nombre de machines achetées par année


15. Affectez les interventions de Roseline OCLOO à Myriam SOK. Supprimer ensuite de la base Roseline OCLOO


16. Changez l’adresse du fournisseur BRUNET qui est désormais localisé « ZI Nord emplacement 3 – Rue de lievin
– 62300 Lens »


17. Ajoutez le type de panne « carte electronique HS »


18. Affichez le nombre de panne traitées par opérateur, classé en décroissant


19. Trouvez si une machine est tombée en panne le jour de votre anniversaire et qui est intervenu dessus


20. Le fabricant 25 ( BRUNET) a fusionné avec le fabricant 22 ( BAUM) pour créer l’entité « BAUM-BRUNET « ,
localisée 47 boulevard de l’industrie 41100 Vendome. Effectuer les opérations dans la base permettant
d’acter ce changement