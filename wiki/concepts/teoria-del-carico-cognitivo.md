---
title: "Teoria del Carico Cognitivo"
type: concept
status: draft
created: 2026-07-04
updated: 2026-07-04
tags: [apprendimento, psicologia-cognitiva, produttività, sviluppo-software]
related: ["concepts/memoria-di-lavoro.md", "concepts/build-a-second-brain.md"]
---

## Summary

Il **carico cognitivo** è la quantità totale di attività mentale richiesta alla
[memoria di lavoro](./memoria-di-lavoro.md) per elaborare e immagazzinare informazioni
durante un compito. La **Teoria del Carico Cognitivo (TCC)**, formalizzata da John
Sweller tra il 1999 e il 2019 a partire da studi di psicologia degli anni '50-'70,
sostiene che l'apprendimento e la performance crollano quando la memoria di lavoro —
l'unica risorsa mentale realmente limitata — viene sovraccaricata. Applicata allo
sviluppo software e alle organizzazioni IT, la teoria inquadra il cervello come il
vero "collo di bottiglia" produttivo, con un costo stimato dalle fonti in ~322 miliardi
di dollari l'anno.

## Details

### Definizione e i tre tipi di carico

Il carico cognitivo è lo sforzo che la mente compie per processare informazioni in un
dato momento. Si suddivide in tre tipi (analogia della birra: la birra è ciò che
vogliamo, la schiuma è spreco):

- **Carico Intrinseco** (la birra) — la difficoltà inerente all'argomento. È ciò che
  vogliamo apprendere: va **ottimizzato**, non eliminato.
- **Carico Estraneo** (la schiuma) — informazioni e distrazioni superflue che affaticano
  inutilmente il cervello. Va **minimizzato**.
- **Carico Pertinente / Essenziale** — lo sforzo *utile* che serve a consolidare le
  informazioni costruendo schemi mentali e legami tra concetti.

Obiettivo pratico: **ottimizzare l'intrinseco e lasciare spazio al pertinente,
riducendo al massimo l'estraneo**.

### Sintomi del sovraccarico

Difficoltà di concentrazione e perdita di focus; esaurimento a fine giornata anche
senza aver scritto codice; disturbi del sonno; ansia, irritabilità e nervosismo (che
scaricati sul team minano la *retention*); nei casi gravi sintomi fisici (mal di testa,
disturbi gastrointestinali, tensione muscolare, tachicardia). Non esiste una misura
oggettiva diretta ("nessun semaforo accanto alla testa"), quindi si ragiona per segnali
indiretti.

### Bias decisionali sotto carico

Con la memoria di lavoro satura le capacità decisionali calano e compaiono bias:

- **Bias di conferma** — si sceglie ciò che conferma lo stato attuale (es. "va bene il
  deploy via FTP che ha sempre funzionato" pur di non imparare Docker).
- **Bias di negatività** — si vede tutto in negativo ("questo linguaggio fa schifo").
- **Bias dello *status quo*** — decisioni impulsive per mantenere il noto ed evitare
  scelte di cui non si valutano bene le conseguenze.
- **Bias della tendenza centrale** — nelle valutazioni si tende al voto medio (sempre
  "3 su 5"), evitando gli estremi e restando nella mediocrità.

### I cinque pilastri (ABCDE)

- **A — Architettura della Memoria**: Environment (stimoli illimitati), Memoria a Lungo
  Termine (praticamente illimitata), Memoria di Lavoro (l'unica limitata → il collo di
  bottiglia). Le informazioni *nuove* pesano molto più di quelle vecchie e complesse già
  consolidate. Vedi [memoria di lavoro](./memoria-di-lavoro.md).
- **B — Biologia della Conoscenza**: *primaria* (implicita, acquisita per evoluzione:
  parlare, camminare — non richiede studio cosciente) vs *secondaria* (esplicita,
  faticosa, cosciente: usare un computer, studiare Event Sourcing).
- **C — Categorizzazione del Carico**: i tre tipi intrinseco/estraneo/pertinente visti
  sopra.
- **D — Domini**: *generali* (competenze trasferibili, es. saper parlare) vs *specifici*
  (legati a un'area, es. Event Sourcing). La differenza tra esperto e principiante sta
  nella quantità di conoscenza specifica accumulata (es. scacchi: il principiante calcola
  centinaia di mosse e si sovraccarica, l'esperto riconosce la configurazione e recupera
  un *chunk* pronto).
- **E — Elementi / Interattività degli elementi**: il carico dipende dal *numero* di
  elementi e da *quanto interagiscono* tra loro. Alta interattività (passi interdipendenti
  di un rilascio complesso, un diagramma elettrico) = carico alto; isolare gli elementi in
  chunk indipendenti lo riduce. Le conoscenze pregresse abbassano l'interattività.

### Tecniche di gestione

**Ridurre il carico estraneo**
- *Ridurre la ridondanza*: non presentare la stessa informazione su canali multipli
  identici (es. leggere ad alta voce una slide che il pubblico sta già leggendo).
- *Evitare la split attention*: non spargere le informazioni (testo + link a Figma +
  video + repo) costringendo a saltare tra fonti.

**Ottimizzare il carico intrinseco**
- *Preteaching*: preparare in anticipo (es. agenda del meeting inviata prima) così che
  chi partecipa recuperi elementi in anticipo e affronti meno novità. Attenzione: se
  l'audience non si prepara, il materiale progettato su quel presupposto diventa carico
  estraneo.
- *Segmentazione / Sequencing*: spezzare argomenti complessi in attività isolate a bassa
  interattività, con una gerarchia logica fornita da un esperto. Due approcci:
  *part-whole* (imparo sottrazioni e tabelline → poi le divisioni) e *whole-part*
  (obiettivo maratona → dimagrimento, resistenza…).
- *Sviluppo iterativo* (metafora di Super Pang, da Jenny Martin/OOPSI): spezzare il
  problema grande in "palle" più piccole e distruggerne un gruppo alla volta, evitando sia
  il blocco monolitico sia il proliferare di sotto-storie iper-dettagliate che tornano a
  interagire — in linea con i principi Agile/XP.

### Rilevanza organizzativa

Il carico cognitivo è descritto dalle fonti come la "crisi nascosta" delle organizzazioni
IT moderne, aggravata da due fattori: il rapido cambiamento tecnologico (formazione
continua) e gli ambienti di lavoro distribuiti (meno feedback visivo/tattile). Il
riferimento è al lavoro di Laura Weis (psicologa del lavoro) e Manuel Pais (co-autore di
*Team Topologies*). Vedi la domanda aperta su
[Team Topologies e l'articolo di IT Revolution](../questions/ingerire-team-cognitive-load-it-revolution.md).

## Open Questions

- Approfondire il legame con *Team Topologies* (Skelton & Pais) e ingerire l'articolo
  originale di IT Revolution → vedi
  [domanda aperta](../questions/ingerire-team-cognitive-load-it-revolution.md).
- I bias decisionali sotto carico potrebbero meritare una pagina concetto propria
  ("bias cognitivi") se altre fonti li toccheranno.

## Sources

- [La Teoria del Carico Cognitivo — riflessioni di un dev (codiceplastico.com)](../sources/2026-07-04-teoria-del-carico-cognitivo.md)
