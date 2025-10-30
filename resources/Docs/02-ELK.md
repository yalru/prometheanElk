# Stack ELK


## Kibana 
UI used to load elastic agents and setup fleet server 


## Fleet server
install a fleetserver 
-> elastic agent used as a fleet server     
![fleet-server-agent-policies-diagram.png](picts/fleet-server-agent-policies-diagram.png)



https://www.elastic.co/docs/reference/kibana/configuration-reference/fleet-settings#fleet-data-visualizer-settings




https://www.elastic.co/docs/deploy-manage/users-roles/cluster-or-deployment-auth/service-accounts
Service accounts usage
    elastic/fleet-server
    The service account used by the Fleet server to communicate with Elasticsearch.
    elastic/kibana
    The service account used by Kibana to communicate with Elasticsearch.
Service account tokens
    https://www.elastic.co/docs/api/doc/elasticsearch/operation/operation-security-create-service-token

POST
/_security/service/{namespace}/{service}/credential/token/{name}



create a service token : 
FLEET_SERVER_SERVICE_TOKEN

use the kibana console to run a request directly : 
http://localhost:5601/app/dev_tools#/console/shell
POST
/_security/service/elastic/fleet-server/credential/token/tokenfleet

{
"created": true,
"token": {
    "name": "tokenfleet",
    "value": "AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuZmxlZXQ6TnBvUXoySE1URnkwbEppZk4wZG5VZw"
    }
}

use the created token for the  FLEET_SERVER_SERVICE_TOKEN in the docker-compose.yaml
FLEET_SERVER_SERVICE_TOKEN=AAEAAWVsYXN0aWMvZmxlZXQtc2VydmVyL3Rva2VuZmxlZXQ6TnBvUXoySE1URnkwbEppZk4wZG5VZw



create fleet policy - fleet-server-policy
FLEET_SERVER_POLICY_ID=fleet-server-policy
https://www.elastic.co/docs/reference/fleet/create-policy-no-ui



create a flet policy 

curl -u elastic:elastic --request POST \
--url http://localhost:5601/api/fleet/agent_policies?sys_monitoring=true \
--header 'content-type: application/json' \
--header 'kbn-xsrf: true' \
--data '{"name":"AgentPolicy1","namespace":"default","monitoring_enabled":["logs","metrics"]}'

AgentPolicy1 created,  

Add integration to policy 
[2025-10-29T09:44:00.889+00:00][ERROR][plugins.fleet] Error connecting to package registry: 
request to https://epr.elastic.co/categories?kibana.version=9.2.0&spec.min=2.3&spec.max=3.5 
failed, reason: self-signed certificate in certificate chain
-> and no integrations available


errors on launching fleet service 
    2025-10-30 09:29:27 {"log.level":"error",
    "@timestamp":"2025-10-30T08:29:27.235Z",
    "log.origin":{"function":"github.com/elastic/elastic-agent/internal/pkg/agent/application/monitoring/reload.(*ServerReloader).Start",
    "file.name":"reload/reload.go",
    "file.line":58},"message":"Failed creating a server: failed to create api server: listen tcp 127.0.0.1:6791: bind: address already in use",
    "log":{"source":"elastic-agent"},"ecs.version":"1.6.0"} 



2025-10-30 10:18:32 {"log.level":"error",
    "@timestamp":"2025-10-30T09:18:32.247Z",
    "message":"failed to fetch elasticsearch version",
    "component":{"binary":"fleet-server",
    "dataset":"elastic_agent.fleet_server",
    "id":"fleet-server-default",
    "type":"fleet-server"},"log":{"source":"fleet-server-default"},"service.name":"fleet-server",
    "service.type":"fleet-server",
    "error.message":"dial tcp [::1]:9200: connect: connection refused",
    "ecs.version":"1.6.0",
    "ecs.version":"1.6.0"}
2025-10-30 10:18:32 {"log.level":"warn",
    "@timestamp":"2025-10-30T09:18:32.247Z",output configuration test
    "message":"Failed Elasticsearch , using bootstrap values.",
    "component":{"binary":"fleet-server",
    "dataset":"elastic_agent.fleet_server",
    "id":"fleet-server-default",
    "type":"fleet-server"},"log":{"source":"fleet-server-default"},"service.type":"fleet-server",
    "error.message":"dial tcp [::1]:9200: connect: connection refused",
    "output":{"Elasticsearch":{"Headers":null,"Hosts":["localhost:9200"],"MaxConnPerHost":128,"MaxContentLength":104857600,"MaxRetries":3,"Path":"",
    "Protocol":"https",
    "ProxyDisable":false,"ProxyHeaders":{},"ProxyURL":"",
    "ServiceToken":"[redacted]",                     _**Mutually exclusive with** --fleet-server-service-token-path._
    "ServiceTokenPath":"",
    "TLS":{"CASha256":null,"CATrustedFingerprint":"",
    "CAs":["/certs/ca/ca.crt"],"Certificate":{"Certificate":"",
    "Key":"",
    "Passphrase":"",
    "PassphrasePath":""},"CipherSuites":null,"CurveTypes":null,"Enabled":null,"Renegotiation":"never",
    "VerificationMode":"none",
    "Versions":null},"Timeout":90000000000},"Extra":null},"ecs.version":"1.6.0",
    "service.name":"fleet-server",
    "ecs.version":"1.6.0"}

--fleet-server-service-token <string>
Service token to use for communication with Elasticsearch. **Mutually exclusive with** --fleet-server-service-token-path.





2025-10-30 10:19:43 {"log.level":"error",
    "@timestamp":"2025-10-30T09:19:43.734Z",
    "message":"failed to fetch elasticsearch version",
    "component":{"binary":"fleet-server",
    "dataset":"elastic_agent.fleet_server",
    "id":"fleet-server-default",
    "type":"fleet-server"},"log":{"source":"fleet-server-default"},"service.name":"fleet-server",
    "service.type":"fleet-server",
    "error.message":"dial tcp [::1]:9200: connect: connection refused",
    "ecs.version":"1.6.0",
    "ecs.version":"1.6.0"}



https://www.elastic.co/docs/reference/fleet/agent-environment-variables#env-bootstrap-fleet-server

FLEET_SERVER_ES_CERT
FLEET_SERVER_CERT

https://www.elastic.co/docs/reference/fleet/secure-connections




## Elastic APM
http://localhost:5601/app/integrations/detail/apm/overview



## Elastic-agent
    - scrap JMX prometheus exporter

https://www.elastic.co/docs/reference/fleet/fleet-server#:~:text=Does%20Fleet%20Server%20run%20inside,a%20special%20Fleet%20Server%20policy.

Admonition
Does Fleet Server run inside of Elastic Agent?
Fleet Server is a subprocess that runs inside a deployed Elastic Agent.
This means the deployment steps are similar to any Elastic Agent, except that you enroll the agent in a special Fleet Server policy.
Typically—especially in large-scale deployments—this agent is dedicated to running Fleet Server as an Elastic Agent communication host and is not configured for data collection.


https://www.elastic.co/blog/getting-started-with-the-elastic-stack-and-docker-compose
https://www.elastic.co/blog/getting-started-with-the-elastic-stack-and-docker-compose-part-2


Agent in a Container: https://www.elastic.co/guide/en/fleet/current/elastic-agent-container.html
docker run --rm docker.elastic.co/elastic-agent/elastic-agent:9.2.0 elastic-agent container -h

which will spin up both Elastic Agent and Fleet Server in a container:

docker run \
--env FLEET_SERVER_ENABLE=true \
--env FLEET_SERVER_ELASTICSEARCH_HOST=<elasticsearch-host> \
--env FLEET_SERVER_SERVICE_TOKEN=<service-token> \
--env FLEET_SERVER_POLICY_ID=<fleet-server-policy> \
-p 8220:8220 \
--rm docker.elastic.co/elastic-agent/elastic-agent:9.2.0


https://www.elastic.co/docs/api/doc/elasticsearch/operation/operation-security-create-service-token
FLEET_SERVER_SERVICE_TOKEN
LWJnZkpwb0JfM0pMeHNBTElyZEQ6UU0yY3NJOEFuZllnLWlKS3hKUnhEZw==





https://www.elastic.co/docs/reference/fleet/fleet-enrollment-tokens#create-fleet-enrollment-tokens
    http://localhost:5601/app/fleet/enrollment-tokens









## NOTES

security 
https://www.elastic.co/docs/deploy-manage/deploy/self-managed/installing-elasticsearch


list of 
https://localhost:9200/_cat/indices



Kibana cannot reach the Elastic Package Registry, which provides Elastic Agent integrations
To view these integrations, configure a proxy server(external, opens in a new tab or window) or host your own registry(external, opens in a new tab or window).


https://www.elastic.co/docs/reference/fleet/air-gapped




Kibana cannot reach the Elastic Package Registry, which provides Elastic Agent integrations

To view these integrations, configure a proxy server(external, opens in a new tab or window) or host your own registry(external, opens in a new tab or window).
https://www.elastic.co/docs/reference/kibana/configuration-reference/fleet-settings#fleet-data-visualizer-settings
https://www.elastic.co/docs/reference/fleet/air-gapped


https://www.elastic.co/docs/reference/kibana/configuration-reference/fleet-settings#fleet-data-visualizer-settings
xpack.fleet.registryUrl
The address to use to reach the Elastic Package Manager registry.
xpack.fleet.registryProxyUrl
The proxy address to use to reach the Elastic Package Manager registry if an internet connection is not directly available. Refer to Air-gapped environments for details.
xpack.fleet.packageVerification.gpgKeyPath
The path on disk to the GPG key used to verify Elastic Package Manager packages. If the Elastic public key is ever reissued as a security precaution, you can use this setting to specify the new key.




Unable to initialize Fleet
Agent binary source needs encrypted saved object api key to be set



https://www.elastic.co/docs/deploy-manage/security/secure-saved-objects

λ openssl rand -base64 40
fqrDBbzVUD9qhl7YpgM+b8tlvfRTBs34E74UKg2smbaLzIBiv7RV0Q==

Docker configuration
XPACK_ENCRYPTEDSAVEDOBJECTS_ENCRYPTIONKEY="min-32-byte-long-NEW-encryption-key"
XPACK_ENCRYPTEDSAVEDOBJECTS_KEYROTATION_DECRYPTIONONLYKEYS[0]="min-32-byte-long-OLD#1-encryption-key"
XPACK_ENCRYPTEDSAVEDOBJECTS_KEYROTATION_DECRYPTIONONLYKEYS[1]="min-32-byte-long-OLD#2-encryption-key"




https://fortuneedema.medium.com/simplifying-elastic-stack-management-with-docker-compose-8a0e6b02cea0



https://evermight.com/docker-elk-2-agent-fleet-server-apm/
