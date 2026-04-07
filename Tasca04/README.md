# Introducció

En el món de la logística la impressió continua tenint un paper molt important: albarans, fulls de transport, etc. necessiten ser impresos. El vostre client no és una excepció  

L'empresa té un magatzem on el volum d'impressió d'albarans és crític. Si una impressora falla o es col·lapsa, els camions no poden sortir, cosa que trenca la cadena de fred. L'objectiu d'aquesta activitat és configurar un Servidor d'Impressió a Windows Server que gestioni aquest volum mitjançant el Printer Pooling (Cua d'impressió compartida) per balancejar la càrrega entre dos dispositius.

# Descripció de l'activitat

El servidor haurà de tenir implementats els serveis de directori (Active Directory) i el servei de servidor d’impressió, permetent així la gestió centralitzada d’usuaris, equips i recursos d’impressió. El client, integrat al domini, haurà de poder autenticar-se amb credencials de xarxa i accedir als recursos compartits, especialment a les impressores desplegades des del servidor.  

Heu de documentar cada pas del procés com si es tractés d’un informe tècnic d’implementació per a un client real, utilitzant un llenguatge clar, estructurat i professional. Cal justificar les decisions preses i descriure les configuracions realitzades.  

L’activitat es divideix en quatre fases tècniques que s’han d’executar dins d’aquest entorn:

## 1. Preparació de l'entorn i simulació de maquinari

- Verificar o preparar l’entorn necessari, o bé aprofitar-ne un de similar ja existent.  
- Instal·la i configura dues instàncies d’impressora PDF24 al servidor en els materials de suport teniu una guia pas a pas. 
- Nomena-les de forma corporativa: IMP_MAGATZEM_A i IMP_MAGATZEM_B.  

## 2. Instal·lació del Rol i Configuració del Pool

- Instal·la el rol de Print and Document Services al Windows Server.  
- Accedeix a la consola Print Management.  
- Configuració del Printer Pooling:

  - Ves a les propietats de IMP_MAGATZEM_A  
  - A la pestanya “Ports”, marca la casella “Enable printer pooling”.  
  - Selecciona el port on es troba la segona impressora IMP_MAGATZEM_B.  
  - A partir d'aquest moment, ambdues impressores funcionaran sota un mateix nom de xarxa, repartint-se la feina.  

**Nota tècnica:** a la IMP_MAGATZEM_A han de quedar seleccionats els dos ports virtuals.

## 3. Desplegament automatitzat de la impressora als clients mitjançant una GPO

L'empresa no vol que els mossos de magatzem hagin d'instal·lar manualment la impressora.

- Crea una GPO (Group Policy Object) anomenada GPO_Impressores_Magatzem.  
- Utilitza l'opció "Deploy with Group Policy" des de la consola de Print Management per vincular la impressora al domini o a una Unitat Organitzativa (OU) específica on es trobi l'usuari de proves.  
- Comprova que, en iniciar sessió al client Windows 11, la impressora apareix automàticament.  

**Nota tècnica:** recordeu que caldrà tancar la sessió i/o forçar l’actualització de les directives executant l’ordre gpupdate /force.

## 4. Prova de càrrega i Seguretat

- Simulació de balanceig: Envia 10 documents seguits a la impressora del magatzem. Observa com el servidor gestiona les dues instàncies per processar les peticions.  
- **Restriccions:** Configura els "Printing Priorities" o els "Available Times" perquè la impressora de magatzem només funcioni en horari laboral (ex: de 06:00 a 22:00).  

# Material de suport

0224 SOX. Material UD8: AA3 [Moodle de l’assignatura]  

[Guia Tècnica](https://github.com/cfugarolas/activitats/blob/main/activitat3/pdf24.md): Instal·lació i configuració PDF24.

[Anar a la pàgina inicial](../README.md)
