# Sprint 2:

# Instal·lació, configuració de programari de base i gestió de fitxers.

## Sistemes de fixers i particions


  - Mida sector

El sector és la unitat mínima física on es guarden les dades en un disco. I per defecte són 512 Bytes. Aquesta mida no es pot canviar, tots els discos tenen aquesta mida per defecte. 

  - Mida bloc

Un bloc es la mida mínima lògica on es guarden las dades en el nostre SO, té una mida de 4096 per defecte. Aquesta mida sí es pot canviar, només quan formatem el disc. El nostre SO per defecte agarra 8 sectors per bloc.
La mida de bloc, així com el sistema de fitxers pot ser diferent a cada partició del disc.

  - Fragmentació interna

La fragmentació interna es quan es desaprofiten blocs del disco perquè els blocs són massa grans per al que s'ha d'emmagatzemar a dintre.
  
  - Fragmentació externa

A mesura que vas treballant el sistema, els arxius es van separant en diferents blocs, 
  
  - Tipus de formatieg
      
  - Baix nivell
   
Borra fitxers, el sistema fitxers i si troba algun sector defectuós els intenta reparar.

  - Mig nivell
      
Borra el sistema de fitxers, però si troba algun sector defectuós, el marca per a no guardar fitxers dintre.

  - Alt nivell
   
Només borra el sistema de fitxers.

  - Gestió de particions
      - GPARTED
      - Comandes
  
- Gesrió de processos
- Gestió d'usuaris i grups i permisos 
- Còpies de seguretat i automatització de tasques
- Quotes d'usuari
