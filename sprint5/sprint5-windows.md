# Sprint 5: Monitoratge i Auditories a Windows Server

## Introducció

En un entorn empresarial, saber qui ha accedit a quins recursos, quan i des d’on és fonamental per garantir la seguretat dels sistemes. Les auditories de seguretat permeten als administradors de sistemes registrar i monitoritzar totes les activitats rellevants que es produeixen en un servidor o estació de treball: inicis de sessió, accessos a fitxers, canvis de configuració, creació i eliminació de comptes, etc.

Windows Server incorpora un sistema d’auditoria integrat basat en polítiques de seguretat locals o de domini que, quan s’activen, generen entrades al Visor d’esdeveniments (`eventvwr.msc`) sota el registre de **Seguretat**. Cada esdeveniment té un Event ID únic que identifica exactament quina acció s’ha produït.

### Per què és important l’auditoria?
- **Detecció d’intrusions**: Identificar intents d’accés no autoritzats (Event 4625 repetits).
- **Compliment normatiu**: Moltes regulacions (ISO 27001, GDPR, PCI-DSS) exigeixen registres d’auditoria.
- **Investigació forense**: En cas d’incident de seguretat, els logs permeten reconstruir els fets.
- **Monitoratge intern**: Controlar l’accés a dades sensibles per part del personal intern.

### Com accedir al Visor d’esdeveniments
Per obrir el Visor d’esdeveniments premem: `Windows + R` → `eventvwr.msc` → `Registros de Windows` → `Seguridad`

Per filtrar per Event ID específic fem: clic dret sobre `Seguridad` → `Filtrar registro actual` → introduir el número d’event.

---

## Part 1: Auditories

### 1. Activar les auditories: Directiva de seguretat local
Obrim el diàleg d’execució amb `Windows + R` i escrivim `secpol.msc` per obrir la Directiva de seguretat local. Acceptem per executar-ho amb privilegis administratius.

![alt text](image-windows-1.png)

### 2. Activar l’auditoria d’inici de sessió
Dins de `secpol.msc`, naveguem a: `Directivas locales` → `Directiva de auditoría` → `Auditar eventos de inicio de sesión`.

Obrim les propietats i marquem tant **Correcto** com **Erróneo**. Això farà que Windows registri tots els inicis de sessió, tant els exitosos (4624) com els fallits (4625).

![alt text](image-windows-2.png)

### 3. Comprovar l’Event ID 4624: inici de sessió correcte
Obrim el Visor d’esdeveniments (`eventvwr.msc`) i naveguem a `Registros de Windows` → `Seguridad`. Filtrem per l’Event ID **4624** i veiem totes les entrades d’inici de sessió correctes.

![alt text](image-windows-3.png)

Això confirma que l’auditoria d’inici de sessió funciona correctament.

---

### 4. Activar l’auditoria d’accés a objectes
Tornem a `secpol.msc` i activem **Auditar el acceso a objetos** marcant Correcto i Erróneo. 

![alt text](image-windows-4.png)

### 5. Crear la carpeta d’auditoria i configurar-la
Creem una carpeta nova a l’arrel del disc `C:` anomenada `ProvaAuditoria`. 

Fem clic dret sobre `ProvaAuditoria` → `Propiedades` → `Seguridad` → `Opciones avanzadas` → `Auditoría` → `Agregar`. Afegim l’usuari Administrador amb tipus d’accés **Control total** perquè quedi registrada qualsevol acció.

![alt text](image-windows-5.png)

### 6. Generar accions dins la carpeta i comprovar (Event ID 4663)
Creem un fitxer de text `hola.txt` dins de `C:\ProvaAuditoria`. Després l’obrim, el modifiquem i l’eliminem. 

Al Visor d’esdeveniments, filtrem per l’Event ID **4663**. Veiem entrades d’accés a l'objecte:

![alt text](image-windows-6.png)

---

### 7. Activar l’auditoria de seguiment de processos
Tornem a `secpol.msc` i activem **Auditar el seguimiento de procesos** amb Correcto i Erróneo.

![alt text](image-windows-7.png)

### 8. Obrir el Bloc de notes i comprovar la creació (Event ID 4688)
Cerquem `notepad` al menú d’inici i l’obrim. Al Visor d’esdeveniments filtrem per **4688**. L'Event mostra el nou procés creat (`notepad.exe`).

![alt text](image-windows-8.png)

### 9. Tancar el Bloc de notes i comprovar la finalització (Event ID 4689)
Tanquem el Bloc de notes. Filtrem per **4689** per comprovar que s’ha registrat la finalització del procés.

![alt text](image-windows-9.png)

---

### 10. Activar l’auditoria d’administració de comptes
A `secpol.msc`, activem **Auditar la administración de cuentas** amb Correcto i Erróneo.

![alt text](image-windows-10.png)

### 11. Obrir la gestió d’usuaris i crear un compte de prova (Event ID 4720)
Premem `Windows + R` i escrivim `lusrmgr.msc` (o des de Usuarios y equipos de Active Directory). Creem un usuari anomenat **joan**.
Filtrem al Visor d’esdeveniments per **4720** i veurem el registre de l'usuari acabat de crear.

![alt text](image-windows-11.png)

### 12. Deshabilitar el compte (Event ID 4725)
Deshabilitem l'usuari `joan`. Al Visor d’esdeveniments, l'Event ID **4725** confirma aquesta acció.

![alt text](image-windows-12.png)

### 13. Eliminar el compte (Event ID 4726)
Eliminem definitivament l'usuari `joan`. Al Visor d’esdeveniments l'Event ID **4726** en documenta l'eliminació, completant el cicle de vida.

![alt text](image-windows-13.png)

---

## Part 2: Monitorització del Sistema

La monitorització consisteix a observar en temps real el comportament dels recursos (CPU, memòria RAM, disc i xarxa) per detectar problemes de rendiment, a diferència de les auditories que ens diuen "què ha passat".

### Pas 1. Obrir l’Administrador de tasques
Premem `Ctrl + Shift + Esc`. A la pestanya *Procesos* veiem el consum general agrupat per aplicacions i processos en segon pla.

![alt text](image-windows-14.png)

### Pas 2. Monitoritzar la CPU i la RAM
A la pestanya *Rendimiento*, observem els gràfics de CPU i Memòria. Ens indica la càrrega actual del processador i cota de memòria lliure, en caché i paginada.

![alt text](image-windows-15.png)

### Pas 3. Monitoritzar la xarxa
A la mateixa pestanya veiem l'apartat *Ethernet* que mostra el rendiment en temps real (enviament i recepció).

![alt text](image-windows-16.png)

### Pas 4. Monitor de recursos (resmon)
Per tenir més detall obrim el **Monitor de recursos** (es pot fer prement `Windows + R` i escrivint `resmon`). Aquest ofereix una visió molt més profunda i desglossada.

![alt text](image-windows-17.png)

### Pas 5. Revisió de serveis concrets a CPU i Memòria
Dins del Monitor de recursos, podem veure exactament quin servei (per exemple `wuauserv` sota `svchost.exe`) està consumint CPU o quin executable (com `MsMpEng.exe` de Windows Defender) fa servir més memòria privada.

![alt text](image-windows-18.png)

### Pas 6. Revisió de disc i Ports actius a la xarxa
A les pestanyes de Disc i Xarxa podem identificar quins processos estan escrivint al disc dur, o bé veure els **Puertos de escucha** (com el 53 DNS o 88 Kerberos), la qual cosa ens permet auditar serveis innecessaris.

![alt text](image-windows-19.png)

---

## Conclusions
- **Diferència clau**: La monitorització és proactiva i ofereix l'estat en temps real (ideal amb `resmon`); l’auditoria és reactiva i ens indica el que ha passat al llarg del temps (Visor d'esdeveniments).
- **Doble configuració d'auditoria**: Per a arxius i objectes, cal activar la política a `secpol.msc` i a les opcions avançades de la carpeta, si no l'auditoria no registra els events com el `4663`.
- **Rendiment**: Activar el seguiment de processos (com l'Event `4688`) en un servidor de producció genera un volum d'informació enorme i pot omplir els logs molt ràpidament. Es recomana derivar la informació a un servidor SIEM extern.
