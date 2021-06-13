# Esselunga<br/>
## Tech Challenge
#### Riccardo Corbella
##### 06/13/2021
---
## (Some) Goals...
--
### Data analytics
- analyze stores sales
- understand customers behaviours
--
### Real-time insights
- compute total stores sales
- find the 10 most profitables stores
- count the number of distinct customers
- identify weekly stores sales trends
---
## High level<br/> architecture
![Architecture](/images/esselunga_tech_architettura.svg)
---
### Data analytics layer
![Analitycs layer](/images/architettura_anal.svg)
--
- _Kafka connect_ loads data on __low cost__ GCS (object storage) using different paritioning strategy
  - data is stored in JSON files with schema
  - as data age its moved in "colder areas" to reduce costs
- _Big Query_ (data wharehouse) reads directly from GCS offering __top notch performances__
  - data is modeled using a star schema, effective for many types of analysis and widely used by BI analysts
---
### Real-time insights layer
![Real-time layer](/images/architettura_real.svg)
--
- _telegraf_ writes sales data on _influxDB_, capable of handling __high write loads__ and keeping KPIs up to date
- KPIs are exposed on custom dashboard built on top of _Grafana_
---
## Next steps
![Extra layer](/images/architettura_extra.svg)
--
- KPIs are exposed trough RESTful APIs to other IT entities (e.g. mobile app, web sites, ...)
- _K8S_ (GKE or Cloud Run as fully managed services) provides the perferct environment to build __etherogeneous microservices__ and due to its __high versatility__ can be used to fullfill new requirements