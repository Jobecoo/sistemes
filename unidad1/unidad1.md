---
layout: default
title: "Sprint 1. Instal·lació i configuració inicial"
---

## Virtualització i instal·lació del sistema operatiu Ubuntu.
En aquest apartat realitzarem una instal·lació del sistema operatiu ubuntu 22 dintre del programa Virtual Box, aquesta màquina és la que utilitzarem durant tot el curs com a plantilla. 

Per començar la creació de la màquina virtual primer pujarem la ISO del ubuntu 22 en l'apartat de "New", li posem el nom que vulguem a la màquina i després és molt important que per aquesta pràctica hem de desseleccionar l'opció de "Skip unattended installation" perquè així podrem fer una instal·lació personalitzada i nosaltres mateixos podrem crear les particions, usuari...

<img width="944" height="620" alt="1" src="https://github.com/user-attachments/assets/bc5a10e6-8845-4b60-a7bd-9294cc1abdc8" />

Després de posar-li el nom a la màquina, anem al apartat "Specify virtual hardware" aquí establirem tant la memòria RAM com els nuclis de CPU que voldrem per a la nostra màquina. He estat buscant en les pàgines d'ubuntu i el mínim normalment s'estableix amb 2 cores i 4 de RAM, però per a que la màquina vagi una mica més fluida he posat el doble a cadascún dels dos apartats. No us preocupeu amb això ja que es pot canviar en qualsevol moment. Però si hem de tenir més d'una màquina engegada no hauriem de posar tants de recursos per a la màquina, tot depenent del nostre ordinador.

<img width="948" height="625" alt="2" src="https://github.com/user-attachments/assets/a15fc521-d63c-41f0-ab74-bd222e8915a3" />

Un cop ja tenim la RAM i els cores establerts, en l'apartat "Specify Virtual hard disk" establirem la mida del disc de la nostra màquina. Es recomana que sigui una mida una mica gran, però no us preocupeu perquè si necessiteu més espai, podeu afegir mes discs.

<img width="948" height="623" alt="3" src="https://github.com/user-attachments/assets/0a4329d6-05c7-42c5-8105-5257e1dfd96d" />

Un cop ja tenim la mida del disc definida, Clicarem el botó finish i ja podrem obrir la nostra màquina fent doble clic sobre aquesta. Després d'uns segons s'ens obrirà una pestanya que serà la nostra nova màquina virtual.
Ara es moment d'instal·lar-la, i com diu el nom, haurem de triar l'opció "Install Ubuntu".

<img width="874" height="671" alt="4" src="https://github.com/user-attachments/assets/acb36115-209f-47e2-8966-44e7e9bd9f28" />

Continuem la instal·lació normal fins que arribem a l'apartat "Installation type" I seleccionem l'opcio "Something else" perquè voldrem crear les nostres pròpies particions per a saber com funcionen.

<img width="831" height="706" alt="5" src="https://github.com/user-attachments/assets/f2f8552c-e8ca-454c-82a6-3a7913537349" />

Ara ja estem dintre del menú de particions, podem crear una nova taula de partiions amb l'opció "New Partition Table". Ens saltarà una advertència de que el disc es borrarà al complet, però a nosaltres no ens importa ja que la màquina és nova, per tant, el disc és nou. Un cop tenim la taula de particions creada, ja podrem definir totes les nostres particions del disc.

<img width="827" height="623" alt="6" src="https://github.com/user-attachments/assets/863d62df-70ed-4859-b28b-542fceb6a418" />

És molt important saber que per a crear una partició, hem de seleccionar el botó de "+" en la taula de particions. Podem tenir diverses, ara, us explicaré les més bàsiques i necessàries:

**/ (arrel)**: Aquesta és la part que conté tot el sistema operatiu, on guardem tots els arxius. La mesura recomanada per a l'arrel és entre uns 15-30 GB de memòria, depenent del ús que li volguem donar. Com que no hem de fer cap instal·lació pesada, de moment nosaltres li establirem uns 20 GB

**/boot** : Conté el kernel, el initrd, i els arxius necessaris per a arrencar el sistema. La mesura recomanada són entre uns 500 MB i 1 GB. Establirem 1 GB per a ahorrar-nos desgràcies a llarg termini.

**/home**: Aquí hi ha els fitxers personals dels usuaris: documents, descàrregues, configuració d'escriptori. És bona pràctica tenir-lo separat per poder reinstal·lar el sistema sense perdre dades. Com que en l'activitat se'ns ha ordenat deixar uns 40 Gb d'espai lliure, li donarem 15 GB de memòria, però normalment s'estableix tot el que queda de disc. 

**swap**: La swap realment sí es recomana, normalment alrededor d'uns 4-8 GB. Però si hem d'hivernar* (que no és el nostre cas) s'hauría de posar una swap més gran que la memòria RAM. La swap serveix com un coixí per a la memòria RAM del nostre equip utilitzant la swap per quan la nostra RAM s'acaba.

**efi**: És necessària si has d'arrancar el sistema amb UEFI, es recomana uns 300-600 MB d'emmagatzematge. 

<img width="833" height="625" alt="7" src="https://github.com/user-attachments/assets/0d6c1850-f075-4cb1-8450-eecfa5ee9745" />

Un cop ja tenim les particions creades, ja podrem definir el nostre nom d'usuari i la nostra contrasenya, jo li he posat Joan, però cadascú pot posar-se el nom que vulgui

<img width="828" height="627" alt="8" src="https://github.com/user-attachments/assets/3aa2f2c8-f0e3-46fb-a494-c2846aabb185" />

***Hivernar**: Aquest concepte l'he tingut que buscar perquè les meves fonts de recerca insistien molt que en el cas d'hivernació, la swap hauria de ser bastant alta. Hivernar serveix per a apagar l'ordinador, però la informació de la RAM en comptes d'eliminar-se, es guarda dintre del disc i s'apaga per complet, llavors, quan tornem a enjegar l'ordinador continúes exactament on ho havies deixat. 

## Llicènciament.
Explicar la llicència del SO Ubuntu 
## Gestors d'arrencada per a instal·lacions duals.
## Punts de restauració.
## Configuració de la xarxa
Nat, Adaptador pont, xarxa interna, xarxa nat. Explicar per què xarxa nat i no una altra. 
## Comandes generals i instal·lacions.

Modificar llicencia github a la cc 4.0 fet
A l'apartat de llicenciament de l'esprint 1 parlar de la llicencia d'ubuntu 
Crear una maquina virtual i explicar la seva configuracio
Instal·lar SO Ubuntu i decidir particions en captures
Redactar al github
