# Sprint 1 de Windows: Instal·lacio i configuracio basica

## Introduccio

En aquest sprint treballarem la instal·lacio i la configuracio inicial de Windows, els punts de restauracio, les llicencies del sistema, el gestor d'arrencada, la xarxa basica, diverses comandes utiles i la instal·lacio d'aplicacions.

La idea d'aquest document es que tu vagis seguint els passos, facis les captures quan toqui i substitueixis cada linia de `CAPTURA X` per la imatge corresponent.

---

## Fase 1: Instal·lacio del sistema operatiu

### Pas 1: Crear la maquina virtual

El primer pas es crear una maquina virtual nova per instal·lar-hi Windows.

Cal configurar-la amb un nom identificable i seleccionar el tipus de sistema operatiu correcte.

![alt text](image.png)

---

### Pas 2: Assignar recursos

Ara cal assignar recursos suficients a la maquina virtual:

- 4 GB de RAM com a minim
- 40 GB de disc com a minim

Si el teu ordinador ho permet, pots assignar una mica mes de memoria per treballar amb mes comoditat.

![alt text](image-1.png)

![alt text](image-2.png)


---

### Pas 4: Instal·lar el sistema

Arrenquem la maquina virtual i seguim l'assistent d'instal·lacio de Windows.

Durant aquest proces s'han de configurar:

- idioma;
- distribucio de teclat;
- usuari;
- contrasenya.

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)
---

### Pas 5: Comprovar que Windows arrenca correctament

Un cop acabada la instal·lacio, comprovem que el sistema arrenca correctament i arriba fins a l'escriptori.

![alt text](image-7.png)

---

## Fase 2: Punts de restauracio

Els punts de restauracio permeten desar l'estat del sistema per poder tornar enrere si fem un canvi que provoca problemes.

### Pas 6: Cercar "Crear un punt de restauracio"

Des del cercador de Windows, escrivim:

```text
Crear un punt de restauracio
```

Obrim l'opcio corresponent.

![alt text](image-9.png)

---

### Pas 7: Activar la proteccio del sistema al disc C:

Dins la configuracio de proteccio del sistema, seleccionem el disc `C:` i activem la proteccio si encara no esta activada.

![alt text](image-10.png)

![alt text](image-11.png)
---

### Pas 8: Crear un punt manual

Ara creem un punt de restauracio manual.

Pots posar-li un nom descriptiu, per exemple:

```text
Punt inicial
```

![alt text](image-12.png)



---

### Pas 9: Fer un canvi al sistema

Per comprovar que la restauracio funciona, fes un canvi al sistema. Instalem steam, epic games i canviem el fons de pantalla.

![alt text](image-13.png)

---

### Pas 10: Restaurar i comprovar

Despres fem la restauracio del sistema i comprovem que el sistema torna a l'estat anterior.

![alt text](image-14.png)

![alt text](image-15.png)

![alt text](image-16.png)


S'han borrat steam i epic games, no obstant, el fons de pantalla no es canvia. 

![alt text](image-17.png)
---

## Fase 3: Llicencies de Windows

### Pas 11: Obrir Configuracio > Sistema > Activacio

Anem a:

```text
Configuracio > Sistema > Activacio
```

En el meu cas està activat amb KMS

![alt text](image-18.png)

---

### Pas 13: Executar `slmgr /xpr`

Obrim `cmd` com a administrador i executem:

```cmd
slmgr /xpr
```

![alt text](image-19.png)

---

### Pas 14: Explicar breument el tipus de llicencia

En aquest apartat has d'escriure una explicacio breu sobre el tipus d'activacio o llicencia que mostra el teu Windows.

Pots comentar si es tracta d'una activacio permanent, d'una activacio digital o d'una llicencia temporal segons el que indiqui el sistema.

!!!!!

CAPTURA 14: finestra o missatge que t'ajudi a justificar l'explicacio de la llicencia.

---

### Pas 15: Consultar el preu aproximat d'una llicencia

Busca el preu aproximat d'una llicencia de Windows a:

- la web oficial de Microsoft;
- o botigues conegudes.

Despres escriu una frase resumint el preu orientatiu que has trobat.

![alt text](image-20.png)

Però de normal a pàgines de keyshops et surt a 5 euros com a molt.
---

## Fase 4: Gestor d'arrencada

### Pas 16: Obrir `cmd` com a administrador

Busca `cmd`, fes clic dret i obre'l com a administrador.

![alt text](image-21.png)
---

### Pas 17: Executar `bcdedit`

Dins la consola, executa:

```cmd
bcdedit
```

![alt text](image-22.png)
---

### Pas 18: Identificar els blocs principals

Dins la sortida de `bcdedit` has d'identificar aquests dos blocs:

- `Windows Boot Manager`
- `Windows Boot Loader`

Del bloc **Boot Manager**, fixa't sobretot en:

- `default {current}`
- `timeout 30`

Del bloc **Boot Loader**, fixa't sobretot en:

- `device partition=C:`
- `path \Windows\system32\winload.efi`
- `description Windows 11` o similar

Unificar amb 17
---

### Pas 19: Interpretar les dades

Ara escriu una petita interpretacio del que signifiquen aquestes dades.

Per exemple, pots explicar:

- quin sistema arrenca per defecte;
- quant temps espera abans d'arrencar;
- a quina particio esta instal·lat Windows;
- quin fitxer inicia el sistema.

fes-ho tu

CAPTURA 19: part concreta de la sortida que facis servir per a la teva interpretacio.

---

### Pas 20: Respondre preguntes curtes

Respon breument aquestes preguntes:

1. Quin sistema s'esta arrencant?
2. A quin disc o particio esta instal·lat?
3. Quant temps espera abans d'arrencar?
4. Quin fitxer inicia Windows?

CAPTURA 20: evidencies de la sortida de `bcdedit` que permeten respondre aquestes preguntes.

respon tu

---

### Pas 21: Interpretacio final en una frase

Escriu una frase final explicant:

- qui decideix l'arrencada (`Boot Manager`);
- qui carrega el sistema (`Boot Loader`).

CAPTURA 21: captura final del bloc `Boot Manager` i/o `Boot Loader`.

fes-ho tu
---

## Fase 5: Xarxa basica

### Pas 22: Obrir la configuracio de xarxa

Obre la configuracio de xarxa de Windows i accedeix a l'adaptador que estas fent servir.

CAPTURA 22: configuracio de xarxa oberta.

---

### Pas 23: Consultar la IP actual

Revisa la configuracio actual de la xarxa per veure la IP assignada.

CAPTURA 23: dades actuals de la connexio de xarxa.

---

### Pas 24: Configurar IP dinamica

Configura l'adaptador per obtenir automaticament:

- IP
- mascara
- gateway
- DNS

CAPTURA 24: configuracio en mode DHCP o obtencio automatica.

---

### Pas 25: Configurar IP fixa

Ara fes la prova contraria i configura una IP fixa manualment.

Has d'indicar:

- IP
- mascara
- passarel·la
- DNS

CAPTURA 25: configuracio manual de la IP fixa.

---

### Pas 26: Comprovar la connexio amb `ping`

Obre `cmd` i executa:

```cmd
ping google.com
```

CAPTURA 26: resultat del `ping`.

Aquesta prova serveix per comprovar si la connectivitat i la resolucio DNS funcionen correctament.

---

## Fase 6: Comandes generals

### Pas 27: Obrir PowerShell

Busca i obre PowerShell.

CAPTURA 27: finestra de PowerShell oberta.

---

### Pas 28: Diferenciar `cmd` i PowerShell

Escriu una petita explicacio sobre la diferencia entre:

- `cmd`, que es la consola classica de comandes;
- `PowerShell`, que es mes potent i orientat a administracio i automatitzacio.

CAPTURA 28: exemple visual de PowerShell o comparacio amb `cmd`.

---

### Pas 29: Comandes basiques

Executa aquestes comandes a `cmd`:

```cmd
dir
cd ..
mkdir prova
echo hola > fitxer.txt
del fitxer.txt
```

Despres explica breument que fa cadascuna.

CAPTURA 29: execucio de les comandes basiques.

---

### Pas 30: Comandes utils del sistema

Executa aquestes comandes:

```cmd
tasklist
taskkill /IM notepad.exe /F
systeminfo
hostname
whoami
```

CAPTURA 30: resultat d'algunes d'aquestes comandes del sistema.

Despres indica breument que mostra cadascuna.

---

### Pas 31: Comandes de xarxa

Executa:

```cmd
ipconfig
ping google.com
netstat -an
```

CAPTURA 31: resultat de les comandes de xarxa.

---

### Pas 32: Comandes interessants

Executa una mica mes de prova amb aquestes comandes:

```cmd
tree
cls
help
shutdown /s /t 0
```

Important: la comanda `shutdown /s /t 0` apaga l'equip immediatament. Si no la vols executar de veritat, pots escriure-la igualment al document i explicar-ne la funcio sense fer-la.

CAPTURA 32: prova d'alguna de les comandes interessants.

---

### Pas 33: Mini interpretacio

Ara escriu una mini explicacio indicant que mostren aquestes comandes:

- `tasklist`
- `ipconfig`
- `systeminfo`

CAPTURA 33: captura de suport per a aquesta interpretacio.

---

## Fase 7: Instal·lacio d'aplicacions

### Pas 34: Descarregar un programa des del navegador

Descarrega un programa des del navegador, per exemple:

- Google Chrome
- Visual Studio Code

CAPTURA 34: descarrega del programa des del navegador.

---

### Pas 35: Instal·lar-lo seguint l'assistent

Executa l'instal·lador i segueix l'assistent.

CAPTURA 35: proces d'instal·lacio del programa.

---

### Pas 36: Obrir-lo i comprovar que funciona

Un cop instal·lat, obre el programa i comprova que funciona correctament.

CAPTURA 36: programa instal·lat i funcionant.

---

### Pas 37: Instal·lar una aplicacio des de Microsoft Store

Obre Microsoft Store i instal·la una aplicacio.

CAPTURA 37: instal·lacio d'una aplicacio des de Microsoft Store.

---

### Pas 38: Obrir-la i comprovar-ne el funcionament

Despres obre l'aplicacio instal·lada i comprova que arrenca correctament.

CAPTURA 38: aplicacio de Microsoft Store oberta i funcionant.

---

### Pas 39: Desinstal·lar una aplicacio

Ves a:

```text
Configuracio > Aplicacions > Aplicacions instal·lades
```

I desinstal·la una de les aplicacions.

CAPTURA 39: proces de desinstal·lacio.

---

### Pas 40: Verificar que ja no apareix al sistema

Comprova que el programa ja no apareix a la llista d'aplicacions o que ja no es pot executar.

CAPTURA 40: comprovacio final que l'aplicacio ha desaparegut del sistema.

---

## Conclusio

En aquest sprint hem realitzat una instal·lacio completa de Windows dins d'una maquina virtual i n'hem revisat diferents aspectes basics d'administracio. Hem treballat la restauracio del sistema, l'activacio i la llicencia, el gestor d'arrencada, la configuracio de xarxa i l'ús de comandes generals de `cmd` i PowerShell.

Tambe hem practicat la instal·lacio i desinstal·lacio d'aplicacions, tant des del navegador com des de Microsoft Store. Tot plegat serveix per entendre millor el funcionament basic de Windows i adquirir una base solida de configuracio i administracio del sistema.
