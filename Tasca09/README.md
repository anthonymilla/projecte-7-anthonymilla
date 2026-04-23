Un dels errors més habituals en equips tècnics novells és confondre “fer feina” amb “gestionar un projecte”. 

Començar a configurar servidors, desenvolupar una web o desplegar serveis sense una planificació rigorosa acostuma a provocar retards, colls d’ampolla i solucions improvisades.

En aquest punt del projecte, la direcció de FoodLogístics S.A. no vol només una proposta tècnica: vol garanties.

Vol saber:

- Quan estaran les solucions operatives  
- Quin ordre seguireu  
- Què passarà si alguna tasca es retarda  
- Si sou capaços de treballar com un equip professional  

Per tant, el vostre objectiu no és “fer un Gantt”, sinó demostrar que sabeu planificar un projecte real amb criteri tècnic i organitzatiu.

Treballareu com a equip de projecte per construir una planificació completa i realista del desplegament de la solució per a FoodLogístics S.A., utilitzant un diagrama de Gantt generat amb [PlantUML](https://plantuml.com/es/) (UMLTree).  

[Editor per veure codi UMLTree](https://www.planttext.com/)  

L’activitat es divideix en fases.

## Fase 1: Anàlisi real del projecte (pensament estructural)

### 1.1 Identificació de tasques i dependències

A partir de les tasques reals del projecte (T01–T08):  
- Identifiqueu:  
  - Ordre lògic d’execució  
  - Tasques que poden anar en paral·lel  
  - Tasques bloquejants  

Heu de respondre preguntes com:  
- Quines tasques no poden començar sense haver-ne acabat una altra?  
- On poden aparèixer colls d’ampolla?  
- Quines tasques són més crítiques per al projecte?  

### 1.2 Identificació del camí crític

Determineu:  
- Quines tasques, si es retarden, afecten tot el projecte  
- Quines tenen marge (slack)  

No es tracta només d’identificar-lo, sinó d’entendre’l.

---

## Fase 2: Estimació d’esforç amb criteri (ús d’IA guiat)

Heu d’estimar la durada de cada tasca en hores, però no de forma arbitrària.  

Per cada tasca, haureu d’analitzar com a mínim aquests factors:

### Factors obligatoris d’estimació

Per cada tasca, tingueu en compte:  
- Temps de comprensió (lectura, anàlisi)  
- Temps de recerca (si cal)  
- Temps d’implementació tècnica  
- Temps de proves i errors  
- Temps de documentació  
- Coordinació amb l’equip  
- Possibles interrupcions (classes, exàmens, altres tasques)  
- Temps de marge (imprevistos)  

### Ús d’IA (obligatori i guiat)

Heu d’utilitzar IA com a assistent, però amb criteri.  

---

## Fase 3: Assignació de recursos (treball en equip real)

Distribuïu les tasques entre els membres de l’equip:  
- Qui fa què  
- Si hi ha tasques compartides  
- Si hi ha dependència entre membres  

👉 Heu d’evitar:  
- Sobrecàrrega d’una persona  
- Temps morts en altres  

---

## Fase 4: Construcció del diagrama de Gantt (UMLTree)

Utilitzant **PlantUML (UMLTree):**  

El diagrama ha de mostrar:  
- Tasques del projecte (T01–T08)  
- Durada de cada tasca  
- Dependències entre tasques  
- Execució en paral·lel  
- Visió temporal de les 3 setmanes  

👉 No és només un dibuix: ha de reflectir decisions reals.

---

## Fase 5: Pla de contingència (pensament professional)

Identifiqueu com a mínim:  
- 2 riscos crítics (reals, invasió zombi o abducció d’un alien no val)  
- Impacte en el projecte  
- Estratègia de mitigació  

👉 Exemple:  
- Retard en servidor → buffer o paral·lelització  
- Problemes amb cloud → alternativa definida  

---

## Què cal lliurar

El lliurament s’haurà de fer dins del repositori del projecte i haurà d’incloure, com a mínim, els següents elements:

### 1. Document de planificació (`README.md`)

Ubicat a la carpeta:  

`/P01/Planificacio/`  

Aquest document haurà de funcionar com a **informe professional de planificació** i incloure:  
- una breu introducció al context i objectiu de la planificació,  
- l’explicació de l’ordre de les tasques i les seves dependències,  
- la justificació de les estimacions temporals,  
- una explicació setmana a setmana de com es distribueix el treball,  
- les decisions més importants preses per l’equip,  
- i una reflexió sobre els possibles colls d’ampolla o punts crítics del projecte.  

El document ha d’estar redactat amb claredat, ben estructurat i amb un format visual correcte. Cal incorporar captures de pantalla, imatges del diagrama i evidències útils per entendre el procés seguit.

---

### 2. Codi PlantUML i imatge del diagrama de Gantt

Dins la mateixa carpeta de planificació, haureu d’incloure:  
- l’arxiu amb el **codi PlantUML** utilitzat per generar el diagrama,  
- i la **imatge exportada del diagrama de Gantt.**  

El diagrama ha de mostrar de forma clara:  
- les **4 setmanes de planificació,**  
- les **tasques del projecte,**  
- els possibles **solapaments o paral·lelismes,**  
- i la relació temporal entre activitats i productes.  

No n’hi ha prou amb generar el diagrama: aquest ha de ser coherent amb el contingut explicat al `README.md.`

---

### 3. Matriu d’assignació de responsabilitats (RACI)

Haureu d’elaborar una **taula RACI** on es vegi clarament quin paper assumeix cada membre de l’equip en cada tasca del projecte.  

La matriu haurà d’indicar, com a mínim:  
- qui és **responsable** d’executar la tasca,  
- qui n’és **responsable final** o validador,  
- qui ha de ser **consultat,**  
- i qui ha de ser simplement **informat.**  

L’objectiu és demostrar que l’equip no només ha repartit feina, sinó que ha pensat com s’organitza professionalment la coordinació del projecte.

---

### 4. Taula de riscos i contingències

Haureu d’incloure una taula on identifiqueu possibles imprevistos que podrien afectar el desenvolupament del projecte i com penseu reaccionar-hi.  

Per a cada risc, cal indicar:  
- quin és el problema o incidència possible,  
- quina part del projecte podria afectar,  
- quin impacte podria tenir sobre la planificació,  
- i quina mesura de contingència o resposta proposa l’equip.  

No es tracta només de dir “pot haver-hi problemes”, sinó de demostrar que sabeu anticipar-vos i prendre decisions de manera professional.

---

## Important

Tots aquests elements han d’estar **connectats entre si.** És a dir:  
- el `README.md` ha d’explicar la lògica de la planificació,  
- el diagrama de Gantt l’ha de representar visualment,  
- la matriu RACI ha de mostrar com es reparteix el treball,  
- i la taula de riscos ha de demostrar que heu previst possibles desviacions.  

El conjunt del lliurament ha de transmetre la idea que sou un equip capaç de **planificar, coordinar i justificar** l’execució d’un projecte real.

---

## Preguntes clau que heu de repondre obligatòries al README

Per forçar reflexió real:  
- Quina és la tasca més crítica del projecte i per què?  
- On heu detectat el principal coll d’ampolla?  
- Quina decisió de planificació ha estat més difícil?  
- Heu hagut de modificar alguna estimació inicial? Per què?  
- Quin risc podria fer fracassar el projecte?  
- Si tinguéssiu una setmana més, què canviaríeu?  

---

## Criteris de qualitat

Es valorarà:  
- Coherència del Gantt amb el projecte  
- Realisme de les estimacions  
- Comprensió de dependències  
- Capacitat d’anticipar problemes  
- Qualitat del README (professional, estructurat, justificat)  
- Ús crític de la IA (no superficial)

[Anar a la Solució](../Tasca09/Solucio.md)   
[Anar a la pàgina inicial](../README.md)
