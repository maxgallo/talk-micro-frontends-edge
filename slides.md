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

### Architettura

1. Contesto
2. Soluzione

### Migrazione

1. Due Frontend
2. Lambda @ Edge
3. Runtime Configuration

4. Canary & BlueGreen Deployment

[.column]

### Challenges

1. Developing
2. Logging Aggregation
3. Metrics / Notifications

→ → 💡Takeaways


---

#[fit] *✂︎* Contesto

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

#[fit] *✂︎* Migrazione

--- 

# Due Frontend, due aziende

![inline 60%](./images/dazn_1_vs_2.png)

---

![original 70% ](./images/monolith_vs_microfrontends.png)

^ Stesse funzionalità

---

# Manca un pezzo !

![original 60% ](./images/1_or_2_question.png)

---

# Caratteristiche

## **-> Scalabilità**
## **-> Stessa URL**
## **-> Indipendente dal Frontend**
## **-> Canary Deployment per Nazione & Browser + Sticky Session**



![Right 50%](./images/1_or_2_question_vertical.png)

---

---

Issues

1000 concurrent limit by default per region (5000 hard limit)




---

#[fit] ☂︎☂︎*☂︎*☂︎☂︎☂︎
# ✂︎ ⌘ ☔︎ ✈︎ ⚉ ⚇ ☞ ⎈ 