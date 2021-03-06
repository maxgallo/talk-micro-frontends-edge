# [fit] Micro-frontends on the edge
### [fit] **una storia di persone, migrazioni e serverless**

<br />
<br />
<br />
<br />
<br />

### @**_maxgallo**

---

# [fit] Ciao, sono Max

### 🇮🇹 🇬🇧 🍝 💻 🎶 🏍 📷 ✈️ ✍️

### **Principal Engineer @ DAZN**

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### twitter: @**_maxgallo**
### web: **maxgallo.io**

![right 30%](./images/me.png)

---

[.column]
<br /><br /><br /><br /><br /><br /><br />
#[fit] Agenda

[.column]

<br /><br />

## **Contesto**

## **Migrazione**

## **Lambda @ Edge**

## **Analisi Soluzione**

---
<!--
### 1. Contesto


1. DAZN Constraints
2. Soluzione

### 2. Migrazione

1. Due Frontend
2. Routing Missing Part

### 3. Lambda @ Edge
- Overview
- Challenges
	- Development
	- Concurrent Limit
	- Logs & Metrics Aggregation
		- Lambda logs & cloudfront logs
- Tips

### 4. Solution Analysis
- Costs
- Check Needs VS Caracteristic
- Canary Deployment
- Runtime configuration
	-  make network calls to resources in the same region where your Lambda@Edge function is executing to reduce network latency.

### 5. TakeAways

---
-->

#[fit] Contesto
## **Migrazione**
## **Lambda @ Edge**
## **Analisi Soluzione**

<br />
<br />

### @**_maxgallo**


---

# Spike di utenti

![original 40%](./images/users_spike.png)

^ Costi
^ Warm up difficile

---

# Spike di utenti
# **-> Scalabilità**

![original 40%](./images/users_spike.png)

---

# Team in Espansione

![original 65%](./images/dazn_expansion.png)

^ Esempio AWS account
^ Prima: Non sapevamo di chi fosse carta di credito dell'account
^ Dopo: 4 account per ogni team (uno per env) e accesso gestito tramite cli

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

[.column]

<br /><br /><br /><br />

# **Spike di utenti**
# **Team in Espansione**
# **Eventi Live**

[.column]

<br /><br /><br /><br /><br /><br /><br /><br />
# [fit] Contesto





---

# Santa Trinità di **AWS**

![original 50%](./images/route53_cloudfront_s3.png)

^ File Statici
^ Scalabilità ✓
^ Indipendenza ✓
^ Velocità ✓

---

## **Contesto**

#[fit] Migrazione

## **Lambda @ Edge**
## **Analisi Soluzione**

<br />

### @**_maxgallo**

---

# Due Frontend, **Due Aziende**

![inline 60%](./images/dazn_1_vs_2.png)

---

![original 60% ](./images/monolith_vs_microfrontends.png)

^ Stesse funzionalità

---

# Micro-frontends

![inline](./images/micro_frontends.png)

[.footer: Micro-frontends resources: [https://medium.com/@lucamezzalira/micro-frontends-resources-53b1ec7d512a](https://medium.com/@lucamezzalira/micro-frontends-resources-53b1ec7d512a)]

---

# Quale Frontend ?

![original 45% ](./images/1_or_2_question.png)

---

# Caratteristiche

[.list: #000000, bullet-character(->), alignment(left)]
[.build-lists: true]

- __*Scalabile*__
- __*Veloce*__
- __*Indipendente dal Frontend*__
- __*Stessa URL*__
- __*Canary Deployment*__

![original 40% ](./images/1_or_2_question_long.png)

---

## **Contesto**

## **Migrazione**

## [fit] Lambda @ Edge

## **Analisi Soluzione**

<br />

### @**_maxgallo**

---

# Lambda @ Edge

[.list: #000000, bullet-character(->), alignment(left)]

[.build-lists: true]
Come le AWS Lambda normali

<br />

- __*Nessuna infrastruttura da gestire*__
- __*Scalano automaticamente*__
- __*Paghi solo quando le usi*__


![right 60%](./images/lambda.png)

---
<br/>
<br/>
<br/>
<br/>

## Lambda @ Edge
### runnano su CloudFront

![original  50%](./images/lambda_at_edge_world.png)

[.footer: 205 Edge Locations and 11 Regional Edge Caches]

---

# Lambda @ Edge

![inline 50%](./images/lambda_at_edge.png)

^ CloudFront events come input & output
^ La riga tratteggiata è dove CloudFront cacha gli oggetti

---

# Lambda @ Edge
### **CloudFront Events** <br/><br/><br/><br/><br/>

![inline 45%](./images/lambda_at_edge_events.png)


[.footer: Full Specifications: [https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-event-structure.html](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-event-structure.html) ]

---


# L@E Challenge #1

## **Concurrent Limit**

Limite di 1000 concurrent executions per ogni account, per region.

<br/><br/>

Esempio: *5000 RPS* * *6ms* execution time = *30* concurrent Lambda @ Edge

![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)

[.footer: È possibile estendere il limite fino a 5000 per account per region. Limiti delle Lambda @ Edge [https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html#limits-lambda-at-edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html#limits-lambda-at-edge)]

---

# L@E Challenge #2

## **Development**

Il deploy delle Lambda@Edge nelle Edge Location può durare fino a 10 minuti.

<br/><br/><br/><br/><br/><br/><br/>

![inline 55%](./images/deployment.png)

<br/><br/><br/><br/><br/>

^ AWS ha detto che stanno lavorando per ridurre il tempo.

---

# L@E Challenge #3

## **Metrics & Alarms**
Disponibili nella regione dove la Lambda @ Edge ha runnato (11 AWS Regions).

Parzialmente aggregate nella console di CloudFront.

![inline 30%](./images/users_spike.png)

^ 11 AWS Region sono dove CloudFront ha un Regional Edge Cache

[.footer: Edge monitoring su Cloudfront: [https://aws.amazon.com/about-aws/whats-new/2019/06/announcing-enhanced-lambda-edge-monitoring-amazon-cloudfront-console/](https://aws.amazon.com/about-aws/whats-new/2019/06/announcing-enhanced-lambda-edge-monitoring-amazon-cloudfront-console/)]

---

# L@E Challenge #4

## **Lambda Logs**

CloudWatch logs nella regione più vicina alla richiesta (11 AWS Regions). <br/><br/><br/><br/>

![inline 45%](./images/logs.png)

^ 11 AWS Region sono dove CloudFront ha un Regional Edge Cache

[.footer: Logs Aggregation [https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/](https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/)]


---

# L@E Challenge #5

## **Lambda Validation Logs**

CloudWatch logs sulla validazione degli output delle Lambda @ Edge.

Disponibili al log group:  __*/aws/cloudfront/LambdaEdge/DistributionId*__


![inline 30%](./images/lambda_at_edge_events.png)

[.footer: Test & Debug Lambda @ Edge: [https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-testing-debugging.html](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-testing-debugging.html) ]
---

## **Contesto**

## **Migrazione**

## **Lambda @ Edge**

## [fit] Analisi Soluzione

<br />

### @**_maxgallo**

---

# Costi

Con circa __*2ms*__ di tempo di esecuzione

![inline 55%](./images/costs.png)

[.footer: Si paga per __*Numero di Richieste*__ e __*GB al secondo*__ di memoria usata (con granularità a 50ms) [https://aws.amazon.com/lambda/pricing/#Lambda.40Edge_Pricing](https://aws.amazon.com/lambda/pricing/#Lambda.40Edge_Pricing)]

---

# Lambda @ Edge in DAZN

[.list: #000000, bullet-character(->), alignment(left)]
[.build-lists: true]

- *Scalabile*
- *Veloce*
- *Indipendente dal Frontend*
- *Stessa URL*
- **Canary Deployment**

![original 42%](./images/1_or_2_question_final.png)

---

# Canary Deployment
### **Due modi di gestire la configurazione**

![inline 50%](./images/canary_two_ways.png)

---

# Canary Deployment
### **External Configuration**

![original 40%](./images/canary_external.png)

[.footer: External data in Lambda@Edge: [https://aws.amazon.com/blogs/networking-and-content-delivery/leveraging-external-data-in-lambdaedge/](https://aws.amazon.com/blogs/networking-and-content-delivery/leveraging-external-data-in-lambdaedge/) ]

---

# Canary Deployment
### **Sticky Session**
### **+ Cookies**

![original 40%](./images/lambda_at_edge_sticky.png)

---

# TakeAways

[.list: #000000, bullet-character(->), alignment(left)]
[.build-lists: true]

- Contesto Contesto Contesto

- Lavorare sulle CDN è possibile

- Non solo AWS (Cloudflare Workers)

- Routing e Canary Release solo l'inizio (SSR[^1], SEO [^2], Security Headers...)



[^1]: Server Side Rendering

[^2]: Search Engine Optimisation

^ Non lavoriamo più in un contesto di Client-Server, ma di Client, Server & CDN.

---

#[fit] Thank You


# [fit] **github.com/maxgallo/talk-micro-frontends-edge**

<br />
<br />
<br />

### @**_maxgallo**
