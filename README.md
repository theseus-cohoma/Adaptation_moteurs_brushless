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

