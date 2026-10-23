# secure-traffic-analyzer-elk — network security log analysis with the ELK stack

A DevOps project (M2 Expert DevOps, ENSITECH): network security logs are generated, ingested by Logstash, indexed in Elasticsearch and explored in Kibana, with the stack deployed through CI/CD pipelines.

## What it does

- **Data:** a Python generator produces realistic security logs (ports, protocol, ALLOW / BLOCK / DROP action, bytes, threat level, geolocation); a second script streams traffic events over TCP to simulate live data
- **Ingestion:** Logstash parses the CSV, converts types, builds a `geo_point` and writes daily `iot-security-*` indices
- **Visualisation:** Kibana on top of the indices (time-based fields and geo_point ready for threat maps)
- **Delivery:** Jenkins pipeline and GitHub Actions workflow validate, build and deploy the Docker Compose stack
- **Access:** Nginx reverse-proxy configuration with TLS and basic authentication for Kibana

![Architecture](docs/schema_architecture.drawio.png)

Data-flow, sequence, Jenkins and use-case diagrams are in [`docs/`](docs).

## Stack

Elasticsearch · Logstash · Kibana 7.17 · Docker Compose · Jenkins · GitHub Actions · Nginx · Python

## Run it

```bash
cd data && python generate_network_security_logs.py   # creates network_security_logs.csv
cd ../elk && docker-compose up -d                      # update the CSV volume path in docker-compose.yml first
# Kibana: http://localhost:5601
```
