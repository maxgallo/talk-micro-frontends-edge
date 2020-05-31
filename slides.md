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

# Ciao, sono Max
anche se forse stavolta posso  dire Massimiliano

# 🇮🇹 -> 🇬🇧

Priincipal Engineer @ DAZN

### @**_maxgallo**

![right filtered fit](./images/profile.JPEG)

---

# Agenda

## **Contesto**

## **Migrazione**

## **Lambda @ Edge**

## **Solution Analysis**

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

## **Contesto**

#[fit] Migrazione

## **Lambda @ Edge**
## **Analisi Soluzione**

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
[.build-lists: true]

- __*Scalabilità*__
- __*Velocità*__
- __*Stessa URL*__
- __*Indipendente dal Frontend*__
- __*Canary Deployment*__

![Right 50%](./images/1_or_2_question_vertical.png)

---

## **Contesto**

## **Migrazione**

## [fit] Lambda @ Edge

## **Analisi Soluzione**

<br />

### @**_maxgallo**

---

# Lambda@Edge

[.list: #000000, bullet-character(->), alignment(left)]

[.build-lists: true]

- __*Simili a AWS Lambda*__
- __*Runnano sulla CDN, CloudFront*__
- __*Paghi solo quando le usi*__
- __*Scalano automaticamente*__

must be deployed in North Virigina (us-east-1)

![right 60%](./images/lambda.png)

---

![original 50%](./images/lambda_at_edge_world.png)

[.footer: 205 Edge Locations and 11 Regional Edge Caches]

---

# Lambda@Edge

![inline 55%](./images/lambda_at_edge.png)

^ La riga tratteggiata è dove CloudFront cacha gli oggetti

---


# L@E Challenge #1

## **Concurrent Limit**

Limite di 1000 concurrent executions per ogni account, per region.


Esempio: *500 RPS* * *14ms* execution time = *7* concurrent Lambda @ Edge

<br/><br/><br/><br/>

![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)

[.footer: È possibile richiedere un aumento fino a 5000.]

---

# L@E Challenge #2

## **Development**

Il deploy delle Lambda@Edge nelle Edge Location può durare fino a 10 minuti. 

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

![inline 55%](./images/deployment.png)

^ AWS ha detto che stanno lavorando per ridurre il tempo.

---

# L@E Challenge #3

## **Metrics**
Le metriche delle lambda sono sparse in 11 AWS Regions.

Dal 20 giugno 2019 sono state parzialmente aggregate nella console di CloudFront.


^ 11 AWS Region sono dove CloudFront ha un Regional Edge Cache

[.footer: https://aws.amazon.com/about-aws/whats-new/2019/06/announcing-enhanced-lambda-edge-monitoring-amazon-cloudfront-console/]

---

# L@E Challenge #4

## **Logs**
Lambda@Edge genera CloudWatch logs in 11 AWS Regions. <br/><br/>


![inline 55%](./images/logs.png)

^ 11 AWS Region sono dove CloudFront ha un Regional Edge Cache

[.footer: https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/]


---


## **Contesto**

## **Migrazione**

## **Lambda @ Edge**

## [fit] Analisi Soluzione

<br />

### @**_maxgallo**

---

# Costi

In DAZN in media ogni Lambda @ Edge impiega x ms per runnare


![inline 55%](./images/costs.png)

---

# Lambda @ Edge in DAZN

[.list: #000000, bullet-character(->), alignment(left)]
[.build-lists: true]

- __*Scalabilità*__
- __*Velocità*__
- __*Stessa URL*__
- __*Indipendente dal Frontend*__ 
- __*Canary Deployment*__ ???

---

# Canary Deployment
### **Indirizzare una percentuale di utenti su DAZN 1.0 o DAZN 2.0**

Nella Lambda @ Edge possiamo mantenere tutta la logica, ma dove teniamo i parametri su cui si basa ?

**Opzione 1:** Nella lambda stessa -> 10 minuti per deployer

**Opzione 2** Configurazione esterna -> Add latency

---

# Runtime Configuration

- Sticky Session + Cookie

[.footer: https://aws.amazon.com/blogs/networking-and-content-delivery/leveraging-external-data-in-lambdaedge/ ]


---

# TakeAways

---

#[fit] Thank you


# [fit] **github.com/maxgallo/talk-micro-frontends-on-the-edge**

<br />
<br />
<br />

### @**_maxgallo**
