---
name: viaplay-sport
description: Hämtar Viaplay:s TV-tablå för helgmotorsport (fredag–söndag) och presenterar den som markdown. Använd när användaren frågar om "viaplay schema", "viaplay sport helgen", "motorsport tablå", "vad körs på viaplay", "formel 1 viaplay", "motogp viaplay", "indycar viaplay", "helgens motorsport" eller liknande. Trigga alltid när Viaplay + motorsport nämns, eller när användaren vill veta vad som sänds på helgen. Serier som täcks: Formel 1, Formel 2, MotoGP, IndyCar.
---

# Viaplay Motorsport – Helgschema

Hämta och presentera Viaplay:s TV-tablå för kommande fredag–söndag, enbart för serierna: Formel 1, Formel 2, MotoGP och IndyCar.

## Steg 1 – Beräkna helgdatumen

Räkna ut vilket datum som är kommande fredag, lördag och söndag utifrån dagens datum.
- Om idag är lördag eller söndag: visa innevarande helg.
- Om idag är måndag–fredag: visa närmast kommande fredag–söndag.

## Steg 2 – Hämta schema parallellt

Gör **fem parallella** WebFetch-anrop med prompten:
> "Lista alla sändningar med datum (YYYY-MM-DD), starttid, sluttid och sessionens namn, t.ex. träning, kval, sprint, race, studio, eftersändning. Inkludera all schemainformation du hittar."

| Källa | URL |
|-------|-----|
| Motorsport-översikt | `https://viaplay.se/sport/motorsport` |
| Formel 1 | `https://viaplay.se/sport/motorsport/formel-1` |
| Formel 2 | `https://viaplay.se/sport/motorsport/formel-2` |
| MotoGP | `https://viaplay.se/sport/motorsport/motogp` |
| IndyCar | `https://viaplay.se/sport/motorsport/indycar` |

Slå ihop resultaten och ta bort dubbletter. Motorsport-översiktssidan brukar ge den bredaste datan.

## Steg 3 – Filtrera och sortera

Välj ut sändningar där:
1. Serien är Formel 1, Formel 2, MotoGP eller IndyCar (inte Formel 3, WTCR etc.)
2. Datumet är fredag, lördag eller söndag för den beräknade helgen

Inkludera alla sessionstyper: träning, kval, sprint, race, studio, eftersändning.

## Steg 4 – Konvertera tider till svensk tid

Tiderna på Viaplay visas i UTC. Konvertera alltid till **svensk tid**:
- Vintertid (nov–mars): UTC+1 (CET)
- Sommartid (apr–okt): UTC+2 (CEST)

## Steg 5 – Presentera som markdown

Gruppera per dag, sortera kronologiskt. Använd detta exakta format:

```markdown
## Viaplay Motorsport – [Fredag d MMM] till [Söndag d MMM yyyy]

### Fredag [d MMMM]
| Tid   | Serie      | Session                         |
|-------|------------|---------------------------------|
| 05:50 | Formel 1   | Australiens GP – Träning 2      |
| 20:00 | IndyCar    | Good Ranchers 250 – Kval        |

### Lördag [d MMMM]
| Tid   | Serie    | Session |
|-------|----------|---------|
...

### Söndag [d MMMM]
| Tid   | Serie    | Session |
|-------|----------|---------|
...

> Tider i CET/CEST. Källa: [viaplay.se/sport/motorsport](https://viaplay.se/sport/motorsport)
```

Om en dag saknar sändningar för de valda serierna: skriv `_Inga sändningar_` under den rubriken.

## Felhantering

- Om WebFetch misslyckas för enskild serie: notera `_Data saknas_` för den serien och fortsätt.
- Om inga data hittas alls: använd WebSearch med `site:viaplay.se [serie] schema [helgdatum]`.
- Om tider saknas för en session: ta med händelsen men markera tiden med `?:??`.
