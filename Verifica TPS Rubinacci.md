# RELAZIONE APPLICAZIONE

L’applicazione fornita è un servizio [**web service**](#tecnologia-usata) di tipo RESTful scritto in linguaggio [Python](#python).

La funzione di questa applicazione è gestire una lista di utenti tramite diverse API HTTP.  
Quando l’app è avviata, si possono fare diverse operazioni: si può vedere l’elenco completo degli utenti, si può cercare un singolo utente usando il suo ID, si può aggiungere un nuovo utente, si può anche modificare un utente esistente oppure eliminarlo. Tutto questo avviene semplicemente inviando delle richieste al server, che risponde con dati in formato JSON.

Attraverso questi endpoint, è possibile effettuare operazioni di tipo CRUD:

- **C**reare un nuovo utente (POST)

- **R**icercare o leggere uno o più utenti (GET)

- **U**pdate un utente (PUT)

- **D**elete un utente (DELETE)

# **Commento codice applicazione**

## DATABASE

| users \= \[	{"id": 1, "name": "Alice"},	{"id": 2, "name": "Bob"}\] |
| :---- |

All’inizio del file è presente questa simulazione di database che contiene due utenti.

## DEFINIZIONE ENDPOINT

| @app.route('/users', methods=\['GET'\])def get\_users():	return jsonify(users) |
| :---- |

Questa sezione restituisce l'elenco completo degli utenti.

| @app.route('/users/\<int:user\_id\>', methods=\['GET'\])def get\_user(user\_id):	user \= next((u for u in users if u\["id"\] \== user\_id), None)	return jsonify(user) if user else ("Utente non trovato", 404\) |
| :---- |

Questa altra parte restituisce l'utente con ID specifico

| @app.route('/users', methods=\['POST'\])def add\_user():	new\_user \= request.json	users.append(new\_user)	return jsonify(new\_user), 201 |
| :---- |

Qui tramite il metodo HTTP POST è possibile aggiungere un nuovo utente all’elenco.

| @app.route('/users/\<int:user\_id\>', methods=\['PUT'\])def update\_user(user\_id):	user \= next((u for u in users if u\["id"\] \== user\_id), None)	if user:    	user.update(request.json)    	return jsonify(user)	return ("Utente non trovato", 404\) |
| :---- |

Qui tramite il metodo PUT è possibile aggiornare i dati di un utente già esistente

| @app.route('/users/\<int:user\_id\>', methods=\['DELETE'\])def delete\_user(user\_id):	global users	users \= \[u for u in users if u\["id"\] \!= user\_id\]	return ("Utente eliminato", 200\) |
| :---- |

Con DELETE si può rimuovere un utente specifico.

![][image1]  
Eseguendo l’applicativo e inserendo [http://127.0.0.1:5000](http://127.0.0.1:5000) nell’URL questo è l’output visionato con /users/ quindi eseguendo un GET di tutti gli elementi del database.

# TECNOLOGIA USATA {#tecnologia-usata}

Come detto in precedenza si tratta di un WEB SERVICE di tipo RESTful.

### **che cos’è un web service?**

Un web service RESTful è un'interfaccia che consente a diversi sistemi di comunicare tra loro via protocollo HTTP, scambiandosi dati in formato JSON o XML.

Utilizza i metodi del protocollo HTTP per le comunicazioni.

**perché si usa?**

* È semplice e leggibile

* È compatibile con browser, app, altri server, altri dispositivi

* È indipendente dal linguaggio di programmazione

**esempi di uso**

I web service sono spesso utilizzati per esempio da app mobile che prendono dati dal server.

Oppure dai siti e-commerce che salvano le operazioni tramite la POST.

# **FLASK**

Flask è il framework che viene usato in questa applicazione, ed è importato con la riga 

| from flask import Flask, jsonify, request. |
| :---- |

Nell'applicazione Flask è il “motore” che gestisce tutta la comunicazione tra l’API e i dati.

## ORIGINI

Flask è un micro framework web per Python creato da **Armin Ronacher** nel 2010\. È nato per offrire uno strumento semplice, leggero e flessibile per creare applicazioni web e API.

La cosa interessante di Flask è che è anche molto potente. Si può creare un server che risponde a richieste HTTP come GET o POST.

Flask si occupa di ricevere le richieste, leggere i dati che arrivano, elaborarli e restituire una risposta, spesso in formato JSON, che è il formato più usato per scambiare dati tra sistemi.

## 

## ALTERNATIVE

Esistono anche altre soluzioni. C’è Django, che è sempre scritto in Python ma è più grande, già pronto per creare applicazioni complete e strutturate. Oppure c’è FastAPI, che è più moderno e adatto per API molto performanti.

# PYTHON {#python}

Il linguaggio usato nell'applicazione è python.  
Python è un linguaggio di programmazione **semplice, leggibile e potente**, nato nel 1991 grazie a **Guido van Rossum**. È molto usato perché ha una **sintassi chiara**, cioè il codice si legge quasi come l’inglese, e permette di fare tante cose con poche righe.

È molto usato sia dai principianti che da aziende come Google, Instagram o Netflix, proprio perché unisce **facilità e potenza**. In poche parole, Python è un linguaggio che ti permette di imparare in fretta e creare progetti utili anche nel mondo reale.

# JSON

Json è il formato in cui sono scritti i dati nel database dell’app.

JSON è un formato di dati molto usato per scambiare informazioni tra un server e un’app o un sito web. È come un **linguaggio universale** che tutti i sistemi possono leggere facilmente.

Ogni **dato** in JSON è rappresentato da una **chiave** (come “name” o “id”) e un **valore** (come “Alice” o “1”), ed è strutturato in oggetti o array.

| esempio di json {  "name": "Alice",  "age": 25,  "city": "Rome"} |
| :---- |

[image1]: <data:image/png;base64,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>