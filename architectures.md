# Comparison of architectures (work in progress)

This is page is intended to document changes in the architecture of biocache to a pipelines based deployment.

## Current architecture
![Existing architecture](https://docs.google.com/drawings/d/e/2PACX-1vQPYIjmbt1e-PNU0ZK6FpYpqxw4xQj4A3tXHjEZIQ3ZGPnwj0cBCdFgEs_SNnccR0rGcnpOFWgqYlLS/pub?w=960&h=720)

#### Notes on the diagram
* BStore instances are virtual machines with following installed:
  * biocache-store executable
  * ala-namematching lucene index
  * SDS required shape file layers
* The connection between BStore instances and the SolrCloud cluster is just for copying built indexes into the production cluster. No "live" indexing currently takes place.

## New architecture
![New architecture](https://docs.google.com/drawings/d/e/2PACX-1vSGixRyj2cCyZjGFdcMZflYLXU_VuiA4Y6CIkNiF4DHLFOa03613iolLFOaDX_-AqnhMu6qdJn-veVA/pub?w=960&h=720)

#### Notes on the diagram
* The use of cassandra is still something under review. There needs to be storage of the UUID mapping. It maybe be possible to do this without using cassandra and using a serialisation of UUID mappings stored on a dataset by dataset basis on the filesystem. Having no connection from pipelines to cassandra is attractive as it reduces barriers to run ALA pipelines in other environments (e.g. GBIF). This work is being tracked in this [issue](https://github.com/AtlasOfLivingAustralia/la-pipelines/issues/14). If cassandra is used, a reduced cluster can utilitised (2 nodes, lower specification for VMs). 
* Cassandra still required by biocache-service to store
  * annotations
  * QID - query IDs, persisted SOLR queries stored in JSON.
  * sandbox metadata
* The connection between Spark and the SolrCloud cluster differs in that spark will make use of the SOLR HTTP API to index directly into the SOLR cloud cluster.
* The orchestration around index generation is yet to be designed & tested. This is being tracked in this [issue](https://github.com/AtlasOfLivingAustralia/la-pipelines/issues/25).
* Spark nodes will have the following installed:
  * spark
  * ala-namematching-service
  * SDS required shape file layers
  * la-pipelines build JAR file.



