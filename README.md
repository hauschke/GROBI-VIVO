
## GROBI - Graphical observatories for bibliometric analyses

In the GROBI project, a reference implementation for bibliometric observatories is being researched and developed. The aim is to develop reusable infrastructures for bibliometric monitoring in various scenarios. To this end, open source workflows are being developed and prepared for various application scenarios with exemplary observatories for scientific journals, institutions, geographical units, specialised communities and funding bodies or funding instruments. The focus is on making bibliometric analyses and visualisations available to a broad target group.

To this end, approaches and methods from visual analytics and library and information science are combined. On the one hand, reliable implementations for common bibliometric methods based on open data sources are created. On the other hand, a graphical user interface with interactive visualisation options is created, by means of which the functionalities can be combined in a simple drag-n-drop interface and results can be exported. All components are published open-source in the form of individually reusable modules.


# How to use the images

To get a VIVO instance up and running using the docker images is quite simple. 

Install Docker or Docker Desktop (https://www.docker.com/get-started/)
Create a folder e.g. VIVO
Create a docker-compose.yml inside that folder (the following can be used without changes):

```
services:                                             
  solr:                                               
    image: bkampe/grobi-solr                          
    ports:                                            
      - 8985:8983                                     
    volumes:                                          
      - solr-data:/opt/solr/server/solr/ckan/data     
    command: solr-create -c vivocore -d /opt/vivocore 
    restart: always                                   
                                                      
  vivo:                                               
    image: bkampe/grobi-vivo                          
    volumes:                                          
      - vivo-home:/usr/local/data/home                
    ports:                                            
      - 8080:8080                                     
    restart: always                                   
                                                      
volumes:                                              
  solr-data:                                          
  vivo-home:
```

Run the following terminal command within the VIVO folder:

```
docker-compose -f docker-compose.yml up -d --build
```
When the process has finished a VIVO instance should be availabel at http://localhost:8080/GROBI
