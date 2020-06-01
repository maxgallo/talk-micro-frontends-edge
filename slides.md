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


### **🇮🇹 -> 🇬🇧**

Principal Engineer @ DAZN

<br /><br />

### twitter: @**_maxgallo**
### web: **maxgallo.io**

![right filtered fit](./images/profile.JPEG)

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
- __*Stessa URL*__
- __*Indipendente dal Frontend*__
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
Come le AWS Lambda normali:

- __*Scalano automaticamente*__
- __*Paghi solo quando le usi*__
- __*Puoi configurare la memoria*__

<br/>

E in particolare hanno

- __*Devono essere deployate in us-east-1*__
- __*Hanno dei limiti leggermente diversi*__
- ...

![right 60%](./images/lambda.png)

[.footer: [https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html#limits-lambda-at-edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html#limits-lambda-at-edge)]

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

![inline 55%](./images/lambda_at_edge.png)

^ La riga tratteggiata è dove CloudFront cacha gli oggetti

---


# L@E Challenge #1

## **Concurrent Limit**

Limite di 1000 concurrent executions per ogni account, per region.


Esempio: *5000 RPS* * *6ms* execution time = *30* concurrent Lambda @ Edge

<br/><br/><br/><br/>

![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)![inline](./images/lambda.png)

[.footer: È possibile estendere il limite fino a 5000 per account per region.]

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

## **Metrics**
Disponibili nella regione dove la Lambda @ Edge ha runnato (11 AWS Regions).

Parzialmente aggregate nella console di CloudFront.

![inline 30%](./images/users_spike.png)

^ 11 AWS Region sono dove CloudFront ha un Regional Edge Cache

[.footer: https://aws.amazon.com/about-aws/whats-new/2019/06/announcing-enhanced-lambda-edge-monitoring-amazon-cloudfront-console/]

---

# L@E Challenge #4

## **Lambda Logs**

CloudWatch logs nella regione più vicina alla richiesta (11 AWS Regions). <br/><br/><br/><br/>

![inline 45%](./images/logs.png)

^ 11 AWS Region sono dove CloudFront ha un Regional Edge Cache

[.footer: [https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/](https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/)]


---

# L@E Challenge #5

## **Lambda Validation Logs**

CloudWatch logs sulla validazione degli output delle Lambda @ Edge.

Disponibili al log group:  __*/aws/cloudfront/LambdaEdge/DistributionId*__


![inline 35%](./images/lambda_at_edge.png)

[.footer: [https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-testing-debugging.html](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-edge-testing-debugging.html) ]
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

---

# Lambda @ Edge in DAZN

[.list: #000000, bullet-character(->), alignment(left)]
[.build-lists: true]

- *Scalabile*
- *Veloce*
- *Stessa URL*
- *Indipendente dal Frontend*
- **Canary Deployment**

![original 42%](./images/1_or_2_question_final.png)

---

# Canary Deployment

Logica per Canary release con geo-routing nella lambda.
Dove teniamo la configurazine ?



![inline 42%](./images/canary.png)

---

# External Configuration

- Sticky Session + Cookie

[.footer: https://aws.amazon.com/blogs/networking-and-content-delivery/leveraging-external-data-in-lambdaedge/ ]


---

# TakeAways

Lavorare on the edge è possibile (non solo AWS)

---

#[fit] Thank You


# [fit] **github.com/maxgallo/talk-micro-frontends-on-the-edge**

<br />
<br />
<br />

### @**_maxgallo**
