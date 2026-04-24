# Adaptation_moteurs_brushless

Objectif du système (boucle de régulation) :

<img width="1357" height="1000" alt="image" src="https://github.com/user-attachments/assets/670a7ad8-7ef2-435a-99d4-41d0409d372d" />

Le but est de piloter un moteur brushless via une carte ESC (Electronic Speed Controler) puis de récupérer la vitesse du moteur via des sondes à effet Hall grâce à un STM32.
Ce STM32 ainsi que l'ESC et le Jetson Nano seront connectés entre eux grâce au protocole de communication CAN.

L'ESC utilisé sera le B-G431B-ESC1 (https://www.st.com/en/evaluation-tools/b-g431b-esc1.html).

Une boite à été designée pour protéger l'ESC d'éventuels court-circuits.

<img width="1033" height="709" alt="image" src="https://github.com/user-attachments/assets/ac81bfdd-0547-4e7b-a71d-6a91a2f58c63" />

[Partie basse de la boite](Modélisation_3D/box_part_bas.stl)
[Partie haute de la boite](Modélisation_3D/box_part_haut.stl)

Moteurs Brushless utilisés : BDUAV 6384-120KV SPECS (moteurs de skate électrique achetés sur Amazon, no name, très peu d'infos disponibles, pas de datasheet)

<img width="1874" height="1008" alt="image" src="https://github.com/user-attachments/assets/6f4d671d-e316-4980-84da-78550ce454ea" />

Adaptation transmission : 

<img width="1445" height="919" alt="image" src="https://github.com/user-attachments/assets/72ead0b2-9925-45b0-b129-29d0fefd4bd7" />

L'enjeu était de pouvoir rempalacer les MCC par des Brushess. Il a donc fallut adapter la transmission. Pour cela nous avons modélisé deux disques qui venaient se fixer un sur le moteur Brushless et l'autre sur la gearbox. La liaison entre les deux tubes était effectuée par des tiges en métal sur les abords des diques et les deux axes de rotations de diamètres différents sont accouplés en utilisant un coupleur comme celui ci-dessous.

<img width="405" height="468" alt="image" src="https://github.com/user-attachments/assets/177b820f-1acd-45e8-991e-a7f13d73ba7b" />

Les gearbox ont été usinés pour acceuillir 4 trous de fixation et les disques d'adaptation ont été imprimés en carbone.

Le système final qui tourne : 

https://github.com/user-attachments/assets/686f73e8-d420-4f12-8da8-5dcabd13b730

Le système une fois remonté dans l'habitacle du robot : 

https://github.com/user-attachments/assets/fa4666f8-0b14-431a-903d-8bc15e6b51ce

Détermination des caractéristiques techniques du moteur : 

<img width="1331" height="695" alt="image" src="https://github.com/user-attachments/assets/3905344a-de6f-4a2d-bd7b-8bcc2d8c8e26" />

Conception d'une carte de distribution de la puissance pour centraliser toute la partie puissance et éviter des brancehment en parallèle "sauvages":

Schématique : 

<img width="1616" height="1118" alt="image" src="https://github.com/user-attachments/assets/a8bc9cc6-16c7-4d86-925f-d2657bb849fd" />

Routage :

<img width="1071" height="850" alt="image" src="https://github.com/user-attachments/assets/1840974d-d962-4d24-8be1-dc4cecd5a58a" />

PCB : 

<img width="1420" height="1090" alt="image" src="https://github.com/user-attachments/assets/e972d538-4978-42e6-9a64-632374000bc2" />

La carte permet d'importer directement de la batterie et des transformateurs les 3 tensions du robot à savoir Vbatt, +12V et +8,4V via les 3 connecteurs XT60 sur la gauche.
Puis elle permet de redistribuer cette énergie via des connecteurs XT60 et des borniers avec le Vbatt sur la partie haute, le 12V au centre et le 8,4V sur le bas et le haut du PCB.
Il y a également de entrées PWM pour les Servos Moteurs.

Software (tuto) :

<img width="360" height="356" alt="image" src="https://github.com/user-attachments/assets/a1348207-d66c-4562-838d-951411b2baff" />

On lance d’abord motorControl Workbench > Load project là vous mettez le fichier BON_MOTEUR.stwb6. Et ça vous ouvre directement la page(Image ci-dessous).

<img width="932" height="488" alt="image" src="https://github.com/user-attachments/assets/219ba486-bc4a-4dba-9ce3-5689575fc156" />

A gauche vous avez les paramètres que vous pouvez modifier etc. Pour lancer motor Pilot il faut Generate the Project :

<img width="623" height="347" alt="image" src="https://github.com/user-attachments/assets/336e2e85-7cd6-46a9-8f2a-2a149682e1bc" />

Cliquer sur generate ça le genére (si vous voyez des lignes orange pas d’inquiétude). Une fois la génération finit,il vous suffit d’appuyer sur Run STM32CubeMx.
A ce stade normalement, unpage STM32CubeMx se lance appuyer sur Generate the code. Ensuite, appuyer sur ouvrez un fichier c de la barre à gaucheet appuyez sur RUN.
Pendant ce temps vous pouvez lancer motorpilot via motor Control workbench (bouton à coter de
Generate the project).
Remarque, l’application qui se lancera va dépendre de ce que vous avez cocher dans Application
Configuration.

<img width="978" height="556" alt="image" src="https://github.com/user-attachments/assets/37074cc7-484a-47be-a8ed-56b2d193a043" />

Dans tous les cas, ceci est la page de base:

<img width="810" height="481" alt="image" src="https://github.com/user-attachments/assets/4f08bcd8-9cfe-4306-828c-cac592c6c6c8" />

<img width="343" height="245" alt="image" src="https://github.com/user-attachments/assets/688a07f7-07ba-4905-9969-83b40cafbf7f" />

Vous pouvez aussi tout contrôler en haut à gauche avec GUI. Enfin, si vous choisissez Load UI il faut choisir le fichier MC_FOC_SDK pour avoir l’interface suivante et contrôler le moteur:

<img width="812" height="431" alt="image" src="https://github.com/user-attachments/assets/b86807e8-6179-448a-94b0-5f987a30a45a" />

Dans l’onglet Control vous pouvez choisir de le contrôler en Torque ou en Speed. Si jamais vous avez un problème de over current, il faut régler le problème ici :

<img width="758" height="613" alt="image" src="https://github.com/user-attachments/assets/f0a8ee58-4251-45f9-bcdc-635473ea3c80" />

Dans Digital Filter Duration, il faut augmenter le temps ici j’ai mis 282.35 ns.

REMARQUE IMPORTANTE : IL FAUT à CHAQUE FOIS RE-GENERATE the project > Run
STM32CubeMx > Generate the code > Run un fichier C POUR CHAQUE CHANGEMENT QUE
VOUS FAITES DANS LE SOFTWARE MC WORKBENCH. (En tout cas c’est la seule façon avec
laquelle on arrivait à faire en sorte que les changements dans le software soit pris en compte si
jamais vous trouvez une autre méthode plus court, bien joué).

J’ai fournit les fichier JSON obtenu via MOTOR Profiler. Libre à vous de tester et d’observer les
mesures. Ce software permet d’identifier les « composants » et leurs valeurs du moteur et faute de
datasheet sur les moteurs commandées, on a du faire avec les moyens du bord.



