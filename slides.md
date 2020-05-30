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
- __*Scalano automaticamente[^1]*__

must be deployed in North Virigina (us-east-1)

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

^ AWS ha detto che stanno lavorando per ridurre il tempo.

---

# L@E Challenge #2

## **Concurrent Limit**
1000 concurrent executions per account per region (5000 hard limit)

Warm Up time
<br/><br/><br/><br/><br/><br/><br/><br/><br/>

![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)

---

# L@E Challenge #3

## **Metrics**
Le metriche delle lambda sono sparse in tutte le region, ma fruibili tutte insieme nella console di CloudFront.

20 June 2019
https://aws.amazon.com/about-aws/whats-new/2019/06/announcing-enhanced-lambda-edge-monitoring-amazon-cloudfront-console/



---

# L@E Challenge #4

## **Logs**
Lambda@Edge genera CloudWatch logs in 11 AWS Regions (dove CloudFront ha un Regional Edge Cache) <br/><br/>



![inline 55%](./images/logs.png)

[.footer: https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/]

---

# L@E Tips & Tricks

1. Optimize network latency
	- enable TCP Keep Alive and reuse connections
	- make network calls to resources in the same region here your Lambda@Edge function is executing
 	- using DynamoDB global tables

2. Use infrastructure as code for Deployment & Logs Aggregation


---


## **Contesto**

## **Migrazione**

## **Lambda @ Edge**

## [fit] Analisi Soluzione

<br />

### @**_maxgallo**

---

# Costi

<br/>

![inline 55%](./images/costs.png)

---

# Lambda @ Edge in DAZN

[.list: #000000, bullet-character(->), alignment(left)]
[.build-lists: true]

- __*Scalabilità*__ ✅
- __*Velocità*__ ✅
- __*Stessa URL*__ ✅
- __*Indipendente dal Frontend*__ ✅
- __*Canary Deployment*__ ❌✅

---

# Canary Deployment

- Change of configuration
- Runtime configuration
- Sticky Session + Cookie

---

# TakeAways

---

#[fit] Thank you


# [fit] **github.com/maxgallo/talk-micro-frontends-on-the-edge**

<br />
<br />
<br />

### @**_maxgallo**
