# MEMÒRIA TÈCNICA DE LA PROPOSTA

**Autors:** Anthony Milla i Nil Lozano     
**Client:** FoodLogístic S.A.

## 1. Introducció

**Context del projecte:**

FoodLogístic S.A. vol modernitzar la seva infraestructura tecnològica, millorar la seguretat i disposar d’una presència digital professional que reflecteixi la seva activitat i valors corporatius.

**Descripció del client:**

FoodLogístic S.A. és una empresa dedicada a la gestió logística i distribució de productes alimentaris, especialitzada en:

- Transport i distribució a temperatura controlada.
- Gestió d’estocs i magatzems.
- Subministrament a supermercats, restaurants i distribuïdors.
- Operacions 24/7 amb alta exigència de traçabilitat i fiabilitat.

El seu entorn operatiu requereix continuïtat de servei, seguretat de dades, coordinació interna eficient i una imatge corporativa sòlida.

**Objectius de la proposta:**

- Modernitzar la infraestructura TI i garantir alta disponibilitat.
- Implementar serveis al núvol per millorar la productivitat.
- Garantir seguretat i compliment RGPD.
- Desenvolupar una web corporativa funcional, moderna i legal.

**En conclusió:**  

La proposta integra infraestructura, serveis cloud, seguretat i web corporativa per garantir eficiència, continuïtat i creixement futur.

## 2. Anàlisi de necessitats

**Problemes detectats i solucions:**

| Problema                   | Impacte            | Solució                     |
|---------------------------|--------------------|-----------------------------|
| Infraestructura antiquada | Risc de fallades   | Migració a entorn virtualitzat |
| Comunicació interna deficient | Baixa productivitat | Suite col·laborativa cloud |
| Falta de seguretat        | Vulnerabilitat     | MFA, xifratge, firewall     |
| Sense web corporativa     | Mala imatge        | Web moderna + RGPD          |

**Necessitats del client:**

- Disponibilitat 24/7
- Seguretat reforçada
- Comunicació eficient
- Web corporativa legal

**Requisits tècnics:**

- Escalabilitat
- Redundància
- Integració cloud
- Compliment RGPD

## 3. Proposta de solució

| 3.1 Infraestructura i alta disponibilitat |
|----------------------------------------|

**Descripció:**

Infraestructura basada en servidors virtualitzats, amb redundància, còpies de seguretat i firewall perimetral.

**Diagrama d’arquitectura (PlantUML);**

**Codi:**

```
@startuml
skinparam rectangleStyle rounded
skinparam shadowing false

actor Usuari as U

U --> Firewall

rectangle "Xarxa Interna" {
    Firewall --> Switch
    Switch --> Hypervisor1
    Switch --> Hypervisor2

    rectangle "Hypervisor 1" {
        Hypervisor1 --> VM1 : Servidor Web
        Hypervisor1 --> VM2 : Servidor Aplicacions
    }

    rectangle "Hypervisor 2" {
        Hypervisor2 --> VM3 : Servidor Backups
        VM3 --> NAS : NAS Backups
    }
}
@enduml
```

![Diagrama d’arquitectura (PlantUML);](Img/Imatge01.jpg)

**Components:**

| Component          | Funció          | Quantitat | Justificació             |
|--------------------|-----------------|-----------|---------------------------|
| Firewall           | Protecció       | 1         | Seguretat                |
| NAS                | Backups         | 1         | Recuperació de desastres |
| Servidors virtuals | Serveis interns | 2         | Escalabilitat            |

| 3.2 Serveis al núvol |
|----------------------------------------|

**Comparativa:**

| Característica   | Google Workspace | Microsoft 365 |
|------------------|------------------|----------------|
| Correu           | Gmail            | Outlook        |
| Emmagatzematge   | Drive            | OneDrive       |
| Col·laboració    | Docs/Sheets      | Office Online  |
| Preu             | €                | €€             |

**Justificació:**

Hem escollit Microsoft 365 per integració empresarial, seguretat i eines completes d’ofimàtica.



[Anar a l'enunciat](../Producte01/README.md)      
[Anar a la pàgina inicial](../README.md)
