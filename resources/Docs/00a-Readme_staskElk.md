


Stack ELK in docker compose 
    3 nodes elasticsearch for a cluster  
    - Container prometheanelk-es01-1
    - Container prometheanelk-es02-1
    - Container prometheanelk-es03-1
    
    Can't simply upgrade the stack number for elasticsearch nodes : they don't start and stay in errors    
    
    If need be, they could migrated one at a time to upgrade the stack ELK, to avoid data losses. 
    TODO : test that from a previous version with some data.


1 conteneur kibana 
    - Container kibana


1 apm-server so we can use fleet apm from kibana 


install of ES and kibana : straight forward,  



1 prometheus service : the database for time series in proemtheus 

1 grafana service : the UI connected to prometheus




http://localhost:5601/app/home#/tutorial/apm

last elastic apm agent : they are not restricted to an ELK stack version (at leaast not the recent ones)
[elastic-apm-agent-1.54.0.jar](../../../../../../Downloads/elastic-apm-agent-1.54.0.jar)









