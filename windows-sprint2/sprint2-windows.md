# Sprint 2 de Windows: Discos, quotes, scripts, processos i ACL

## Introducció

En aquest sprint treballarem la gestió de discs a Windows, la configuració de quotes, la creació d'usuaris i grups, l'automatització amb scripts d'inici de sessió, la gestió de processos i els permisos ACL sobre carpetes i fitxers.

La idea d'aquest document és que puguis seguir-lo pas a pas. A cada apartat hi tens també indicada la captura de pantalla que has de fer. Després només hauràs d'esborrar el text de la captura i enganxar-hi la imatge corresponent.

---

## Fase 1: Preparació del sistema i discs

### Pas 1: Afegir un nou disc virtual a la màquina virtual

Obre la configuració de la màquina virtual a VirtualBox i ves a l'apartat d'emmagatzematge. Afegeix un nou disc dur virtual de `5 GB`, en format `VDI` i de mida dinàmica.

Aquest disc serà el que després utilitzarem per crear dues particions diferents dins de Windows.

---

### Pas 2: Obrir la gestió de discs de Windows

Inicia la màquina virtual de Windows i obre la gestió de discs. Ho pots fer executant:

```text
diskmgmt.msc
```

Comprova que apareix un disc nou sense inicialitzar i amb espai no assignat.

---

### Pas 3: Inicialitzar el disc i crear la partició Dades

Inicialitza el disc nou i crea-hi una primera partició de `5000 MB`. Assigna-li la lletra `E:`.
Formata aquesta partició en `NTFS`, ja que aquest sistema de fitxers permet treballar amb quotes i ACL.
---

### Pas 4: Crear la partició Portable

Amb l'espai restant del disc, crea una segona partició. Assigna-li la lletra `F:` i posa-li l'etiqueta:

```text
Portable
```

En aquest cas, el sistema de fitxers ha de ser `FAT32`.

Pots comentar al document que FAT32 és molt compatible amb altres dispositius, però no suporta quotes ni permisos ACL avançats, a diferència d'NTFS.

---

### Pas 5: Verificar la configuració amb diskpart

Obre una consola `CMD` com a administrador i executa aquestes comandes:

```cmd
diskpart
list disk
sel disk 1
list part
list vol
```

Amb això podràs comprovar que el disc nou té les dues particions creades correctament.

---

## Fase 2: Quotes de disc i usuaris

### Pas 6: Activar quotes a la partició Dades

Obre l'Explorador de fitxers, fes clic dret sobre la unitat `E:` i entra a `Propietats`. Des de la pestanya de quota, activa la gestió de quotes.

Les quotes només funcionen sobre particions `NTFS`, per això la partició Dades s'ha creat amb aquest format.
---

### Pas 7: Configurar el límit de 300 MB

Dins la configuració de quotes, activa les opcions necessàries i configura:

- límit de disc de `350 MB`;
- nivell d'advertència;
- registre d'esdeveniments quan se supera el límit o l'avís.

L'objectiu és que cada usuari no pugui superar els `300 MB` d'espai ocupat a la unitat `E:`.
---

### Pas 8: Crear els usuaris locals alumne1 i alumne2

Executa:

```text
lusrmgr.msc
```

Des d'aquesta consola, crea dos usuaris locals nous:

- `alumne1`
- `alumne2`

Si vols evitar problemes durant les proves, pots activar l'opció perquè la contrasenya no caduqui.

---

### Pas 9: Crear el grup Limitats i afegir-hi els usuaris

Dins de la mateixa consola, crea un grup nou amb el nom:

```text
Limitats
```

Afegeix-hi com a membres els usuaris `alumne1` i `alumne2`.

> 📸 **Captura**: Fes una captura de la finestra del grup `Limitats` on es vegin els dos usuaris afegits.

---

### Pas 10: Provar que les quotes funcionen

Inicia sessió com a `alumne1` i obre una consola. Després intenta crear fitxers grans a `E:\` amb `fsutil`.

Per exemple:

```cmd
fsutil file createnew E:\prova.dat 350000000
fsutil file createnew E:\prova.dat 150000000
fsutil file createnew E:\prova2.dat 50000000
fsutil file createnew E:\prova3.dat 50000000
fsutil file createnew E:\prova4.dat 50000000
fsutil file createnew E:\prova5.dat 50000000
```

Has de veure que, quan l'usuari supera el límit, Windows retorna un error d'espai insuficient.

> 📸 **Captura**: Fes una captura de la consola on es vegin fitxers creats correctament i també l'error quan se supera la quota.

---

## Fase 3: Script de còpia i automatització

### Pas 11: Afegir un tercer disc virtual per a còpies

Torna a VirtualBox i afegeix un tercer disc virtual de `5 GB`. Aquest disc servirà per guardar-hi còpies de seguretat.

> 📸 **Captura**: Fes una captura de la configuració de VirtualBox on es vegi el tercer disc virtual afegit.

---

### Pas 12: Formatar el tercer disc com a Backups

Un cop dins de Windows, obre de nou la gestió de discs i localitza el nou disc. Crea-hi un volum simple, assigna-li la lletra `B:` i posa-li l'etiqueta:

```text
Backups
```

Aquest volum s'ha de formatar en `NTFS`.

> 📸 **Captura**: Fes una captura de `Gestió de discs` on es vegi la unitat `B:` creada amb el nom `Backups`.

---

### Pas 13: Crear la carpeta CòpiesUsuaris

Dins de la unitat `B:`, crea manualment una carpeta amb aquest nom:

```text
CòpiesUsuaris
```

Allà és on l'script anirà guardant la còpia del perfil de cada usuari.

> 📸 **Captura**: Fes una captura de l'Explorador de fitxers on es vegi la carpeta `B:\CòpiesUsuaris`.

---

### Pas 14: Crear l'script de còpia

Crea un fitxer `script.bat` amb aquest contingut:

```bat
@echo off
xcopy C:\Users\%USERNAME% B:\CòpiesUsuaris\%USERNAME% /E /I /Y
```

Aquest script copia tot el perfil de l'usuari que ha iniciat sessió cap a la carpeta de còpies del disc `B:`.

> 📸 **Captura**: Fes una captura del fitxer `script.bat` o del bloc de notes on es vegi clarament el contingut de l'script.

---

### Pas 15: Obrir l'editor de directives de grup

Executa:

```text
gpedit.msc
```

Després navega fins a:

```text
Configuració d'usuari > Configuració de Windows > Scripts (inici o tancament de sessió)
```

Obre l'opció d'inici de sessió.

> 📸 **Captura**: Fes una captura de `gpedit.msc` on es vegi la ruta fins a l'apartat d'Scripts d'inici de sessió.

---

### Pas 16: Assignar l'script a l'inici de sessió

Afegeix l'script `script.bat` a la configuració d'inici de sessió perquè s'executi automàticament cada vegada que un usuari entri al sistema.

Pots indicar també que aquesta configuració local afecta els usuaris del sistema segons la política aplicada.

> 📸 **Captura**: Fes una captura de la finestra on es vegi l'script afegit a la llista de scripts d'inici de sessió.

---

### Pas 17: Verificar que la còpia es fa correctament

Inicia sessió com a `alumne1` i comprova que s'ha creat la carpeta:

```text
B:\CòpiesUsuaris\alumne1
```

Dins hi haurien d'aparèixer les carpetes habituals del perfil d'usuari, com ara `Desktop`, `Documents`, `Downloads` i altres.

> 📸 **Captura**: Fes una captura de l'Explorador de fitxers on es vegi la carpeta de còpia de `alumne1` dins de `B:\CòpiesUsuaris`.

---

## Fase 4: Gestió de processos

### Pas 18: Llistar els processos actius

Obre `CMD` i executa:

```cmd
tasklist
```

Aquesta comanda mostra tots els processos en execució, amb el seu nom, PID, sessió i ús de memòria.

> 📸 **Captura**: Fes una captura de la consola amb la sortida de `tasklist`.

---

### Pas 19: Guardar la llista de processos en un fitxer

Redirigeix la sortida a un fitxer de text amb aquesta comanda:

```cmd
tasklist > C:\Users\%USERNAME%\processos_inici.txt
```

Després pots fer un `dir` per comprovar que el fitxer existeix.

> 📸 **Captura**: Fes una captura de la consola on es vegi la creació del fitxer `processos_inici.txt`.

---

### Pas 20: Analitzar alguns processos importants

Filtra el fitxer per buscar processos concrets:

```cmd
findstr explorer.exe C:\Users\%USERNAME%\processos_inici.txt
findstr SearchIndexer.exe C:\Users\%USERNAME%\processos_inici.txt
findstr OneDrive.exe C:\Users\%USERNAME%\processos_inici.txt
```

Després explica breument què fa cada procés:

- `explorer.exe`: gestiona l'escriptori i l'explorador de fitxers;
- `SearchIndexer.exe`: s'encarrega de la indexació per a les cerques;
- `OneDrive.exe`: sincronitza fitxers amb el núvol.

> 📸 **Captura**: Fes una captura de la consola on es vegin els resultats de `findstr` sobre aquests processos.

---

### Pas 21: Identificar processos prescindibles

Pots buscar processos que no siguin essencials en una màquina virtual de laboratori, per exemple:

```cmd
tasklist | findstr "OneDrive.exe Teams.exe SkypeApp.exe"
```

Aquí pots comentar que eliminar processos com `OneDrive` o `Teams` pot ajudar a alliberar memòria RAM i millorar el rendiment.

> 📸 **Captura**: Fes una captura on es vegin els processos prescindibles detectats a la consola.

---

### Pas 22: Tancar un procés manualment

Prova a tancar `OneDrive.exe` amb:

```cmd
taskkill /IM OneDrive.exe /F
```

Després comprova si encara queda alguna instància oberta amb:

```cmd
tasklist | findstr OneDrive.exe
```

> 📸 **Captura**: Fes una captura de la consola on es vegi el resultat de `taskkill` i la comprovació posterior.

---

### Pas 23: Automatitzar l'eliminació de processos a l'inici de sessió

Modifica l'script `script.bat` i deixa'l així:

```bat
@echo off
xcopy C:\Users\%USERNAME% B:\CòpiesUsuaris\%USERNAME% /E /I /Y
taskkill /IM OneDrive.exe /F
taskkill /IM Teams.exe /F
```

D'aquesta manera, cada cop que un usuari iniciï sessió es farà la còpia del seu perfil i també s'intentaran tancar aquests processos.

> 📸 **Captura**: Fes una captura del contingut actualitzat de `script.bat`.

---

### Pas 24: Verificar l'automatització amb un altre usuari

Inicia sessió com a `alumne2` i comprova si `OneDrive.exe` continua actiu:

```cmd
tasklist | findstr OneDrive.exe
```

Si no surt cap resultat, significa que l'script ha funcionat correctament.

> 📸 **Captura**: Fes una captura de la consola on no aparegui cap resultat per a `OneDrive.exe`.

---

### Pas 25: Explicar què passa si mates explorer.exe

En aquest apartat pots escriure una petita explicació teòrica. Si es tanca `explorer.exe`, desapareixen l'escriptori, la barra de tasques i les finestres de l'explorador, però el sistema no queda bloquejat del tot.

També pots indicar que es pot recuperar obrint l'Administrador de tasques i executant de nou:

```cmd
explorer.exe
```

> 📸 **Captura**: Si fas la prova, fes una captura controlada de l'escriptori sense `explorer.exe`. Si no la fas, pots no posar captura en aquest punt i deixar només l'explicació.

---

## Fase 5: ACL i permisos

### Pas 26: Crear la carpeta Projectes

Com a administrador, crea la carpeta:

```text
E:\Projectes
```

La farem servir per provar permisos diferents entre usuaris.

> 📸 **Captura**: Fes una captura de l'Explorador de fitxers on es vegi la carpeta `E:\Projectes`.

---

### Pas 27: Configurar els permisos per al grup Limitats

Entra a:

```text
E:\Projectes > Propietats > Seguretat > Opcions avançades
```

Desactiva l'herència si cal i ajusta els permisos perquè el grup `Limitats` tingui control sobre la carpeta. També pots eliminar algunes entrades heretades que no necessitis per deixar la configuració més clara.

L'objectiu és que `alumne1` i `alumne2`, pel fet de pertànyer al grup `Limitats`, puguin accedir a la carpeta.

> 📸 **Captura**: Fes una captura de la configuració avançada de seguretat on es vegi el grup `Limitats` amb permisos sobre `E:\Projectes`.

---

### Pas 28: Comprovar que alumne1 pot escriure

Inicia sessió com a `alumne1` i crea un fitxer de prova dins de `E:\Projectes`, per exemple:

```text
hey.txt
```

Escriu-hi algun contingut curt, com ara `hola`, i desa'l.

> 📸 **Captura**: Fes una captura on es vegi que `alumne1` ha pogut crear i desar el fitxer dins de `E:\Projectes`.

---

### Pas 29: Aplicar una excepció de només lectura per a alumne2

Torna a entrar com a administrador i executa:

```cmd
icacls "E:\Projectes" /grant:r alumne2:(R)
```

Aquesta comanda dona a `alumne2` un permís explícit de només lectura sobre la carpeta.

És interessant comentar que les entrades explícites d'un usuari poden tenir prioritat sobre els permisos heretats per grup, segons com estigui configurada l'ACL.

> 📸 **Captura**: Fes una captura de la consola on es vegi la comanda `icacls` executada correctament.

---

### Pas 30: Verificar que alumne2 no pot modificar

Inicia sessió com a `alumne2` i intenta crear o modificar fitxers dins de `E:\Projectes`.

Si la configuració és correcta, Windows hauria de denegar l'acció de modificació o d'escriptura.

> 📸 **Captura**: Fes una captura del missatge d'error o de la prova on es vegi que `alumne2` no pot crear o modificar fitxers dins de `E:\Projectes`.

---

### Pas 31: Consultar l'estat final dels permisos amb icacls

Per acabar, executa:

```cmd
icacls "E:\Projectes"
```

Amb aquesta comanda podràs veure totes les entrades ACL finals de la carpeta.

Pots explicar breument alguns codis habituals:

- `(F)` = control total;
- `(R)` = només lectura;
- `(OI)` = herència cap als fitxers;
- `(CI)` = herència cap a les subcarpetes.

> 📸 **Captura**: Fes una captura de la consola amb la sortida final de `icacls "E:\Projectes"`.

---

## Conclusió

Amb aquest sprint has practicat diverses tasques habituals d'administració a Windows: preparar discs, formatar particions amb sistemes de fitxers diferents, limitar espai amb quotes, crear usuaris i grups, automatitzar còpies de seguretat amb scripts, analitzar processos del sistema i configurar permisos avançats amb ACL.

També has vist que Windows permet combinar eines gràfiques i eines de consola per administrar el sistema de manera bastant completa.
