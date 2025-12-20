# Sprint 2:

# Instal·lació, configuració de programari de base i gestió de fitxers.

## Sistemes de fixers i particions

### Mida sector

El sector és la unitat mínima física on es guarden les dades en un disco. I per defecte són 512 Bytes. Aquesta mida no es pot canviar, tots els discos tenen aquesta mida per defecte. 

### Mida bloc

Un bloc es la mida mínima lògica on es guarden las dades en el nostre SO, té una mida de 4096 per defecte. Aquesta mida sí es pot canviar, només quan formatem el disc. El nostre SO per defecte agarra 8 sectors per bloc.
La mida de bloc, així com el sistema de fitxers pot ser diferent a cada partició del disc.

  - Fragmentació interna

La fragmentació interna es quan es desaprofiten blocs del disco perquè els blocs són massa grans per al que s'ha d'emmagatzemar a dintre.
  
  - Fragmentació externa

A mesura que vas treballant el sistema, els arxius es van separant en diferents blocs, 
  
### Tipus de formatieg

Aquí tenim els diferents tipus de sistemes de formateig.
      
  - Baix nivell
   
Borra fitxers, el sistema fitxers i si troba algun sector defectuós els intenta reparar.

  - Mig nivell
      
Borra el sistema de fitxers, però si troba algun sector defectuós, el marca per a no guardar fitxers dintre.

  - Alt nivell
   
Només borra el sistema de fitxers.

  - Gestió de particions
      - GPARTED
      - Comandes


Una partició és un tros físic de disc, però el volum és una agrupació de particions lògiques. És afegir una capa d'abstracció damunt de les particions.

## Pràctica

Aquí podem comprovar com creem un arxiu anomenat "adeu" amb el text "Bon dia" dintre. Mirem cuants bytes ocupa i ens mostra que ocupa 8 bytes, però la seva mida del sector es de 4096 bytes, és a dir, que estem desaprofitant espai.

<img width="403" height="160" alt="image" src="https://github.com/user-attachments/assets/7baa6820-ce85-45fa-ad96-71822a2827b1" />

Si fem

```
fdisk -l
```
podrem observar la nostra mida del sector del disc per defecte

<img width="548" height="129" alt="image" src="https://github.com/user-attachments/assets/f733e4b1-f589-47f6-8411-46d6076857ef" />

Per a poder treure la mida del bloc de cada partició, utilitzant tune2fs podem observar que el nsotre disc sda3 te la mida de bloc de 4096

<img width="525" height="75" alt="image" src="https://github.com/user-attachments/assets/5a845332-eeb0-4548-aa6d-aa1cd3244dec" />

Si volem saber si és necessari desfragmentar el sistema.

<img width="1117" height="368" alt="image" src="https://github.com/user-attachments/assets/52f75020-3966-400a-b507-aa3c789a5643" />

Si volem desfragmentar és la mateixa comanda però sense el -c

<img width="1068" height="420" alt="image" src="https://github.com/user-attachments/assets/10b3581b-46f9-43d4-924e-fcceb93a2a4d" />

### Particions

Per a realitzar particions podem utilitzar gparted, és una eina uqe ens crear particions però no permet canviar la mida del bloc. 

<img width="775" height="538" alt="image" src="https://github.com/user-attachments/assets/3a5a3f47-7958-48f0-b524-eafb2ba0fe53" />

### Particions per comandes

Amb l'eina fdisk podem crear particions per comandes.

<img width="867" height="430" alt="image" src="https://github.com/user-attachments/assets/560e3371-84be-4c02-b868-647dc0cce8d0" />

Ara creem una segona partició i guardem.

<img width="793" height="316" alt="image" src="https://github.com/user-attachments/assets/6cb0f7e6-49fa-466a-960d-81fa21e34f93" />

Com podem observar, aquí tenim les dues particions.

<img width="555" height="214" alt="image" src="https://github.com/user-attachments/assets/3191553a-a376-4c85-ae8a-47ac20920adc" />

Canviem la mida del bloc del sdb1, per tant, passarem la mida del bloc de 4096 a 2048.

<img width="695" height="264" alt="image" src="https://github.com/user-attachments/assets/a4d4e909-445a-41a8-bccd-bf1504bbbdb6" />

Comprovem que la mida del bloc s'hagicanviat correctament.

<img width="592" height="108" alt="image" src="https://github.com/user-attachments/assets/e275f5ad-8746-485e-9783-bb9659054d1e" />

Ara canviem el sistema de fitxers de la segona partició a ntfs i comprovem que s'hagi fet correctament.

<img width="705" height="150" alt="image" src="https://github.com/user-attachments/assets/3a1d861d-7dc9-487b-a4ee-98990f7a516a" />

Per a poder fer una comprovació més visual, tenim el gparted

<img width="775" height="261" alt="image" src="https://github.com/user-attachments/assets/e5a8ee83-f44b-4e25-91aa-f45212d06c24" />


# Gestió d'usuaris i grups i permisos

definir que son usuaris i grups

### Fitxers importants

L'arxiu /etc/passwd és un fitxer important on podem observar els usuaris. 

Quan creem un uusari sempre es crea un grup amb el mateix nom uqe l'usuari, aquest grup té un numero identificador. Tots els usuaris formen part d'un grup prinicipal, només pot ser un. 

<img width="986" height="851" alt="image" src="https://github.com/user-attachments/assets/71ab9fb2-fcea-4c34-9f88-2962422d9979" />

En l'arxiu _/etc/shadow_ podem observar l'arxiu amb les contrasenyes de tots els usuaris, però aquestes sempre estarán encriptades, normalment, amb md5. Aquest arxiu també conté informació sobre la caducitat de les contrasenyes.

<img width="977" height="857" alt="image" src="https://github.com/user-attachments/assets/4a848ec2-f223-4f7a-88a7-ee2847a711b8" />

En l'arxiu /etc/group podem observar els grups. 

<img width="956" height="859" alt="image" src="https://github.com/user-attachments/assets/47bf4208-4b8e-4569-9e80-6dfd71aa33f0" />

En l'arxiu gshadow també podem observar els usuaris que formen part d'un grup. Al gshadow, a diferencia del _/etc/group_, podem observar qui és administrador del group. 

<img width="990" height="858" alt="image" src="https://github.com/user-attachments/assets/fda93481-fad0-4407-902d-1a5ab2018d4d" />

### Comandes bàsiques

Nosaltres organitzarem els nostres usuaris i grups mitjançant comandes, però existeix una eina anomenada gnome-system-tools que ens permet gestionar els nnostres usuaris d'una manera bastant còmoda, podent gestionar els permisos de l'usuari. 

<img width="1056" height="356" alt="image" src="https://github.com/user-attachments/assets/eacfc331-4a61-4636-a677-46c2b0deecba" />

Aquí podem observar com és l'eina gràficament. Podem afegir, esborrar i gestionar grups. 

<img width="652" height="437" alt="image" src="https://github.com/user-attachments/assets/12ce7e2f-c527-43f9-89d8-90446cd78883" />

Ara passem a la creació d'usuaris mitjançant comandes. Podem crear un usuari mitjançant la comanda adduser. Creem un usuari anomenat Luffy

<img width="710" height="422" alt="image" src="https://github.com/user-attachments/assets/4caad8ba-1a84-49aa-a4ef-812aff7c7bd5" />

Si anem a /etc/passwd podem observar com l'usuari Luffy s'ha creat correctament. 

<img width="460" height="66" alt="image" src="https://github.com/user-attachments/assets/3953bb6f-4354-41a9-8f78-420242e694f5" />

També podem observar que al _/etc/shadow_ està el nostre usuari Luffy

<img width="899" height="84" alt="image" src="https://github.com/user-attachments/assets/466af7a0-9ed5-4f08-ac53-bc4ffd60e3f1" />

Si fem un ls de _/home_ podem observar com l'usuari luffy té el seu propi directori 

<img width="230" height="60" alt="image" src="https://github.com/user-attachments/assets/cccc3397-7454-4347-8e73-9019be5802ca" />

No obstant, si esborrrem l'usuari luffy manté el seu propi directori

<img width="425" height="130" alt="image" src="https://github.com/user-attachments/assets/50d6453f-2f4c-4f0f-a50e-0f2b51fc8570" />

Però si fem un deluser -r luffy llavors la seva hom si que s'esborraria. Tornem a crear l'usuari luffy i ho comprovem. 

<img width="725" height="400" alt="image" src="https://github.com/user-attachments/assets/b052979f-5bde-43ac-b0d4-6035f2611e86" />

Si accedim a la home de l'usuari, podrem observar que te la seva home completa.

<img width="734" height="63" alt="image" src="https://github.com/user-attachments/assets/56221f0e-befb-450a-a2f3-93ab5d22cff2" />

També tenim l'opció d'utilitzar l'eina useradd, que ens permet crear usuaris que no hagin de accedir gràficament. 

Primer fem un useradd, amb el nom d'usuari que vulguem. De moment aquest usuari no té cap utilitat

<img width="278" height="41" alt="image" src="https://github.com/user-attachments/assets/47848aeb-757f-4148-be39-7dcf4c27e0ae" />

Podem observar que l'usuari existeix

<img width="441" height="53" alt="image" src="https://github.com/user-attachments/assets/b66e1b98-a6a2-4826-b20e-9213d2492573" />

Però no existeix el direcotri de l'usuari zoro

<img width="237" height="59" alt="image" src="https://github.com/user-attachments/assets/a66a274a-5c03-41b6-b31c-fed713239c94" />

També podem observar que el grup zoro s'ha creat

<img width="402" height="63" alt="image" src="https://github.com/user-attachments/assets/77cc22e5-83ee-4605-90d4-5c38d3ff2020" />

Ara modificarem l'usuari mitjançant l'eina usermod. Modificarem el shell. Abans teniem /bin/sh, i ara tenim /bin/bash.

<img width="427" height="80" alt="image" src="https://github.com/user-attachments/assets/a609c309-929c-4d9c-8287-9390f9f0fc5a" />

Ara creem un directori per a l'usuari zoro. Però el problema és que el propietari d'aquesta és root, i no zoro. 

<img width="514" height="180" alt="image" src="https://github.com/user-attachments/assets/8df75a2a-f17a-4d36-a7a0-4c2f48388eb5" />

Amb la comanda chown li podem canviar la propietat de la carpeta. 

<img width="511" height="150" alt="image" src="https://github.com/user-attachments/assets/7b0fb831-52f4-4c1c-ab4b-25780863e6f9" />

Per a poder accedir a l'usuari, necessitarem una contrasenya per a l'usuari Zoro. Mitjançant passwd li podem assiganar-li una

<img width="509" height="113" alt="image" src="https://github.com/user-attachments/assets/730aacf0-
582e-4cb0-847b-2a796b070808" />

I com podem observar, ja podem accedir a l'usuari Zoro

<img width="718" height="74" alt="image" src="https://github.com/user-attachments/assets/3e8093fe-4a0e-44b3-9152-252fb9797c68" />

Si volem bloquejar un usuari, podem utilitzar usermod -L. I el que fa es posar un "!" a l'encriptació del _/etc/shadow_.

<img width="879" height="116" alt="image" src="https://github.com/user-attachments/assets/51410fe8-254b-4729-859b-221d88138ecc" />

I per a desbloquejar l'usuari, amb usermod -U i podrem tornar accedir a l'usuari.

<img width="891" height="77" alt="image" src="https://github.com/user-attachments/assets/da2b4298-9578-41f4-8554-a67579108f16" />

Per a poder crear groups, farem addgroup, i per a modificar el seu nom és amb groupmod -n

<img width="435" height="139" alt="image" src="https://github.com/user-attachments/assets/854478f4-763f-4a5f-98d2-a0952c51f4f7" />

Si volem afegir un usuari a un group, podem fer adduser "nom de l'usuari" "nom del group"

<img width="386" height="94" alt="image" src="https://github.com/user-attachments/assets/1bd1ad6b-7a17-4006-a552-f6c1cb4d6fd7" />

Es pot observar com l'usuari forma part del group pirates

<img width="399" height="83" alt="image" src="https://github.com/user-attachments/assets/448e57db-664f-4258-ae73-1bb011590238" />

Aquí podem observar la diferència entre l'usuari luffy i l'usuari amb el que hem creat la màquina.

<img width="397" height="211" alt="image" src="https://github.com/user-attachments/assets/0e224d93-ddbd-4585-83d2-ecae19bf147f" />

Si volem esborrar un usuari d'un group ho podem fer mitjançant deluser.

<img width="397" height="75" alt="image" src="https://github.com/user-attachments/assets/6b9d666f-e876-43b4-b5f1-4d573dd968c4" />


## Canviar nom usuari correctament

Si volem canviar el nom d'un usuari ho podem fer amb usermod, amb les coletilles -l, per a canviar el nom antic, -d, per a establir una home nova, i molt important el -m per a poder moure tots els arxius de la home de luffy per a donar-li al usuari zoro.

<img width="525" height="344" alt="image" src="https://github.com/user-attachments/assets/7f80cdca-51e6-44f3-adfb-01116d5bebbc" />


## Crear un usuari amb una sola comanda

Per a crear un usuari amb userad afegirem les coletilles -m, que li crea una home automàticament, i -s per a que li crei una shell al usuari nami.

<img width="426" height="76" alt="image" src="https://github.com/user-attachments/assets/7d62716d-b290-41d7-8221-ea1dbe8924d8" />


# Permisos

## Permisos Bàsics (XWR) a Linux

Els permisos **XWR** són la notació simbòlica clau utilitzada en el sistema de permisos UGO (Usuari, Grup, Altres) de Linux per determinar les accions permeses sobre un fitxer o directori.

| Lletra | Nom Complert | Notació Octal | Funció sobre Fitxers | Funció sobre Directoris |
| :---: | :---: | :---: | :--- | :--- |
| **r** | **Lectura** (Read) | 4 | Permet visualitzar el contingut del fitxer. | Permet **llistar** el contingut del directori (`ls`). |
| **w** | **Escriptura** (Write) | 2 | Permet **modificar, desar i eliminar** el fitxer. | Permet **crear, eliminar i canviar el nom** dels fitxers dins del directori. |
| **x** | **Execució** (Execute) | 1 | Permet **executar** el fitxer (si és un programa). | Permet **accedir** al directori (`cd`) i als seus subdirectoris (sense aquest permís no es pot entrar). |

Per a canviar la propietat d'un arxiu o carpeta d'un usuari al altre, podem fer-ho de dues formes diferents.

<img width="495" height="149" alt="image" src="https://github.com/user-attachments/assets/91087599-ed61-484a-9e59-69564664b4b5" />

També podem establir un gup per a la carpeta. 

<img width="490" height="63" alt="image" src="https://github.com/user-attachments/assets/68ee1333-60b4-48fa-a9b9-1681b3cb39a7" />

També podem observar que li podem llevar permisos sobre aquest arxiu a qualsevol usuari que no formi part del grup o sigui propietari.

<img width="487" height="77" alt="image" src="https://github.com/user-attachments/assets/49bcf6ef-3193-42a1-ac4e-0c45996719a5" />

Si entrem al usuari nick, es pot observar com pot crear arxius dintre i accedir a la carpeta.

<img width="380" height="93" alt="image" src="https://github.com/user-attachments/assets/348edca0-2662-43c1-bd3f-188a93312cfa" />

Intentem accedir a l'usuari cire, i entrar a la carpeta, ens deixa, però com que no forma part del grup no ens deixa crear fitxers dintre. 

<img width="433" height="71" alt="image" src="https://github.com/user-attachments/assets/7e5e762f-520c-4887-990d-25a18330438b" />

I com que l'usuari ferran no forma part del grup palomes no ens deixa entrar dintre del directori palomes.

<img width="345" height="56" alt="image" src="https://github.com/user-attachments/assets/3002157e-b79c-4612-9503-3999cc9300bc" />

Ara establim que tots els usuaris dintre del grup palomes pot accedir i crear dintre.

<img width="514" height="72" alt="image" src="https://github.com/user-attachments/assets/21e9b26d-bf81-4f78-9d05-4a54cb982f87" />

Ara, l'usuari deivy que esta dintre del grup palomes, pot crear arxius dintre d'aquesta. 

<img width="416" height="76" alt="image" src="https://github.com/user-attachments/assets/9c1f8fc1-663f-49a0-9a81-8b4b34bfdb21" />

I els altres usuaris tambe poden acedir, crear i visualitzar els fitxers de dintre.

<img width="296" height="78" alt="image" src="https://github.com/user-attachments/assets/a100c2f2-2cf0-42cc-8ba0-c466e5473333" />




## UMASK

Sense sudo és 0022 i l'usuari normal és 0002

<img width="269" height="130" alt="image" src="https://github.com/user-attachments/assets/d60b7c91-6b52-4f49-9463-bab3ed811b6f" />

Editem el fitxer login.defs

<img width="317" height="83" alt="image" src="https://github.com/user-attachments/assets/82181e2d-0e02-469f-a8a3-c7d289ca297f" />

Al .profile podem observar quina és la màscara de l'usuari.

<img width="1020" height="233" alt="image" src="https://github.com/user-attachments/assets/b10425c8-46f5-4747-827b-d3f862fb0447" />

Fem un canvi de la màscara de l'usuari 

<img width="230" height="114" alt="image" src="https://github.com/user-attachments/assets/c544f55d-fb07-47a3-9252-edc75b42b05e" />

Canviem umask a 0004 i canvien els permisos dels fitxers que hem creat.

<img width="461" height="122" alt="image" src="https://github.com/user-attachments/assets/010c20c8-4eb6-41b5-aaf8-7c6704ef1839" />

Per a fer-ho definitiu podem modificar el login.defs

<img width="1007" height="453" alt="image" src="https://github.com/user-attachments/assets/2875886b-7fe7-4143-afde-5219dd9dd2a9" />

Creem un usari nou, i per a comprovar el funcionament del canvi de màscara, a part del umask, podem crear una carpeta i un arxiu. 

<img width="442" height="206" alt="image" src="https://github.com/user-attachments/assets/5aedac87-a43e-4fe2-aec4-e812333ab688" />


# ACLs

Les ACLS (Access Control Lists o Llistes de Control d'Accés) són un sistema de permisos que complementa els permisos bàsics UGO (Usuari, Grup, Altres) de Linux, oferint un control d'accés més granular i flexible. Permeten assignar permisos concrets de lectura, escriptura o execució a usuaris individuals o grups específics que no siguin el propietari o el grup principal del fitxer. Això és fonamental en entorns col·laboratius on el control d'accés ha de ser precís i detallat.

Creo una carpeta anomenada "1piece", i amb la comanda getfacl podem comprovar els permisos. 

<img width="412" height="255" alt="image" src="https://github.com/user-attachments/assets/eac8070e-f9cc-4268-b670-f214b47da64a" />


Si volem que algun usuari no pugui accedir a la carpeta podem uilitzar la comanda 

```
setfacl -m user:usuari: --- carpeta
```

  <img width="427" height="219" alt="image" src="https://github.com/user-attachments/assets/66ccb7ab-f21d-46f6-9b36-00ac24c765dd" />

Ens connectem amb l'usuari luffy i accedm a la carpeta 1piece, veurem que no podrem accedir.

<img width="485" height="289" alt="image" src="https://github.com/user-attachments/assets/37bc2804-2fec-4786-85b0-1a50f88a251a" />

Ara podem resetejar les ACL utilitzant la coletilla -b a setfacl.

<img width="291" height="363" alt="image" src="https://github.com/user-attachments/assets/0e6edca2-34ee-43d4-be13-33e8ed5a6114" />

# Permisos especials

## Permisos Especials (Especials) a Linux

| Nom del Permís | Notació Octal | Notació Simbòlica | Aplicació Típica | Funció Principal |
| :--- | :---: | :---: | :--- | :--- |
| **SetUID (SUID)** | 4000 | `s` (a la posició de l'usuari) | Fitxers executables (com `passwd`) | Permet executar el fitxer amb els **permisos del propietari** (sovint *root*). |
| **SetGID (SGID)** | 2000 | `s` (a la posició del grup) | Directoris de projectes compartits | **Directoris:** Tots els fitxers nous **hereten el grup** del directori pare. |
| **Sticky Bit** | 1000 | `t` (a la posició dels altres) | Directoris públics (com `/tmp`) | Impedeix que un usuari **esborri fitxers d'un altre usuari**, fins i tot si té permisos d'escriptura (`w`). |

Podem observar sense el sticky bit altres ususaris poden esborrar arxius d'altres.

<img width="519" height="197" alt="image" src="https://github.com/user-attachments/assets/e855fd7f-c0e3-4df6-adc4-bba7812ac58b" />

I amb el sticky bit no funciona

<img width="316" height="24" alt="image" src="https://github.com/user-attachments/assets/dc0c439d-bf52-447f-a484-ac437166bbbf" />


<img width="528" height="258" alt="image" src="https://github.com/user-attachments/assets/764024c6-61a4-47b0-b895-34e3a8865dc7" />






---

# Gestió de Processos

## Introducció

En Linux, un **procés** és una instància d'un programa en execució. Cada procés té un identificador únic anomenat **PID (Process ID)**. El sistema operatiu gestiona aquests processos assignant-los recursos com CPU, memòria i temps d'execució.

La gestió de processos és fonamental per:
- Monitoritzar l'ús de recursos del sistema
- Identificar processos que consumeixen massa CPU o memòria
- Finalitzar processos que no responen
- Ajustar prioritats d'execució
- Gestionar tasques en segon pla

## Comandes bàsiques de visualització

### `ps` - Process Status

La comanda `ps` mostra informació sobre els processos actius. L'opció més utilitzada és `ps aux`:

- **a**: mostra processos de tots els usuaris
- **u**: mostra informació detallada (usuari, %CPU, %MEM)
- **x**: inclou processos sense terminal associada

[alt text](image.png)

També podem filtrar processos específics utilitzant `grep`:

```bash
ps aux | grep firefox
```

![alt text](image-1.png)

Per veure només els processos d'un usuari:

```bash
ps -u nom_usuari
```

![alt text](image-2.png)

### `pstree` - Arbre de processos

La comanda `pstree` mostra la jerarquia de processos en forma d'arbre, facilitant la visualització de les relacions pare-fill entre processos.

```bash
pstree
```

![alt text](image-3.png)

Per veure també els PIDs:

```bash
pstree -p
```

![alt text](image-4.png)

## Monitorització en temps real

### `top` - Monitor de processos

`top` és una eina interactiva que mostra els processos en temps real, actualitzant la informació cada pocs segons. Per defecte, ordena els processos per consum de CPU.

```bash
top
```

![alt text](image-5.png)

Tecles útils dins de `top`:
- **q**: sortir
- **k**: matar un procés (demana el PID)
- **M**: ordenar per ús de memòria
- **P**: ordenar per ús de CPU
- **h**: ajuda

### `htop` - Monitor millorat

`htop` és una versió millorada de `top` amb una interfície més visual i fàcil d'utilitzar. Permet utilitzar el ratolí i té colors per facilitar la lectura.

```bash
htop
```

![alt text](image-6.png)

Funcions principals:
- **F4**: filtrar processos per nom
- **F9**: matar un procés (selecciona la senyal)
- **F6**: ordenar per diferents criteris
- **F10** o **q**: sortir

![alt text](image-7.png)

### `btop` - Monitor modern

`btop` és una eina de monitorització molt potent i visualment atractiva. Mostra gràfics detallats de CPU, RAM, xarxa i discos.

Primer cal instal·lar-lo:

```bash
sudo apt install btop
```

![alt text](image-8.png)

Després executem:

```bash
btop
```

![alt text](image-9.png)

Característiques de `btop`:
- Gràfics animats de CPU i RAM
- Monitorització de xarxa en temps real
- Temperatures del sistema
- Ús del disc
- Suport per ratolí
- Interfície personalitzable

## Gestió de processos - Senyals

### `kill` - Finalitzar processos

La comanda `kill` envia senyals als processos. La senyal més comuna és **SIGTERM (15)**, que demana al procés que es tanqui de manera ordenada.

Primer identifiquem el PID del procés:

```bash
ps aux | grep nom_proces
```

![alt text](image-10.png)

Després enviem la senyal de terminació:

```bash
kill PID
```

![alt text](image-11.png)

### `kill -9` - Terminació forçada

Si un procés no respon a `kill`, podem forçar la seva finalització amb la senyal **SIGKILL (9)**:

```bash
kill -9 PID
```

![alt text](image-12.png)

**Diferències entre senyals:**

| Senyal | Número | Descripció |
|--------|--------|------------|
| SIGTERM | 15 | Terminació ordenada (per defecte) |
| SIGKILL | 9 | Terminació forçada immediata |
| SIGHUP | 1 | Reiniciar procés |
| SIGSTOP | 19 | Pausar procés |
| SIGCONT | 18 | Continuar procés pausat |

## Prioritats de processos

### Concepte de prioritat (Nice)

Linux utilitza un sistema de prioritats anomenat **nice** que va de **-20** (màxima prioritat) a **19** (mínima prioritat). Per defecte, els processos s'inicien amb prioritat 0.

- **Valors negatius (-20 a -1)**: Major prioritat (només root)
- **Valor 0**: Prioritat normal
- **Valors positius (1 a 19)**: Menor prioritat

### `nice` - Iniciar procés amb prioritat

Per iniciar un procés amb una prioritat específica:

```bash
nice -n 10 sleep 100 &
ps -l | grep sleep
```

![alt text](image-13.png)


### `renice` - Canviar prioritat d'un procés existent

Per canviar la prioritat d'un procés que ja està en execució:

```bash
# Primer iniciem un procés
sleep 200 &
# Anotem el PID
# Canviem la seva prioritat
sudo renice -n -5 -p PID
ps -l | grep sleep
```

![alt text](image-14.png)

## Treballs en segon pla (Background Jobs)

### Executar processos en segon pla amb `&`

Per executar un procés en segon pla (background), afegim `&` al final de la comanda:

```bash
sleep 300 &
```

![alt text](image-16.png)

### `jobs` - Llistar treballs

Per veure els treballs en execució en la sessió actual:

```bash
jobs
```

![alt text](image-15.png)

Per veure també els PIDs:

```bash
jobs -l
```

![alt text](image-17.png)

### `bg` - Continuar en segon pla

Si hem pausat un procés amb **Ctrl+Z**, podem continuar-lo en segon pla:

```bash
# Iniciem un procés
sleep 400
# Premem Ctrl+Z per pausar-lo
# Després executem:
bg
jobs
```

![alt text](image-18.png)

### `fg` - Portar a primer pla

Per portar un treball de segon pla a primer pla:

```bash
fg %1
```

On `%1` és el número del treball mostrat per `jobs`.

![alt text](image-19.png)

## Resum de comandes

| Comanda | Funció |
|---------|--------|
| `ps aux` | Llista tots els processos amb detalls |
| `ps -u usuari` | Processos d'un usuari específic |
| `pstree` | Arbre jeràrquic de processos |
| `pstree -p` | Arbre amb PIDs |
| `top` | Monitor en temps real |
| `htop` | Monitor millorat interactiu |
| `btop` | Monitor modern amb gràfics |
| `kill PID` | Finalitzar procés (SIGTERM) |
| `kill -9 PID` | Forçar finalització (SIGKILL) |
| `nice -n X comanda` | Iniciar amb prioritat X |
| `renice -n X -p PID` | Canviar prioritat a X |
| `comanda &` | Executar en segon pla |
| `jobs` | Llistar treballs actius |
| `jobs -l` | Llistar treballs amb PIDs |
| `bg` | Continuar treball en segon pla |
| `fg %N` | Portar treball N a primer pla |
| `Ctrl+Z` | Pausar procés actual |

---


---

# Còpies de Seguretat i Automatització de Tasques

## Introducció

Les còpies de seguretat (backups) són essencials per protegir les dades davant de pèrdues accidentals, fallades de maquinari o atacs maliciosos. L'automatització d'aquestes tasques garanteix que es realitzin de manera regular sense intervenció manual.

En aquesta secció aprendrem:
- Comandes per crear còpies de seguretat (`tar`, `rsync`)
- Automatització de tasques amb `cron` i `anacron`
- Scripts per automatitzar backups
- Diferències entre Cron i Anacron

---

## Comandes de Backup

### `tar` - Arxius comprimits

`tar` (Tape Archive) és una eina per crear arxius que agrupen múltiples fitxers i directoris en un sol fitxer. Pot comprimir-los per estalviar espai.

#### Crear un arxiu tar

```bash
tar -cvf backup.tar /ruta/directori/
```

Opcions:
- **c**: crear arxiu
- **v**: verbose (mostra el progrés)
- **f**: especifica el nom del fitxer

![alt text](image-21.png)

#### Crear arxiu tar comprimit amb gzip

```bash
tar -czvf backup.tar.gz /ruta/directori/
```

Opcions addicionals:
- **z**: comprimir amb gzip

![alt text](image-20.png)

#### Llistar contingut d'un tar

```bash
tar -tvf backup.tar.gz
```

Opcions:
- **t**: llistar contingut
- **v**: mode verbose

![alt text](image-22.png)

#### Extreure un arxiu tar

```bash
tar -xzvf backup.tar.gz -C /ruta/destino/
```

Opcions:
- **x**: extreure
- **C**: especificar directori de destinació

![alt text](image-23.png)

### `rsync` - Sincronització de fitxers

`rsync` és una eina potent per sincronitzar fitxers i directoris entre ubicacions. És més eficient que `cp` perquè només copia els canvis.

#### Sincronització bàsica

```bash
rsync -av /origen/ /destino/
```

Opcions:
- **a**: mode arxiu (preserva permisos, timestamps, etc.)
- **v**: verbose

![alt text](image-24.png)

---

## Automatització de Tasques

### Cron - Programador de tasques

**Cron** és un dimoni (servei) que executa tasques programades a hores específiques. És ideal per sistemes que estan sempre encesos.

#### Estructura de crontab

El format d'una línia crontab és:

```
* * * * * comanda_a_executar
│ │ │ │ │
│ │ │ │ └─── Dia de la setmana (0-7, 0 i 7 són diumenge)
│ │ │ └───── Mes (1-12)
│ │ └─────── Dia del mes (1-31)
│ └───────── Hora (0-23)
└─────────── Minut (0-59)
```

**Exemples:**
- `0 2 * * *` - Cada dia a les 2:00 AM
- `*/15 * * * *` - Cada 15 minuts
- `0 0 * * 0` - Cada diumenge a mitjanit
- `30 3 1 * *` - Dia 1 de cada mes a les 3:30 AM

#### Veure /etc/crontab

```bash
cat /etc/crontab
```

![alt text](image-25.png)

#### Editar crontab d'usuari

```bash
crontab -e
```

Obre l'editor per afegir tasques del usuari actual.

![alt text](image-26.png)

#### Exemple: Script de backup automatitzat

Creem un script que faci backup automàtic:

```bash
#!/bin/bash
FECHA=$(date +%Y%m%d_%H%M%S)
tar -czf /backup/backup_$FECHA.tar.gz /home/usuario/datos/
echo "Backup creat: $FECHA" >> /var/log/backup.log
```

![alt text](image-27.png)

Afegim al crontab per executar cada dia a les 2 AM:

```
0 2 * * * /home/usuario/backup_script.sh
```

![alt text](image-28.png)

#### Verificar logs de cron

```bash
sudo grep CRON /var/log/syslog | tail -n 20
```

![alt text](image-33.png)

---

### Anacron - Tasques periòdiques

**Anacron** està dissenyat per sistemes que no estan sempre encesos (portàtils, PCs d'escriptori). Executa tasques pendents quan el sistema arranca.

#### Diferències Cron vs Anacron

| Característica | Cron | Anacron |
|----------------|------|---------|
| **Precisió** | Hora exacta | Dia aproximat |
| **Requisit** | Sistema sempre encès | Pot estar apagat |
| **Ús típic** | Servidors | Portàtils, PCs |
| **Granularitat** | Minuts | Dies |
| **Execució perduda** | No es recupera | S'executa al arrancar |


#### Configuració d'anacron

```bash
cat /etc/anacrontab
```

![alt text](image-29.png)

Format d'anacrontab:
```
període_dies   retard_minuts   identificador   comanda
```

Exemple:
```
1    5    cron.daily    run-parts /etc/cron.daily
7    10   cron.weekly   run-parts /etc/cron.weekly
```

#### Directoris de scripts automàtics

Linux té directoris predefinits per scripts que s'executen automàticament:

```bash
ls -l /etc/cron.daily/
ls -l /etc/cron.weekly/
ls -l /etc/cron.monthly/
```

![alt text](image-30.png)

Qualsevol script executable en aquests directoris s'executarà automàticament.

#### Crear script en cron.daily

```bash
sudo nano /etc/cron.daily/cleanup_temp
```

Contingut del script:
```bash
#!/bin/bash
find /tmp -type f -mtime +7 -delete
echo "Neteja executada: $(date)" >> /var/log/cleanup.log
```

Donar permisos:
```bash
sudo chmod +x /etc/cron.daily/cleanup_temp
```

![alt text](image-31.png)
---

### Directori /etc/cron.d/

Aquest directori permet crear fitxers de configuració cron personalitzats amb el mateix format que `/etc/crontab`.

```bash
sudo nano /etc/cron.d/backup_personalitzat
```

Contingut:
```
30 3 * * * root /home/usuario/backup_script.sh
```

![alt text](image-32.png)

---



---

## Resum de comandes

| Comanda | Funció |
|---------|--------|
| `tar -cvf arxiu.tar dir/` | Crear arxiu tar |
| `tar -czvf arxiu.tar.gz dir/` | Crear tar comprimit |
| `tar -xzvf arxiu.tar.gz` | Extreure tar comprimit |
| `tar -tvf arxiu.tar.gz` | Llistar contingut |
| `rsync -av origen/ desti/` | Sincronitzar directoris |
| `rsync -av --delete origen/ desti/` | Sincronitzar i eliminar obsolets |
| `rsync -av --dry-run origen/ desti/` | Simular sincronització |
| `crontab -e` | Editar tasques cron |
| `crontab -l` | Llistar tasques cron |
| `cat /etc/crontab` | Veure crontab del sistema |
| `cat /etc/anacrontab` | Veure configuració anacron |
| `/etc/cron.daily/` | Scripts diaris |
| `/etc/cron.weekly/` | Scripts setmanals |
| `/etc/cron.monthly/` | Scripts mensuals |
| `/etc/cron.d/` | Configuracions cron personalitzades |

---



---

# Quotes de Disc

## Introducció

Les **quotes de disc** (disk quotas) són un mecanisme del sistema operatiu que permet limitar la quantitat d'espai de disc que un usuari o grup pot utilitzar en una partició. Això és essencial en entorns multiusuari per:

- Evitar que un usuari ompli tot el disc
- Distribuir equitativament l'espai disponible
- Controlar el creixement de dades
- Prevenir atacs de denegació de servei (DoS)

En aquesta secció aprendrem:
- Instal·lar i configurar el sistema de quotes
- Establir límits per usuaris i grups
- Monitoritzar l'ús de quotes
- Provar els límits configurats

---

## Conceptes bàsics

### Tipus de límits

Les quotes de disc tenen dos tipus de límits:

| Tipus | Descripció | Comportament |
|-------|------------|--------------|
| **Soft Limit** | Límit tou o flexible | Es pot excedir temporalment amb advertències. Té un període de gràcia (normalment 7 dies) |
| **Hard Limit** | Límit dur o absolut | NO es pot excedir mai. El sistema bloqueja l'escriptura quan s'arriba a aquest límit |

### Mètriques de quota

Les quotes es poden aplicar a:

- **Blocks**: Espai de disc utilitzat (normalment mesurat en KB o MB)
- **Inodes**: Nombre de fitxers i directoris creats

---

## Instal·lació

### Instal·lar el paquet quota

```bash
sudo apt update
sudo apt install quota
```


---

## Configuració

### 1. Preparar la partició

Primer identifiquem les particions disponibles:

```bash
df -h
lsblk
```


Creem un directori de dades (si no existeix):

```bash
sudo mkdir -p /mnt/datos
```


### 2. Editar /etc/fstab

Per activar les quotes, hem d'afegir les opcions `usrquota` i `grpquota` a la partició en `/etc/fstab`.

Abans de modificar, veiem el contingut actual:

```bash
cat /etc/fstab
```


Editem el fitxer:

```bash
sudo nano /etc/fstab
```

Afegim les opcions a la línia de la partició:

```
/dev/sdb1  /mnt/datos  ext4  defaults,usrquota,grpquota  0  2
```


Verifiquem els canvis:

```bash
cat /etc/fstab | grep quota
```


### 3. Remontar la partició

Apliquem els canvis remuntant la partició:

```bash
sudo mount -o remount /mnt/datos
mount | grep /mnt/datos
```


### 4. Crear fitxers de base de dades de quotes

```bash
sudo quotacheck -cugm /mnt/datos
```

Opcions:
- **c**: crear fitxers de quota
- **u**: comprovar quotes d'usuari
- **g**: comprovar quotes de grup
- **m**: no remontar en mode només lectura

Verifiquem que s'han creat els fitxers:

```bash
ls -l /mnt/datos/aquota.*
```

![alt text](image-43.png)

### 5. Activar les quotes

```bash
sudo quotaon /mnt/datos
```

Verifiquem que estan actives:

```bash
sudo quotaon -p /mnt/datos
```

![alt text](image-44.png)

---

## Establir quotes per usuaris

### Crear usuari de prova

```bash
sudo adduser testquota
sudo mkdir /mnt/datos/testquota
sudo chown testquota:testquota /mnt/datos/testquota
```

![alt text](image-45.png)

### Editar quota de l'usuari

```bash
sudo edquota -u testquota
```

S'obrirà un editor (vim o nano) amb aquest format:

```
Filesystem  blocks  soft    hard    inodes  soft  hard
/dev/sdb1   0       10000   15000   0       100   150
```

On:
- **blocks**: Espai actual utilitzat
- **soft/hard (blocks)**: Límits en KB (10MB soft, 15MB hard)
- **inodes**: Nombre de fitxers actual
- **soft/hard (inodes)**: Límits de fitxers (100 soft, 150 hard)

![alt text](image-46.png)

### Verificar quota establerta

```bash
sudo quota -u testquota
```

![alt text](image-47.png)

### Veure reporte de totes les quotes

```bash
sudo repquota -a
```

![alt text](image-48.png)

---

## Provar les quotes

### Canviar a l'usuari de prova

```bash
su - testquota
cd /mnt/datos/testquota
```

### Crear fitxer dins del límit

```bash
dd if=/dev/zero of=archivo1.dat bs=1M count=5
ls -lh
```

![alt text](image-51.png)

### Verificar ús de quota

```bash
quota
```

![alt text](image-52.png)

### Excedir el límit soft

```bash
dd if=/dev/zero of=archivo2.dat bs=1M count=8
quota
```

Veurem un missatge d'advertència indicant que s'ha excedit el límit soft.

![alt text](image-53.png)


### Intentar excedir el límit hard

```bash
dd if=/dev/zero of=archivo3.dat bs=1M count=10
```

Obtindrem un error: **"Disk quota exceeded"**

![alt text](image-54.png)

---

## Quotes de grup

### Crear grup i establir quota

```bash
sudo groupadd proyectoA
sudo edquota -g proyectoA
```


### Verificar quota de grup

```bash
sudo quota -g proyectoA
```


---

## Gestió de quotes

### Desactivar quotes

```bash
sudo quotaoff /mnt/datos
```

### Reactivar quotes

```bash
sudo quotaon /mnt/datos
```


### Comprovar estat de quotes

```bash
sudo quotaon -p /mnt/datos
```

Mostra si les quotes estan actives o no.

---

## Resum de comandes

| Comanda | Funció |
|---------|--------|
| `apt install quota` | Instal·lar paquet de quotes |
| `quotacheck -cugm /particio` | Crear fitxers de base de dades |
| `quotaon /particio` | Activar quotes |
| `quotaoff /particio` | Desactivar quotes |
| `quotaon -p /particio` | Veure estat de quotes |
| `edquota -u usuari` | Editar quota d'usuari |
| `edquota -g grup` | Editar quota de grup |
| `quota -u usuari` | Veure quota d'usuari |
| `quota -g grup` | Veure quota de grup |
| `quota` | Veure quota de l'usuari actual |
| `repquota -a` | Reporte de totes les quotes |
| `repquota /particio` | Reporte de quotes d'una partició |

---

