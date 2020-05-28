# [fit] Micro-frontends on the edge
### [fit] **una storia di persone, migrazioni e serverless**

<br />
<br />
![inline 80%](./images/arrow.png)
<br />

### @**_maxgallo**

---

# [fit] Micro-frontends on the edge
### [fit] **una storia di persone, migrazioni e serverless**

<br />
<br />
<br />
<br />
<br />

### @**_maxgallo**

---

Slide about me

---

# Agenda

[.column]

### 1. Contesto

1. DAZN Constraints
2. Soluzione

### 2. Migrazione

1. Due Frontend
2. Lambda @ Edge
3. Runtime Configuration

4. Canary & BlueGreen Deployment

[.column]

### 3. Challenges

1. Developing
2. Logging Aggregation
3. Metrics / Notifications

→ → 💡Takeaways


---

#[fit] Contesto

<br />
<br />
<br />
<br />
<br />
<br />

### @**_maxgallo**


---

# Spike di utenti

![original 70%](./images/users_spike.png)

---

# Spike di utenti
# **-> Scalabilità**

![original 70%](./images/users_spike.png)

---

# Team in Espansione

![original 65%](./images/dazn_expansion.png)

---

# Team in Espansione
# **-> Indipendenza**

![original 65%](./images/dazn_expansion.png)

---

# Eventi Live

![original 70%](./images/goal.png)

---


# Eventi Live
# **-> Velocità**

![original 70%](./images/goal.png)

---

# Santa Trinità di **AWS**

![original 50%](./images/route53_cloudfront_s3.png)


^ Scalabilità ✓
^ Indipendenza ✓
^ Velocità ✓

---

#[fit] Migrazione

<br />
<br />
<br />
<br />
<br />
<br />

### @**_maxgallo**

--- 

# Due Frontend
## **Due Aziende**

![inline 60%](./images/dazn_1_vs_2.png)

---

![original 70% ](./images/monolith_vs_microfrontends.png)

^ Stesse funzionalità

---

# Manca qualcosa !

![original 60% ](./images/1_or_2_question.png)

---

# Caratteristiche

[.list: #000000, bullet-character(->), alignment(left)]

- __*Scalabilità*__
- __*Stessa URL*__
- __*Indipendente dal Frontend*__
- __*Canary Deployment per Nazione & Browser + Sticky Session*__

![Right 50%](./images/1_or_2_question_vertical.png)

---

# Lambda@Edge

[.list: #000000, bullet-character(->), alignment(left)]

[.build-lists: true]

- __*Simili a AWS Lambda*__
- __*Runnano sulla CDN, CloudFront*__
- __*Paghi solo quando le usi*__
- __*Scalano automaticamente[^1]*__

![right 60%](./images/lambda.png)

[^1]: Torneremo su questo a breve.

---

![original 50%](./images/lambda_at_edge_world.png)

[.footer: 205 Edge Locations and 11 Regional Edge Caches]

---

# Lambda@Edge

![inline 55%](./images/lambda_at_edge.png)

^ La riga tratteggiata è dove CloudFront cacha gli oggetti

---


# L@E Challenge #1

## **Development**
Il deploy delle Lambda@Edge nelle varie Edge Location può durare fino a 15/20 minuti. 

---

# L@E Challenge #2

## **Concurrent Limit**
1000 concurrent limit by default per region (5000 hard limit)
<br/><br/><br/><br/><br/><br/><br/><br/><br/>

![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)

---

# L@E Challenge #3

## **Logs & Metrics Aggregation**
I log e le metriche delle lambda sono sparsi in tutte le region

<br /><br />

![inline 55%](./images/logs.png)

---

## Warm Up time
Bla bla

^ Da AWS ci hanno detto che stanno lavorando per fare durare meno il deploy.

---

#[fit] ☂︎☂︎*☂︎*☂︎☂︎☂︎
# ✂︎ ⌘ ☔︎ ✈︎ ⚉ ⚇ ☞ ⎈ *✂︎*