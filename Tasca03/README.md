# Introducció

Quan el volum de negoci creix, també ho fa el volum de dades i sovint aquí comencen els problemes. La informació es compartimenta, de manera que manca una visió global de la situació.  

FoodLogistic  no ha estat una excepció, cada departament guardava la documentació de forma local. És per això, que un dels requisits de l’encàrrec que n’heu rebut és solucionar aquest problema.  

L'objectiu és implementar una infraestructura de fitxers segura, organitzada i amb control d'espai, utilitzant permisos NTFS/SMB, quotes i filtratge de fitxers (FSRM). Haureu de demostrar el domini de les tres vies d'administració: l'Explorador de fitxers, el Server Manager i PowerShell.

# Descripció de l'activitat

L'activitat es divideix en fites que simulen el procés de consultoria i implementació real.

## 1. Preparació i Seguretat de Grups (AD)

Abans de crear el servidor de fitxers, cal preparar el terreny a l'Active Directory. Sobre un domini (foodlogistic.test) on se us recomana crear una estructura de Ous coherent, que caldrà justificar per les necessitats que desenvolupareu, creeu els següents grups de seguretat:

- Administracio: Gestió de factures i albarans.  
- Transport: Xofers i caps de flota.  
- Direccio: Gerència.  

## 2. Implementació de Recursos Compartits (Tres mètodes)

Heu de crear les següents estructures de carpetes al servidor, cadascuna amb un mètode diferent:

A. Carpeta Public (Mètode: Explorador d'arxius)

- Compartiu-la per a tothom.  
- Configuració: Permisos SMB de "Lectura" i permisos NTFS de "Modificació". Verifiqueu la combinació de permisos efectiva.  

B. Carpeta Operacions (Mètode: Server Manager - FSSM)

- Instal·leu el rol File and Storage Services si no hi és.  
- Creeu el recurs compartit.  
- Fer que només es mostri pels usuaris amb accés (Acces-Based Enumeration).  
- Restricció: Només el grup Transport hi pot accedir.  

C. Carpeta Confidencial (Mètode: PowerShell bàsic)

- Creeu la carpeta Direccio$ (recurs ocult).  
- Restricció: només hi pot accedir el grup Direccio.  
- Utilitzeu el cmdlet New-SmbShare per compartir-la.  
- Configureu una GPO perquè aquesta carpeta aparegui automàticament com a unitat Z: només als usuaris de Direcció.  

D. Carpeta Confidencial (Mètode: PowerShell avançat)

- Creeu la carpeta Direccio.  
- Restricció: només hi pot accedir el grup Direccio.  
- Utilitzeu el cmdlet New-SmbShare per compartir-la i habiliteu per PowerShell l’ Access-Based Enumeration.  
- Configureu una GPO perquè aquesta carpeta aparegui automàticament com a unitat Z: només als usuaris de Direccio.  

Heu de triar entre el mètode C o D, òbviament el mètode D té una valoració més alta.

## 3. Control d'Emmagatzematge (FSRM i Quotes NTFS)

El client es queixa que els usuaris guarden fotos personals i omplen el disc. Heu d'actuar:

### Quotes NTFS (Control per Volum):

- A la unitat de dades, activeu les quotes NTFS des de les propietats del volum.  
- Establir un límit de 500 MB per defecte per a qualsevol usuari nou.  

### FSRM (Control per Carpeta):

- Instal·leu el rol File Server Resource Manager.  
- Quota de Carpeta: A la carpeta Public, apliqueu una quota de 200 MB (Hard Quota). Configureu un avís al 90% que enviï un missatge personalitzat:  
  "Compte! FoodLogístic t'informa que estàs a punt d'esgotar l'espai compartit."  
- Filtrat de Fitxers: A la carpeta Operacions, creeu un filtre que impedeixi guardar arxius executables (.exe, .msi) i fitxers d'àudio o vídeo.  

## 4. Verificació i Auditoria

Connecteu-vos des d'un client Windows 10/11 i comproveu:

- Verifiqueu l’accés i la visibilitat dels recursos per un usuari de cada grup.  
- Què passa si intenteu copiar un .exe a Operacions?  
- Si canvieu l'extensió d'un executable a .txt, el servidor el deixa passar? (Proveu el filtratge actiu).  

# Què cal lliurar

Es lliurarà un informe tècnic detallat en format MarkDown que inclogui:

- Resum de Configuració: Taula amb els noms de carpeta, camins UNC, grups amb accés i mètode de creació usat.  
- Evidències:  Captura i explicacions de les diferents configuracions realitzades en els tres apartats.  
- Proves de funcionament: comprovacions des dels clients, on es puguin comprovar que funcionen els controls d’accés, les quotes i les restriccions.

[Anar a la Guia](../Tasca03/Guia.md)    
[Anar a la pàgina inicial](../README.md)
