# Software Security & Challenges

Questo repository contiene gli elaborati d'esame per il corso di **Software Security**, suddivisi in due macro-progetti: un'analisi approfondita di un campione malware reale e una raccolta di soluzioni a challenge di sicurezza informatica.

## 🎓 Informazioni sul Corso

* **Università:** Università degli Studi di Napoli Federico II
* **Corso di Laurea:** Laurea Magistrale in Ingegneria Informatica
* **Corso:** Software Security
* **Professore:** Roberto Natella
* **Autore:** Pietro Conte

---

## 🦠 Progetto 1: Malware Analysis & Detection Engineering

Analisi strutturale, comportamentale e metodologica di un dropper .NET multi-payload appartenente alla macro-famiglia degli Infostealer (RedLine Stealer e ClipBanker).

### 🔍 Fasi dell'Analisi
*   **Analisi Statica:** Ispezione del formato PE, analisi dell'entropia (identificazione di payload GZip compressi) e reverse engineering del bytecode .NET tramite dnSpy per ricostruire la logica "Drop-and-Execute". Valutazione delle capabilities tramite Mandiant capa.
*   **Analisi Dinamica:** Esecuzione in ambiente isolato (VM host-only). Network sinkholing tramite FakeNet-NG, monitoraggio I/O con Process Monitor (Procmon) ed esplorazione dei processi con Process Explorer. Identificazione dell'uso di mutex per il controllo di concorrenza.
*   **Detection Engineering:**
    *   **YARA:** Sviluppo di regole multi-stadio per l'identificazione statica del dropper e del payload, basate su pattern di estrazione e refusi tipografici (es. "Get Cliboard Address").
    *   **Sigma:** Creazione di regole comportamentali per l'individuazione della tecnica Drop-and-Execute da directory `%TEMP%` sfruttando i log di Sysmon (EventID 1).

---

## ⚔️ Progetto 2: Software Security Challenges

Risoluzione pratica di scenari d'attacco e implementazione di difese in molteplici domini della sicurezza software.

### 🛡️ Aree di Intervento
*   **Memory Corruption (Buffer Overflow):**
    *   Sfruttamento di vulnerabilità su architetture x86 e x64.
    *   Iniezione di shellcode (Reverse Shell) e sovrascrittura di indirizzi di ritorno.
    *   Bypass delle difese di sistema e compilazione custom.
*   **Web Security:**
    *   *Cross-Site Request Forgery (CSRF):* Analisi e mitigazione tramite policy `SameSite` (Lax, Strict, Normal).
    *   *Cross-Site Scripting (XSS):* Sviluppo di attacchi Stored XSS e di un worm auto-propagante. Mitigazione tramite Content Security Policy (CSP).
    *   *SQL Injection:* Manipolazione di query di `UPDATE` e cifratura SHA-1. Messa in sicurezza tramite Prepared Statements.
*   **Fuzzing & Memory Errors:**
    *   Fuzzing della libreria OpenSSL tramite American Fuzzy Lop (AFL) e AddressSanitizer (ASAN) per individuare la vulnerabilità Heartbleed (buffer over-read).
    *   Diagnostica dei crash tramite GDB e Valgrind.
    *   Ottimizzazione del throughput tramite modalità persistente (AFL_LOOP).
*   **Static Analysis (CodeQL):**
    *   Taint Tracking sul codice sorgente del bootloader U-Boot per individuare vulnerabilità di Remote Code Execution (RCE).
    *   Sviluppo di classi personalizzate e predicati di sanitizzazione (Barriers).
    *   Integrazione e automazione delle query di sicurezza tramite GitHub Actions (DevSecOps).
*   **Cyber Threat Intelligence (CTI):**
    *   Emulazione della kill chain del malware fileless Astaroth (Dropper, BITSAdmin, ADS, DLL Side-Loading).
    *   Mappatura delle Tattiche, Tecniche e Procedure (TTPs) sul framework MITRE ATT&CK.
    *   Creazione di regole Sigma e Snort per il rilevamento di beaconing e query DNS sospette.

---

## ⚙️ Tecnologie e Strumenti
*   **Reverse Engineering & Malware Analysis:** dnSpy, PeStudio, PEiD, Process Monitor, Process Explorer, FakeNet-NG, Wireshark, IDA Pro.
*   **Detection & CTI:** YARA, Sigma, Zircolite, Snort, Mandiant capa, yarGen.
*   **Vulnerability Exploitation:** GDB, Pwntools, Metasploit, AFL (American Fuzzy Lop), Valgrind.
*   **Code Analysis:** CodeQL, GitHub Actions.
