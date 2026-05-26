readme_content = """# Dinamiche di Opinione su Reti Sociali
### Modello Agent-Based (Mesa & NetworkX) | Progetto CMCS

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Mesa](https://img.shields.io/badge/Mesa-Agent--Based-orange.svg)](https://mesa.readthedocs.io/)
[![NetworkX](https://img.shields.io/badge/NetworkX-Complex%20Networks-brightgreen.svg)](https://networkx.org/)
[![Colab](https://img.shields.io/badge/Colab-Apri%20Notebook-yellow?logo=googlecolab)](https://colab.research.google.com/github/YOUR_USERNAME/YOUR_REPO/blob/main/Dinamiche_Social_CA_636697.ipynb)

Questo repository contiene l'implementazione di un modello di simulazione ad agenti (ABM) progettato per studiare i meccanismi di formazione dell'opinione pubblica, la polarizzazione ideologica e l'impatto degli algoritmi di raccomandazione (*Filter Bubble*) e degli influencer strategici all'interno delle reti sociali complesse.

---

## 🚀 Materiale del Progetto

Tutti i componenti fondamentali del progetto sono organizzati e pronti per la consultazione diretta:

| Risorsa | Descrizione | Link Rapido |
| :--- | :--- | :--- |
| 📓 **Jupyter Notebook** | Ambiente di computazione interattivo con il codice sorgente completo del modello, la pipeline di simulazione e la generazione dei grafici scientifici. | [💻 Apri il Notebook](./Dinamiche_Social_CA_636697.ipynb) |
| 📄 **Documentazione Tecnica** | Relazione accademica approfondita (redatta in LaTeX) con la formalizzazione matematica, i requisiti, i dettagli dell'architettura software e l'analisi topologica della rete. | [👁️ Leggi la Relazione (PDF)](./documentazione_636697.pdf) |
| 📊 **Presentazione** | Slide riassuntive utilizzate per l'esposizione orale e il public pitch del modello. | [🖼️ Apri le Slide (PDF)](./Presentazione_25-05_636697.pdf) |

---

## 📊 Anteprima Presentazione

Puoi visualizzare un'anteprima rapida e dinamica delle slide principali direttamente da qui. Cliccando sulla GIF o espandendo il menu sottostante, avrai accesso ai punti salienti affrontati durante la presentazione.

[![Anteprima Presentazione](img/presentazione_preview.gif)](./Presentazione_25-05_636697.pdf)
*Clicca sulla GIF per aprire il documento PDF completo delle slide.*

<details>
  <summary>🔍 <b>Mostra i punti chiave della presentazione</b></summary>
  
  La struttura delle slide riassume i seguenti passaggi del progetto:
  1. **Introduzione al Fenomeno:** Come i social media agiscono da motori principali per lo spostamento e la polarizzazione dell'opinione pubblica.
  2. **Formalizzazione del Modello:** Struttura della rete scale-free, dinamiche di interazione e spetti ideologici continui in $[0, 1]$.
  3. **Scenari a Confronto:** Impatto delle forze esterne (influencer statici vs. dinamici basati sulla Finestra di Overton).
  4. **Persistenza e Resilienza:** Analisi della stabilità delle *Filter Bubble* e degli effetti di polarizzazione auto-sostenuta anche post-rimozione dei nodi di disturbo.
</details>

---

## 🔬 Cosa Analizza il Progetto

Il modello quantifica l'andamento del consenso e la frammentazione sociale analizzando la complessa interazione tra fenomeni psicologici individuali e algoritmi di piattaforma:

* **Modelli di Convergenza e Tolleranza ($\epsilon$):** Basato sulla regola di **Deffuant (2000)** per la *Bounded Confidence*. Gli agenti modificano la propria opinione se la differenza ideologica rientra in una soglia di tolleranza $\epsilon$.
* **Effetto Backfire (Radicalizzazione):** Se la distanza di opinione supera la soglia critica, gli agenti non solo si ignorano, ma possono divergere radicalmente nella direzione opposta, simulando la polarizzazione del mondo reale.
* **Filter Bubble Algoritmiche & Rewiring:** Il modello simula gli algoritmi di raccomandazione modificando la topologia della rete nel tempo: gli utenti tendono a tagliare i legami con chi ha opinioni troppo distanti, aumentando la densità dei collegamenti interni alle proprie camere d'eco (*Echo Chambers*).
* **Strategie di Manipolazione dell'Opinione:** Studio comparativo sull'efficacia di account automatizzati (bot/influencer) che applicano approcci statici o la strategia evolutiva della **Finestra di Overton** (spostare la percezione accettabile in modo graduale per trascinare la media globale).

---

## 🛠️ Dettagli Implementativi ed Architettura

Il software è interamente implementato in **Python** adottando il paradigma di programmazione a oggetti integrato con i framework per modelli complessi ad agenti:

### 1. Stack Tecnologico
* **Mesa:** Gestione del ciclo di simulazione (`Schedule`), posizionamento degli agenti e raccolta dati tramite il `DataCollector`.
* **NetworkX:** Generazione, manipolazione e calcolo delle metriche strutturali su grafici di reti complesse.
* **NumPy & Pandas:** Vettorizzazione delle operazioni matematiche di aggiornamento e manipolazione dei dataset di output.
* **Matplotlib & tqdm:** Rendering dei grafici scientifici a fine simulazione e barre di avanzamento per i cicli di calcolo intensivi.

### 2. Struttura delle Classi Core
* **`UtenteRegolare(mesa.Agent)`:** Rappresenta l'utente della piattaforma. Possiede un'opinione continua $x_i \in [0, 1]$, un parametro di tolleranza $\epsilon$ e un tasso di accoglimento $\mu$. Implementa la logica di interazione di Deffuant e il meccanismo di *rewiring* algoritmico degli archi.
* **`StrategicInfluencer(mesa.Agent)`:** Agente esterno non soggetto a modifiche di opinione da parte degli altri utenti. Configurabile in modalità `statico` (opinione fissa ai poli) o `Overton` (l'opinione si sposta dinamicamente passo dopo passo per agganciare e muovere la tolleranza degli utenti regolari).
* **`SocialNetworkModel(mesa.Model)`:** Inizializza una rete scale-free basata sulla topologia di **Barabási-Albert** ($N=500$ nodi, parametro di attaccamento preferenziale $m=5$). Gestisce l'attivazione casuale degli agenti e supervisiona la robustezza strutturale complessiva.

### 3. Pipeline degli Scenari Sperimentali
Il modello esegue cicli strutturati su **5 scenari principali** (con un setup standard di 150 step e 12 run indipendenti per scenario per garantire stabilità statistica):
1. **Scenario Base:** Solo utenti regolari per analizzare la tendenza naturale alla convergenza o alla frammentazione.
2. **Influencer Statico:** Inserimento di un hub centrale fisso sul polo alto.
3. **Overton Completo:** Inserimento di un influencer dinamico che applica la traslazione progressiva della finestra di tolleranza.
4. **Due Fazioni Statiche:** Due influencer contrapposti (polo alto vs. polo basso) per studiare la polarizzazione pura.
5. **Due Fazioni Overton:** Competizione dinamica tra due strategie evolutive di manipolazione di massa.

---

## 📈 Output Grafici Generati

Al termine dell'esecuzione, il sistema esporta automaticamente nella cartella di lavoro i grafici riassuntivi delle simulazioni:

* **`sim_fazioni_confronto.png`:** Analisi comparativa temporale dell'evoluzione delle 6 metriche principali macroscopiche del sistema per tutti e 5 gli scenari.
* **`sim_epsilon_sweep.png`:** Mappatura dello spazio dei parametri: andamento della polarizzazione finale al variare sistematico di $\epsilon$.
* **`sim_resilienza.png`:** Analisi post-rimozione degli influencer; dimostra come, a causa del rewiring algoritmico, la polarizzazione rimanga cristallizzata nelle *Filter Bubble* anche eliminando i bot.
* **`evoluzione_topologia.png`:** Monitoraggio dei cambiamenti microstrutturali della rete, tracciando il numero assoluto degli archi e l'andamento della distribuzione del grado cumulativa (CCDF).

---

## 💻 Installazione e Riproducibilità

### Prerequisiti
Il progetto richiede **Python 3.9** o superiore. Installare le dipendenze richieste eseguendo dal terminale: