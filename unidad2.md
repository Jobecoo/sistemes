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


- Gestió de processos
- Gestió d'usuaris i grups i permisos 
- Còpies de seguretat i automatització de tasques
- Quotes d'usuari
