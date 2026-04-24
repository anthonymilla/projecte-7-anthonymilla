# SERVIDOR DE FITXERS

## Introducció

Quan el volum de negoci creix, també ho fa el volum de dades i sovint aquí comencen els problemes. La informació es compartimenta, de manera que manca una visió global de la situació.

FoodLogistic no ha estat una excepció, cada departament guardava la documentació de forma local. És per això, que un dels requisits de l’encàrrec que n’heu rebut és solucionar aquest problema.

L'objectiu és implementar una infraestructura de fitxers segura, organitzada i amb control d'espai, utilitzant permisos NTFS/SMB, quotes i filtratge de fitxers (FSRM). Haureu de demostrar el domini de les tres vies d'administració: l'Explorador de fitxers, el Server Manager i PowerShell.

## Descripció de l'activitat

**L'activitat es divideix en fites que simulen el procés de consultoria i implementació real.**

Domini:



1. Preparació i Seguretat de Grups (AD)

Abans de crear el servidor de fitxers, cal preparar el terreny a l'Active Directory. Sobre un domini (foodlogistic.test) on se us recomana crear una estructura de OUs coherent, que caldrà justificar per les necessitats que desenvolupareu, creeu els següents grups de seguretat:

Administracio: Gestió de factures i albarans.

Transport: Xofers i caps de flota.

Direccio: Gerència.

Preparem el terreny a l'Active Directory, sobre un domini; foodlogistic.test, on crearem una estructura de OUs (Usuaris i Grups), ja que així no serà lliós i podrem dividir correctament aquests per les necessitats que desenvoluparem, creem els següents grups de seguretat corresponentment:

2. Implementació de Recursos Compartits (Tres mètodes)

Heu de crear les següents estructures de carpetes al servidor, cadascuna amb un mètode diferent:

A. Carpeta Public (Mètode: Explorador d'arxius):

Compartiu-la per a tothom.

Configuració: Permisos SMB de "Lectura" i permisos NTFS de "Modificació". Verifiqueu la combinació de permisos efectiva.

Creem la carpeta; Public (Mètode: Explorador d'arxius), la compartim per a tothom i la configurem: Permisos SMB de "Lectura" i permisos NTFS de "Modificació".

B. Carpeta Operacions (Mètode: Server Manager - FSSM):

Instal·leu el rol File and Storage Services si no hi és.

Ja el tenim instal·lat:

Creeu el recurs compartit.

Creem el recurs compartit (Click dret i New Share…):

Fer que només es mostri pels usuaris amb accés (Acces-Based Enumeration).

Seguidament en Configure share setttings (Configura els setttings de compartició), en Other Settings (Altres paràmetres) marquem que: només es mostri pels usuaris amb accés (Enable acces-based enumeration).

Confirm selections (Confirmem les seleccions):

Restricció: Només el grup Transport hi pot accedir.

En restricció que: Només el grup Transport hi pugui accedir:

C. Carpeta Confidencial (Mètode: PowerShell bàsic):

Creeu la carpeta Direccio$ (recurs ocult).

Restricció: només hi pot accedir el grup Direccio.

Utilitzeu el cmdlet New-SmbShare per compartir-la.

Configureu una GPO perquè aquesta carpeta aparegui automàticament com a unitat Z: només als usuaris de Direcció.

D. Carpeta Confidencial (Mètode: PowerShell avançat):

Creeu la carpeta Direccio.

Restricció: només hi pot accedir el grup Direccio.

Utilitzeu el cmdlet New-SmbShare per compartir-la i habiliteu per PowerShell l’ Access-Based Enumeration.

Creem la carpeta Direccio i restricció: només hi pot accedir el grup Direccio.

Utilitzem el cmdlet New-SmbShare per compartir-la i habilitem per PowerShell l’Access-Based Enumeration (Enumeració Basada en Accés).

Configureu una GPO perquè aquesta carpeta aparegui automàticament com a unitat Z: només als usuaris de Direccio.

Configurem una GPO perquè aquesta carpeta aparegui automàticament com a unitat Z: només als usuaris de Direccio (Anthony Milla en aquest cas). Per això obrim la Default Domain Policy (Política de Domini Predeterminada). Anem a: User Configuration (Configuració d’Usuari), Preferences (Preferències), baixem el desplegable; Windows Settings (Configuració de Windows), Drive Maps (Mapes d’Unitats), clic dret; New (Nou) i Mapped Drive (Unitat Assignada).

Configurem:

Action (Acció): Update (Actualitzar)

Location (Ubicació): \\\DC17\Direccio

Drive Letter (Lletra d’unitat): Use Z (Usar Z)

Marquem: Show this drive (Mostrar aquesta unitat)

Aquesta GPO només s’aplicarà als usuaris del grup Direccio (Anthony Milla en aquest cas).

Ara anem a la Default Domain Policy (Política de Domini Predeterminada), en Computer Configuration (Configuració de l’Equip), en Preferences (Preferències), baixem el desplegable; Windows Settings (Configuració de Windows), Network Shares (Comparticions de Xarxa), clic dret; New (Nou) i Network Share (Recurs Compartit).

Configurem:

Action (Acció): Update (Actualitzar)

Share name (Nom del recurs compartit): direccio

Folder path (Ruta de la carpeta): \\\DC17\Direccio

Access‑Based Enumeration (Enumeració Basada en Accés): marquem Enabled (Activat)

Això reforça la configuració del recurs compartit.

Intentem accedir a \\\DC17\Direccio amb l'usuari Jhon Justiniano i no deixa accedir ja que no té permisos (no és del grup Direccio).

Ara amb l'usuari Anthony Milla (l'usuari del grup Direccio) l'Unitat Z és visible i accessible.

I podem veure que l'usuari del grup Direccio pot obrir-la.

Heu de triar entre el mètode C o D, òbviament el mètode D té una valoració més alta.

3. Control d'Emmagatzematge (FSRM i Quotes NTFS)

El client es queixa que els usuaris guarden fotos personals i omplen el disc. Heu d'actuar:

Quotes NTFS (Control per Volum):

A la unitat de dades, activeu les quotes NTFS des de les propietats del volum.

Primerament activem les quotes NTFS.

Establir un límit de 500 MB per defecte per a qualsevol usuari nou.

Establim un límit de 500 MB per defecte per a qualsevol usuari nou:

FSRM (Control per Carpeta):

Instal·leu el rol File Server Resource Manager.

Quota de Carpeta: A la carpeta Public, apliqueu una quota de 200 MB (Hard Quota). Configureu un avís al 90% que enviï un missatge personalitzat: "Compte! FoodLogístic t'informa que estàs a punt d'esgotar l'espai compartit."

Instal·lem el rol File Server Resource Manager. A la carpeta Public, apliquem una quota de 200 MB (Hard Quota). Configurem un avís al 90% que enviï un missatge personalitzat que serà: "Compte! FoodLogístic t'informa que estàs a punt d'esgotar l'espai compartit."

Filtrat de Fitxers: A la carpeta Operacions, creeu un filtre que impedeixi guardar arxius executables (.exe, .msi) i fitxers d'àudio o vídeo.

A la carpeta Operacions, creem un filtre que impedeixi guardar arxius executables (.exe, .msi) i fitxers d'àudio o vídeo.

4. Verificació i Auditoria

Connecteu-vos des d'un client Windows 10/11 i comproveu:

Verifiqueu l’accés i la visibilitat dels recursos per un usuari de cada grup.

Usuari Anthony Milla, pot veure la carpeta Direcció:

Usuari Jhon Justiniano, pot veure la carpeta Operacions:

Usuari Nil Lozano, pot veure la carpeta public:

Què passa si intenteu copiar un .exe a Operacions?

El servidor el bloqueja. FSRM té un file screen actiu sobre C:\Operacions i, tal com es veu al document, quan intentem copiar WinSCP.exe apareix: “Acceso a la carpeta de destino denegado”.

Si canvieu l'extensió d'un executable a .txt, el servidor el deixa passar? (Proveu el filtratge actiu).

També el bloqueja. El filtratge és actiu, així que no es deixa enganyar per l’extensió. Al document es veu que, tot i renombrar-lo a .txt, torna a sortir: “Necesita permisos para realizar esta acción”.

Resum de Configuració: Taula amb els noms de carpeta, camins UNC, grups amb accés i mètode de creació usat.

| **Carpeta**   | **Camí UNC**           | **Grup(s) amb Accés** | **Permisos**                                   | **Mètode de Creació** |
|-----------|---------------------|--------------------|---------------------------------------------|--------------------|
| **Public**    | \\\\DC17\\public    | Everyone           | SMB: Lectura / NTFS: Modificació            | Explorador d’Arxius |
| **Operacions**| \\\\DC17\\Operacions| Transport          | Full Control                                | Server Manager (FSSM) |
| **Direccio**  | \\\\DC17\\Direccio  | Direccio           | Full Control + ABE activat                  | PowerShell avançat (New-SmbShare + Set-SmbShare) + GPO unitat Z: només als usuaris de Direccio |

[Anar a l'enunciat](../Tasca03/README.md)      
[Anar a la pàgina inicial](../README.md)
