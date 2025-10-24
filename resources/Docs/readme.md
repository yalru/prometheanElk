elastic-agent-7.17.23-amd64.deb

dpkg -i elastic-agent-7.17.23-amd64.deb




A service token grants Fleet Server permissions to write to Elasticsearch.
Save your service token information. This will be shown only once.
**Service token**
AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzEzOTIxODM6VWZZT2VmdVJSWEdtdHpzQmduN1o2dw


sudo elastic-agent enroll --url=http://127.0.0.1:8220 \\   --fleet-server-es=http://localhost:9200 \\   --fleet-server-service-token=AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzEzOTIxODM6VWZZT2VmdVJSWEdtdHpzQmduN1o2dw \\   --fleet-server-policy=499b5aa7-d214-5b5d-838b-3cd76469844e \\   --certificate-authorities=<PATH\_TO\_CA> \\   --fleet-server-es-ca=<PATH\_TO\_ES\_CERT> \\   --fleet-server-cert=<PATH\_TO\_FLEET\_SERVER\_CERT> \\   --fleet-server-cert-key=<PATH\_TO\_FLEET\_SERVER\_CERT\_KEY>


`/usr/share/elastic-agent/*`Elastic Agent program files

`/etc/elastic-agent/elastic-agent.yml`Main Elastic Agent configuration

`/etc/elastic-agent/fleet.enc`Main Elastic Agent Fleet encrypted configuration

`/var/lib/elastic-agent/data/elastic-agent-*/logs/elastic-agent.ndjson`Log files for Elastic Agent and Beats shippers[^1^](https://www.elastic.co/docs/solutions/observability/apm/apm-server/installation-layout#footnote-1)

`/usr/bin/elastic-agent`Shell wrapper installed into PATH


sudo elastic-agent enroll   \\   --fleet-server-es=http://localhost:9200 \\   --fleet-server-service-token=AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzE3NjUyMTc6cFQzYnNEWWpTYW1SbVEtVHFFZ25WUQ \\   --fleet-server-policy=499b5aa7-d214-5b5d-838b-3cd76469844e \\   --fleet-server-insecure-http



apt-get update && apt-get install sudo nano

http://127.0.0.1:8220

AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzE4NDI3MjI6RFZqZUdORlRURnFoRmxDZmI5TTN4UQ


sudo elastic-agent enroll   \\   --fleet-server-es=http://localhost:8220 \\   --fleet-server-service-token=AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzE4NDI3MjI6RFZqZUdORlRURnFoRmxDZmI5TTN4UQ \\   --fleet-server-policy=499b5aa7-d214-5b5d-838b-3cd76469844e \\   --fleet-server-insecure-http


AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzIzODQ1NzY6M0FiaUZVYmVUQnVEamh4cDNpalJZUQ

```
sudo ./elastic-agent install   \
  --fleet-server-es=https://localhost:9200 \
  --fleet-server-service-token=AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzIzODQ1NzY6M0FiaUZVYmVUQnVEamh4cDNpalJZUQ \
  --fleet-server-policy=499b5aa7-d214-5b5d-838b-3cd76469844e \
  --fleet-server-insecure-http
```


sudo elastic-agent enroll   \\   --fleet-server-es=https://localhost:8220 \\   --fleet-server-service-token=AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuLTE3NjEyMzE4NDI3MjI6RFZqZUdORlRURnFoRmxDZmI5TTN4UQ \\   --fleet-server-policy=499b5aa7-d214-5b5d-838b-3cd76469844e \\   --fleet-server-insecure-http



