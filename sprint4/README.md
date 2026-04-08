# Sprint 4: Configuracio del programari de base i sistemes d'emmagatzematge a Ubuntu

## Teoria RAID

### Que es un RAID?

RAID (Redundant Array of Independent Disks) es una tecnologia que permet combinar diversos discos fisics en una sola unitat logica. L'objectiu principal es millorar el rendiment, la disponibilitat de les dades i la tolerancia a fallades.

El sistema operatiu veu aquest conjunt de discos com si fos un unic dispositiu d'emmagatzematge.

### Beneficis principals del RAID

- Tolerancia a fallades: alguns nivells de RAID permeten continuar treballant encara que un disc falli.
- Mes disponibilitat: el sistema pot seguir operatiu i es redueix el temps d'aturada.
- Millora del rendiment: alguns nivells reparteixen lectures i escriptures entre diversos discos.
- Escalabilitat: es poden afegir discos per augmentar capacitat o proteccio.
- Millor aprofitament dels recursos: es poden obtenir solucions robustes sense haver de dependre de maquinari molt car.

### Tipus de RAID mes habituals

| Nivell | Nom | Discos minims | Descripcio |
| --- | --- | --- | --- |
| RAID 0 | Striping | 2 | Distribueix les dades entre discos per millorar el rendiment, pero no ofereix redundancia. |
| RAID 1 | Mirroring | 2 | Fa una copia exacta de les dades en dos discos. Si un falla, l'altre continua funcionant. |
| RAID 5 | Striping amb paritat | 3 | Combina rendiment i redundancia. Permet suportar la fallada d'un disc. |
| RAID 6 | Striping amb doble paritat | 4 | Similar al RAID 5, pero tolera la fallada simultania de dos discos. |
| RAID 10 | Mirroring + Striping | 4 | Combina bon rendiment i alta tolerancia a fallades, pero redueix la capacitat util. |

### Combinacions possibles

- RAID 0+1: primer es fa striping i despres mirroring.
- RAID 1+0 o RAID 10: primer es fa mirroring i despres striping.
- RAID 50: combina diversos grups RAID 5.
- RAID 60: combina diversos grups RAID 6.

### Que son els volums logics o LVM?

LVM (Logical Volume Manager) es una capa de gestio d'emmagatzematge que permet administrar l'espai en disc de manera mes flexible que amb particions tradicionals.

- Volum fisic (PV): cada disc o particio afegida a LVM.
- Grup de volums (VG): conjunt de volums fisics que formen un espai comu.
- Volum logic (LV): particio virtual creada dins del grup de volums.

LVM es pot combinar amb RAID per obtenir redundancia i flexibilitat al mateix temps.

---

## Practica: configuracio d'un RAID 1 amb mdadm a Ubuntu

En aquesta practica configurem un RAID 1 entre dos discos virtuals de 2 GiB cadascun, per exemple `/dev/sdb` i `/dev/sdc`, fent servir l'eina `mdadm`.

### Instal·lacio de mdadm

`mdadm` es l'eina habitual de Linux per gestionar RAID per programari. Per instal·lar-la executem:

```bash
sudo apt update
sudo apt install mdadm
```

CAPTURA 1: terminal amb la instal·lacio de `mdadm`.

Despres de la instal·lacio, el sistema ja disposa de l'eina necessaria per crear i administrar arrays RAID.

---

### Comprovar els discos disponibles

Abans de crear el RAID, comprovem que els dos discos nous existeixen i que encara no tenen particions configurades:

```bash
sudo fdisk -l
```

CAPTURA 2: sortida de `fdisk -l` on es vegin `/dev/sdb` i `/dev/sdc`.

En aquesta comprovacio s'ha de veure que els dos discos tenen la mateixa mida i que estan preparats per ser particionats.

---

### Crear la particio del primer disc

Ara obrim `fdisk` sobre el primer disc:

```bash
sudo fdisk /dev/sdb
```

Dins de `fdisk` creem una particio nova amb aquestes opcions:

```text
n
p
1
[Enter]
[Enter]
w
```

CAPTURA 3: creacio de la particio a `/dev/sdb`.

Amb aquest proces es crea `/dev/sdb1`, que ocupara tot el disc.

---

### Crear la particio del segon disc

Repetim exactament el mateix proces al segon disc:

```bash
sudo fdisk /dev/sdc
```

I fem:

```text
n
p
1
[Enter]
[Enter]
w
```

CAPTURA 4: creacio de la particio a `/dev/sdc`.

Així obtenim la particio `/dev/sdc1`.

---

### Verificar les particions creades

Un cop fetes les dues particions, tornem a comprovar l'estat dels discos:

```bash
sudo fdisk -l
```

CAPTURA 5: sortida on es vegin `/dev/sdb1` i `/dev/sdc1`.

Ara ja tenim els dos discos preparats per formar part del RAID 1.

---

### Crear el punt de muntatge

Creem el directori on muntarem el RAID:

```bash
sudo mkdir -p /mnt/raid1
sudo chmod 777 /mnt/raid1
```

CAPTURA 6: creacio de `/mnt/raid1`.

Aquest directori sera el punt de muntatge del dispositiu RAID.

---

### Crear l'array RAID 1

Ara creem l'array RAID 1 amb `mdadm`:

```bash
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```

CAPTURA 7: comanda de creacio del RAID 1 amb `mdadm`.

En aquest moment es crea `/dev/md0`, que sera el dispositiu RAID resultant. El sistema pot iniciar una sincronitzacio automàtica entre els dos discos.

---

### Formatar el RAID

Per poder utilitzar el dispositiu RAID, cal crear-hi un sistema de fitxers. En aquest cas fem servir `ext4`:

```bash
sudo mkfs.ext4 /dev/md0
```

CAPTURA 8: formatacio de `/dev/md0` amb `mkfs.ext4`.

Despres d'aquest pas, el RAID ja te sistema de fitxers i esta preparat per ser muntat.

---

### Verificar l'estat del RAID

Podem consultar l'estat detallat del RAID amb:

```bash
sudo mdadm --detail /dev/md0
```

CAPTURA 9: resultat de `mdadm --detail /dev/md0`.

Aqui hauria d'apareixer que l'array esta en estat correcte i que els dos discos estan actius.

---

### Desar la configuracio de mdadm

Per fer que el RAID es reconstrueixi automaticament en reiniciar el sistema, guardem la configuracio:

```bash
sudo mdadm --detail --scan
sudo sh -c "mdadm --detail --scan > /etc/mdadm/mdadm.conf"
```

CAPTURA 10: sortida de `mdadm --detail --scan` i desament a `mdadm.conf`.

D'aquesta manera el sistema coneixera l'array RAID quan torni a arrencar.

---

### Comprovar el contingut de mdadm.conf

Per verificar que la configuracio s'ha guardat correctament:

```bash
sudo nano /etc/mdadm/mdadm.conf
```

CAPTURA 11: contingut del fitxer `/etc/mdadm/mdadm.conf`.

En aquest fitxer ha d'apareixer la informacio de l'array `/dev/md0` amb el seu UUID.

---

### Configurar el muntatge automatic amb fstab

Ara afegim una entrada al fitxer `/etc/fstab` per muntar el RAID automaticament:

```bash
sudo nano /etc/fstab
```

I hi afegim aquesta linia:

```text
/dev/md0   /mnt/raid1   ext4   defaults   0   0
```

CAPTURA 12: fitxer `/etc/fstab` amb la nova linia afegida.

Aquesta configuracio fa que el RAID es munti automaticament cada vegada que s'inicia el sistema.

---

### Aplicar els canvis i actualitzar l'arrencada

Despres d'editar `fstab`, apliquem el muntatge i actualitzem `initramfs`:

```bash
sudo mount -a
sudo update-initramfs -u -k all
```

CAPTURA 13: execucio de `mount -a` i `update-initramfs -u -k all`.

Amb aixo ens assegurem que el sistema reconeixera correctament el RAID durant l'arrencada.

---

### Verificar el RAID despres del reinici

Despres de reiniciar la maquina, comprovem de nou l'estat del RAID:

```bash
sudo mdadm --detail /dev/md0
```

CAPTURA 14: comprovacio del RAID despres del reinici.

Si tot esta ben configurat, el RAID hauria de continuar actiu i en estat correcte.

---

### Crear fitxers de prova

Per comprovar que el RAID funciona de veritat, hi creem fitxers i directoris:

```bash
cd /mnt/raid1
touch prova1
mkdir carpeta_prova
ls -la
```

CAPTURA 15: creacio de fitxers dins de `/mnt/raid1`.

Amb aquesta prova confirmem que el sistema de fitxers permet llegir i escriure dades sense problemes.

---

### Simular la fallada d'un disc

Per demostrar la tolerancia a fallades del RAID 1, podem marcar un dels discos com a defectuos i retirar-lo:

```bash
sudo mdadm /dev/md0 -f /dev/sdb1
sudo mdadm /dev/md0 -r /dev/sdb1
sudo mdadm --detail /dev/md0
```

CAPTURA 16: estat del RAID en mode degradat.

En aquest moment l'array continua funcionant, pero amb un sol disc actiu. Aquesta es precisament la utilitat del RAID 1.

---

### Verificar l'acces a les dades durant la fallada

Tot i tenir l'array degradat, les dades continuen accessibles:

```bash
ls -la /mnt/raid1
touch /mnt/raid1/prova2
ls -la /mnt/raid1
```

CAPTURA 17: comprovacio que les dades continuen accessibles en estat degradat.

Aquesta prova demostra que el sistema pot continuar treballant encara que un dels discos hagi fallat.

---

### Recuperar el RAID

Finalment, podem tornar a afegir el disc per reconstruir l'array:

```bash
sudo mdadm /dev/md0 -a /dev/sdb1
sudo mdadm --detail /dev/md0
```

CAPTURA 18: reconstruccio del RAID i resincronitzacio.

Quan el disc es reincorpora, `mdadm` inicia la resincronitzacio automatica. Un cop acabada, el RAID torna a estar completament operatiu.

---

## Conclusio

En aquesta practica hem configurat un RAID 1 a Ubuntu amb `mdadm`, hem preparat els discos, hem creat l'array, l'hem formatat i configurat perque es munti automaticament. Tambe hem comprovat que el sistema continua funcionant en cas de fallada d'un disc i que el RAID es pot reconstruir posteriorment.

Aquesta practica mostra com RAID 1 es una solucio util per protegir dades i millorar la disponibilitat del sistema.
