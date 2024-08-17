# Demo API Helm Charts

## Install Charts & Upgrade Chart

When installing chart user command:

- `helm install demoapi ./helm/`

When updating installed chart use command:

- `helm upgrade demoapi ./helm/`

The purpose of that API was to practice Helm Charts. 
Communication between Pods seems to work fine. 
`demoapi-api1` can send requests to `demoapi-api2` via REST API calls.
SpringBoot API uses Rest Template to call endpoint `/api/person/items/{personId}`

## What is going on ?

The `UI` (PHP) makes curl call to `API1` to get `Person` and its `Items`. 

## Person API & Item API

Basically both use the same app that sits in that repo `https://github.com/smicho01/springboot-demo-api` 

Docker compose in that repo spins up 2 container for api:
- demoapi
- demoapi-items

The same app but on different ports. `PeronService.java` in the method `getPersonItems` makes Rest Template request to other instance of the API to get Person Items.  It could happen within the same service, but it was created like that for the purpose of having 2 K8S pods that iteracts with each other, but I was way too lazy to build totally different API , make repo for it, Docker Hub repo etc. 