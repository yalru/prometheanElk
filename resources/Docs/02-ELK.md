# Stack ELK


## Kibana 
UI used to load elastic agents and setup fleet server 


## Fleet server
install a fleetserver 
-> elastic agent used as a fleet server     
![fleet-server-agent-policies-diagram.png](picts/fleet-server-agent-policies-diagram.png)



https://www.elastic.co/docs/reference/kibana/configuration-reference/fleet-settings#fleet-data-visualizer-settings





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








## NOTES

list of 
https://localhost:9200/_cat/indices



Kibana cannot reach the Elastic Package Registry, which provides Elastic Agent integrations
To view these integrations, configure a proxy server(external, opens in a new tab or window) or host your own registry(external, opens in a new tab or window).


https://www.elastic.co/docs/reference/fleet/air-gapped


