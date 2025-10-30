



wget --no-check-certificate --user=elastic --password=elastic http://host.docker.internal:9200/



curl --insecure

curl --insecure -u elastic:elastic https://host.docker.internal:9200/
OK : the good one 


curl --insecure -u elastic:elastic https://es01:9200/
OK still good with insecure 

OK from fleet server 


curl --insecure -u elastic:elastic https://localhost:9200/




2025-10-30 11:48:51 {"log.level":"error",
    "@timestamp":"2025-10-30T10:48:51.724Z",
    "message":"failed to fetch elasticsearch version",
    "component":{"binary":"fleet-server",
    "dataset":"elastic_agent.fleet_server",
    "id":"fleet-server-default",
    "type":"fleet-server"},"log":{"source":"fleet-server-default"},"ecs.version":"1.6.0",
    "service.name":"fleet-server",
    "service.type":"fleet-server",
    "error.message":"dial tcp [::1]:9200: connect: connection refused",
    "ecs.version":"1.6.0"}
2025-10-30 11:48:51 {"log.level":"warn",
    "@timestamp":"2025-10-30T10:48:51.725Z",
    "message":"Failed Elasticsearch output configuration test, using bootstrap values.",
    "component":{"binary":"fleet-server",
    "dataset":"elastic_agent.fleet_server",
    "id":"fleet-server-default",
    "type":"fleet-server"},"log":{"source":"fleet-server-default"},"service.type":"fleet-server",
    "error.message":"dial tcp [::1]:9200: connect: connection refused",
    "output":{"Elasticsearch":{"Headers":null,"Hosts":["localhost:9200"],"MaxConnPerHost":128,"MaxContentLength":104857600,"MaxRetries":3,"Path":"",
    "Protocol":"https",
    "ProxyDisable":false,"ProxyHeaders":{},"ProxyURL":"",
    "ServiceToken":"[redacted]",
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



`"output":{"Elasticsearch":{"Headers":null,"Hosts":["localhost:9200"],`"MaxConnPerHost":128,"MaxContentLength":104857600,"MaxRetries":3,"Path":"",


[root@3fb837d74040 elastic-agent]# curl --insecure -u elastic:elastic https://localhost:9200/
curl: (7) Failed to connect to localhost port 9200: Connection refused





https://discuss.elastic.co/t/error-in-fleet-server-kibana-elastic-search/366362




You will also need to set ssl.verification_mode: none in the Output settings in Fleet and Integrations UI.
https://www.elastic.co/docs/reference/fleet/agent-environment-variables




localhost:9200



2025-10-30 13:52:31 {"log.level":"warn","@timestamp":"2025-10-30T12:52:31.497Z","message":"Failed Elasticsearch output configuration test, using bootstrap values.","component":{"binary":"fleet-server","dataset":"elastic_agent.fleet_server","id":"fleet-server-default","type":"fleet-server"},"log":{"source":"fleet-server-default"},"ecs.version":"1.6.0","service.name":"fleet-server","service.type":"fleet-server","error.message":"dial tcp [::1]:9200: connect: connection refused","output":{"Elasticsearch":{"Headers":null,"Hosts":["localhost:9200"],"MaxConnPerHost":128,"MaxContentLength":104857600,"MaxRetries":3,"Path":"","Protocol":"https","ProxyDisable":false,"ProxyHeaders":{},"ProxyURL":"","ServiceToken":"[redacted]","ServiceTokenPath":"","TLS":{"CASha256":null,"CATrustedFingerprint":"","CAs":["/certs/ca/ca.crt"],"Certificate":{"Certificate":"","Key":"","Passphrase":"","PassphrasePath":""},"CipherSuites":null,"CurveTypes":null,"Enabled":null,"Renegotiation":"never","VerificationMode":"none","Versions":null},"Timeout":90000000000},"Extra":null},"ecs.version":"1.6.0"}
2025-10-30 13:52:31 {"log.level":"info","@timestamp":"2025-10-30T12:52:31.497Z","message":"Found settings with recommended ram.","component":{"binary":"fleet-server","dataset":"elastic_agent.fleet_server","id":"fleet-server-default","type":"fleet-server"},"log":{"source":"fleet-server-default"},"ecs.version":"1.6.0","service.name":"fleet-server","service.type":"fleet-server","memory_mb":19998,"recommended_mb":16192,"ecs.version":"1.6.0"}


curl -s --cacert /usr/share/elasticsearch/config/certs/ca/ca.crt https://localhost:9200 | grep -q 'missing authentication credentials',
/usr/share/elasticsearch

- certs:/usr/share/elasticsearch/config/certs




config/certs/ca/ca.crt https:




elastic-agent.yml

This example configures an Elasticsearch output called default in the elastic-agent.yml file:

outputs:
    default:
        type: elasticsearch
        hosts: [127.0.0.1:9200]
        username: elastic
        password: elastic
    




.