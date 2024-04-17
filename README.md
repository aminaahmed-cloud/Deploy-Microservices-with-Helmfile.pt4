# Deploy-Microservices-with-Helmfile


**Create install.sh file**

Create a shell script `install.sh` that contains all the helm install commands.

```sh
#!/bin/bash

helm install -f values/redis-values.yaml rediscart charts/redis

helm install -f values/email-service-values.yaml emailservice charts/microservice
helm install -f values/cart-service-values.yaml cartservice charts/microservice
helm install -f values/currency-service-values.yaml currencyservice charts/microservice
helm install -f values/payment-service-values.yaml paymentservice charts/microservice
helm install -f values/recommendation-service-values.yaml recommendationservice charts/microservice
helm install -f values/productcatalog-service-values.yaml productcatalogservice charts/microservice
helm install -f values/shipping-service-values.yaml shippingservice charts/microservice
helm install -f values/ad-service-values.yaml adservice charts/microservice
helm install -f values/checkout-service-values.yaml checkoutservice charts/microservice
helm install -f values/frontend-values.yaml frontendservice charts/microservice
```

```
chmod u+x install.sh
./install.sh
```

---

**Create uninstall.sh**

```
#!/bin/bash

helm uninstall rediscart 

helm uninstall emailservice 
helm uninstall cartservice 
helm uninstall currencyservice
helm uninstall paymentservice
helm uninstall recommendationservice
helm uninstall productcatalogservice
helm uninstall shippingservice
helm uninstall adservice
helm uninstall checkoutservice
helm uninstall frontendservice
```

---

### - This option is not practical that is why we will create helmfile

### What is Helmfile?

- Declarative way for deploying Helm charts

- Declare a definition of an entire Kubernetes cluster

- Change specification depending on application or type of environment

---

**Create a Helmfile**

Create a Helmfile.yaml to define the releases.

```yaml
releases: 
  - name: rediscart
    chart: charts/redis
    values: 
      - values/redis-values.yaml
      - appReplicas: "1"
      - volumeName: "redis-cart-data"

  - name: emailservice
    chart: charts/microservice
    values:
      - values/email-service-values.yaml

  - name: cartservice
    chart: charts/microservice
    values:
      - values/cart-service-values.yaml

  - name: currencyservice
    chart: charts/microservice
    values:
      - values/currency-service-values.yaml   

  - name: paymentservice
    chart: charts/microservice
    values:
      - values/payment-service-values.yaml

  - name: recommendationservice
    chart: charts/microservice
    values:
      - values/recommendation-service-values.yaml

  - name: productcatalogservice
    chart: charts/microservice
    values:
      - values/productcatalog-service-values.yaml

  - name: shippingservice
    chart: charts/microservice
    values:
      - values/shipping-service-values.yaml

  - name: adservice
    chart: charts/microservice
    values:
      - values/ad-service-values.yaml

  - name: checkoutservice
    chart: charts/microservice
    values:
      - values/checkout-service-values.yaml

  - name: frontendservice
    chart: charts/microservice
    values:
      - values/frontend-values.yaml
```

---

**Install Helmfile**

```
brew install helmfile
```

---

<img src="https://i.imgur.com/fHa11BA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

---

**Deploy Helmchart**

```
helmfile sync
```

---

**To uninstall all releases with one command:**

```
helmfile destroy
```

---

<img src="https://i.imgur.com/pGYydrb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

---
