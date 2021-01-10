# Local Setup

To setup the billing-service in your local system, clone the git repo(https://github.com/egovernments/business-services).

## Dependencies


### Infra Dependency

- [X] Postgres DB
- [ ] Redis
- [ ] Elasticsearch
- [X] Kafka
  - [X] Consumer
  - [ ] Producer

## Running Locally

To run the service locally, you need to port forward below services.

```bash
function kgpt(){kubectl get pods -n egov --selector=app=$1 --no-headers=true | head -n1 | awk '{print $1}'}

kubectl port-forward -n egov $(kgpt user) 8085:8080
kubectl port-forward -n egov $(kgpt idgen) 8086:8080
kubectl port-forward -n egov $(kgpt mdms) 8087:8080
kubectl port-forward -n egov $(kgpt egov-apportion-service) 8088:8080
kubectl port-forward -n egov $(kgpt localization) 8089:8080
``` 

Update below listed properties in `application.properties` before running the project:

```ini
user.service.hostname = http://127.0.0.1:8085
egov.idgen.hostname = http://127.0.0.1:8086

# can use non port forwarded environment host as well
egov.mdms.host = http://127.0.0.1:8087
egov.apportion.host = http://127.0.0.1:8088

# can use non port forwarded environment host as well
egov.localization.host = http://127.0.0.1:8089
```