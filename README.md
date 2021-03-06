# <center> The Panama Papers Project   </center>


# I - Introduction: The leaks


-- to be added

-- give appropriate credit

# II - The Data

 We consider the available data from the ICIJ database on the [_Panama papers_](https://offshoreleaks.icij.org/pages/database) and the _Swiss Leaks_ Github [repository](https://github.com/swissleaks/swiss_leaks_data). (Check if these are note the same, but in different formats. I think they are. See link in the repo).
 The database is powered by the graph database [Neo4j](https://neo4j.com/). The graph database has a perfect fit to the type of data at hand, as it reveals the network in a natural way, applying an organization scheme similar to the human mind .The data model used by ICIJ is explained [here](https://neo4j.com/blog/analyzing-panama-papers-neo4j/). In this models, one recognizes 4 types of entities:
 
 * Clients 
 * Companies
 * Addresses
 * Officers ( which can be either a person or a company) 
 
with relationships as (using Cypher, the language used in Neo4j):

 * (:Officer)-[:is officer of]->(:Company)
  
  with the classifications:
  * protector
  * beneficiary, shareholder, director
  * beneficiary
  * shareholder
  
 * (:Officer)-[:registered address]->(:Address)
 * (:Client)-[:registered]->(:Company)
 * (:Officer)-[:has simialr name or address]->(:Address)
  
 
## Issues with the data

 The ICIJ data contains a lot of duplicates, but only a small part of which is connected by a "has a similar name or address" relatioship. Another issue is that the shareholder information is stored with the "Officer", where the officer can be the share holder of any number of Companies. If the shareholder information would be stored in the "is officer of - Shareholer" relationship instead, we would remove the ambiguities in the shareholder information. [_source_](https://neo4j.com/blog/analyzing-panama-papers-neo4j/)
 
# III - Extending the data 
## Domain: Switzerland

 There are several ways to extend and enrich the _Panama papers_ database. Unfortunately, we don't have access to big part of the data and metadata from the original leaks. On the other hand, one can look for other sources and makes cross checks in order to complement the information at hand. This task is part of our project.
  
 In this project, we will focus on Switzerland. Due to the public interest, it is an obvious move to cover at least two groups of entities withing Switzerland:
 
 * Politicians
 * Coorporations
 
 We have pre-scanned the web for sources on the above entities. For identifying and investigating links with swiss corporations, we will make use of
 
 * [opencorporates](https://opencorporates.com/)
     * The largest open database of companies in the world with 115.272.454 companies.
     * Has an open API.
 * [moneyhouse](https://www.moneyhouse.ch/)
     * Has well structured data on a companie's
         * Nominal capital
         * board of directors
         * managers 
         * signatories
     * More information can be purchased.
  * [zefix](http://zefix.admin.ch/zfx-cgi/hrform.cgi/hraPage?alle_eintr=on&pers_sort=original&pers_num=0&language=4&col_width=366&amt=007)
      * Similar information content as money house
  * [wikipedia](https://en.wikipedia.org/wiki/List_of_Swiss_companies_by_revenue)
      * List of biggest swiss companies by revenue
      
 We have also access to a list of former and active swiss politicians.
          
 * https://www.parlament.ch/en/organe/national-council/members-national-council-a-z
 * https://www.parlament.ch/centers/documents/de/interessen-nr.pdf
 
 Moreover, we have a list of their _declared interests_, in which they officially declare which companies they support (make this more precise/complete).

- https://www.parlament.ch/centers/documents/de/interessen-nr.pdf
- https://www.parlament.ch/centers/documents/de/interessen-sr.pdf

at national and federal levels respectively.

 The difficulty with the above information is that we have only found it in pdf format. 

### Lobbying in Switzerland 
 We would like to investigate this official statements and identify unnofical ones. We keep in mind that political campaigns in Switerland are privately funded.
 
  
It is expected that these subgroups have intersections, which will naturally be highlighted. We will investigate links among people/companies based in Switzerland and those between elements outside Switzerland, whenever we consider it relevant.

On of the foreseeable achievements will be to reveal the networks in a similar fashion as it has been done in this example, for the Aliyev family in Azerbaijan: 

<img src="https://s3.amazonaws.com/dev.assets.neo4j.com/wp-content/uploads/20160408103432/azerbaijan-president-linkurious-fraud-ring.png" width=500>




## Extra: money flow

-  The super-rich