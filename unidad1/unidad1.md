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
Ubuntu, en la seva major part, té un llicenciament GPL és a dir _General Public License_. Té un ús gratuït, es pot modificar al teu gust, pots redistribuir-lo amb les teves modificacions, inclús el codi font d'Ubuntu ha d'estar públicat. En cas de fer una redistribució d'un Ubuntu modificat, no podem donar-li el nom d'ubuntu, però no podrem obtenir beneficis econòmics gràcies a aquest.

## Gestors d'arrencada per a instal·lacions duals.
En aquest apartat del sprint realitzarem dues instal·lacions duals, una amb un sol disc, i una altra dual amb dos discos. Realment és molt més còmode tenir dos discos, un per a cada sistema operatiu, perquè aixi no desaprofitem espai de cap disc.

### Instal·lació dual amb un sol disc
Començarem amb un sol disc, farem que cada vegada que arranqui la màquina virtual, puguem seleccionar amb el GRUB si arrencar amb Windows o amb Ubuntu, jo utilitzaré un ubuntu 22 i un Windows 10 enterprise. En teoría, el senzill és primer instal·lar el sistema operatiu Windows, i després Ubuntu, però nosaltres ho farem al revés, ja que, sinó no té gràcia i se'ns podria donar el cas de només tenir un disc amb un Ubuntu ja instal·lat.

Primer de tot, necessitarem una màquina creada de Ubuntu 22 que funcioni correctament. I col·locarem la ISO del Windows.

<img width="577" height="397" alt="1" src="https://github.com/user-attachments/assets/17bc5dc0-9ee4-4510-b154-980ef281481c" />

Per a que el sistema Windows no ens doni problemes amb el sistema de particions, perquè Ubuntu utilitza GPT, però Windows vol MBR. Llavors haurem de marcar la casella de UEFI dintre de la nostra màquina. 

<img width="1060" height="616" alt="3" src="https://github.com/user-attachments/assets/06be9344-70db-4a2a-bb80-874ddffba5fa" />

Un cop arrencada la màquina observem que no se'ns dona la opció de arrencar l'ubuntu, sinó que s'obre Windows directament, a punt per a preparar-lo per a la seva instal·lació. Seleccionem l'idioma i "Instalar Ahora". Després d'això seleccionem uns instal·lació personalitzada perquè voldrem posar el sistema Windows en una partició en específic.

<img width="640" height="484" alt="2" src="https://github.com/user-attachments/assets/f4328266-2297-49f4-99cd-8746589c2d60" />

Seleccionem que s'instal·li windows a la partició 6, que es la que haviem deixat 40 GB lliures anteriorment.

<img width="642" height="479" alt="4" src="https://github.com/user-attachments/assets/b3b9f8dc-65a5-48b5-93f5-298885cd17e5" />

Ara esperem a que s'instal·li el sistema operatiu Windows

<img width="645" height="479" alt="5" src="https://github.com/user-attachments/assets/1b974919-77b3-4b1e-be04-00b91347afce" />

En haver instal·lat el Windows, se'ns demanarà que fessim una configuració bàsica (Usuari, contrasenya, si volem donar accés a la ubicació...) tot aixo al gust de l'usuari. I després d'un poc temps, ja tindrem el windows llest. 

<img width="1024" height="857" alt="6" src="https://github.com/user-attachments/assets/fb3dcbfa-c41c-4c26-97da-dfb237155907" />

Ara, comença el problema "On és el meu ubuntu?" "Per què no em deixa triar Ubuntu?" És senzill, la resposta és que Windows es carrega el grub del Ubuntu, però es pot solucionar, en iniciar la màquina premem repetidament ESC/F12 i se'ns obrirà un menú. Seleccionarem l'opció de boot manager.

<img width="847" height="254" alt="7" src="https://github.com/user-attachments/assets/f905b7aa-3fa5-49bb-9057-d7eb0cfd3d3f" />

Arranquem amb Ubuntu.

<img width="487" height="249" alt="8" src="https://github.com/user-attachments/assets/84febf30-f96c-4793-a2ac-0a3d4655dc02" />

Ja estarem dintre del nostre sistema Ubuntu, ara iniciem la sessió dintre de Ubuntu i obrim un terminal, amb les següents comandes

```
sudo update-grub
sudo grub-install /dev/sda
```

<img width="737" height="483" alt="9" src="https://github.com/user-attachments/assets/2ca94d18-344a-463c-94ec-11a6fe5f402b" />

He tingut algun problemeta perquè al reiniciar la màquina només em detectava ubuntu, he estat mirant i la solució és editar el fitxer _/etc/default/grub_ i afegir la línea següent:

```
GRUB_DISABLE_OS_PROBER=false
```
i després tornem a fer un sudo update-grub per a tornar a reiniciar la màquina.

<img width="698" height="398" alt="10" src="https://github.com/user-attachments/assets/68dcaaff-9ead-41ef-ac11-8aa25a726ab6" />


Com podem observar, en reiniciar la màquina ja ens apareix per a arrencar o amb Windows o amb Ubuntu.

<img width="632" height="277" alt="11" src="https://github.com/user-attachments/assets/92d4af17-a395-4e5d-b95e-82f4f5d187fe" />


## Punts de restauració.
Mitjançant el programa timeshift, realitzarem punts de restauració en el nostre sistema operatiu Ubuntu.

Evidentment, el primer que farem serà instal·lar Timeshift dintre de la nostra màquina virtual. 

<img width="637" height="147" alt="image" src="https://github.com/user-attachments/assets/de50b151-bdc8-4df3-8dd5-89e197efc088" />

Ara, seleccionem el tipus de instantània que volem

<img width="520" height="201" alt="image" src="https://github.com/user-attachments/assets/6a87cced-5bf9-4dd2-98e8-124ed15437de" />

Le localització de la instantània

<img width="735" height="204" alt="image" src="https://github.com/user-attachments/assets/8c59380d-ba6f-477f-9733-320dde6b8be8" />

Quan volem que es faci cada instantània, jo crec queseía recomanable cada boot.

<img width="411" height="295" alt="image" src="https://github.com/user-attachments/assets/ba68c5ea-81ed-43f7-8094-e8b33802650f" />

Voldrem que nomes s'agafin els arxius de la home del meu usuari

<img width="597" height="154" alt="image" src="https://github.com/user-attachments/assets/fe62e7df-f528-4333-87d9-b8f16a0135d9" />

En teoria, per cada vegada que arranquem el sistema es fa una còpia de seguretat, però també la podem fer manualment. 

<img width="790" height="629" alt="image" src="https://github.com/user-attachments/assets/62319ce0-97b1-4202-bf11-12b56cce17d0" />

Pero abans de crear-la, creem uns arxius per a comprovar que funciona correctament. He creat una carpeta que es diu adeu, i un fitxer que es diu hola.

<img width="503" height="70" alt="image" src="https://github.com/user-attachments/assets/dd104cdb-e1b4-4149-b25c-8187b920b975" />

Ara si, ja podem crear la instantànea

<img width="499" height="602" alt="image" src="https://github.com/user-attachments/assets/74813232-f904-45d3-a940-a650f06152bc" />

Com podem observar, ja la tenim instal·lada. Ara borrem els fitxers creats anteriorment.

<img width="784" height="324" alt="image" src="https://github.com/user-attachments/assets/3194cdbd-9dd0-43e9-89a6-aecd2c11c6d7" />

<img width="404" height="89" alt="image" src="https://github.com/user-attachments/assets/42035951-f479-4b55-88b3-d982614c56f8" />

Restablim la instantània, i ens avisa dels arxius que modificarà
<img width="502" height="310" alt="image" src="https://github.com/user-attachments/assets/d20dc0dd-53fe-4711-802b-9f191110df16" />

I comença a fer-se la restauració, després d'això es reinicia el sistema
<img width="741" height="259" alt="image" src="https://github.com/user-attachments/assets/6370747b-1747-4e49-b70e-929243c86dcc" />

Comprovem que s'hagin restaurat els arxius, tornen a estar hola i adeu.
<img width="544" height="97" alt="image" src="https://github.com/user-attachments/assets/89ed5832-cffb-49eb-ac5b-7d1aa1f85606" />


## Configuració de la xarxa
Quan creem una màquina virtual, hem d'establir un tipus de xarxa, nosaltres explicarem els 4 més importants i quina és el més recomanable per a aquest tipus de pràctiques. 

- **NAT**: La màquina comparteix connexió directa amb el nostre ordinador. Però no tenim connexió a xarxa

- **Adaptador Pont**: La màquina es comporta com un equip més dintre de la xarxa, però és molt incòmoda perquè no te una IP fixa i pot canviar.

- **Xarxa Interna**:La màquina només pot comunicar-se amb altres màquines que estiguin a la mateixa xarxa interna.

-  **Xarxa NAT**: La màquina pot comunicar-se amb el nostre i ordinador, però també a la xarxa.

D'aquestes 4 opcions, la més òptima és la Xarxa NAT, degut a que podem instal·lar i actualitzar paquets quan vulguem (Tenim connexió a xarxa), també tenim connexió directa al nostre ordinador, i a més gràcies a això no exposem la màquina a la LAN de la nostra xarxa. A part de tot això, també l'escollim perquè la IP es pot fer fixa, i a mi em convé bastant perquè treballo amb un disc que te ubuntu instal·lat, i cada dia puc estar a un ordinador diferent, en cas de que no tingues una IP fixa (Adaptador Pont) la IP canviaria en qualsevol moment. 

## Comandes generals i instal·lacions.

apt cache policy, configuracio del preferences.d, apt-cache policy "paquet" apt install
