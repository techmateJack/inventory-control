# Tooling Decisions

## Data Persistence Layer

### SQL or NoSQL

Favour NoSQL for the folowing reasons:
- Less mental overheads re using SQL 
- no JOINS / UNIONS 
- ~~single table~~ - some whole / part relations
- ragged table structure / variable number of columns per row

Disadvantages of NoSQL
- less flexibilty in design comapred to normalised schema
- following on - view desgn needs to inform data model


### MongoDB or CouchDB

Unfortunately Fedora has a dropped MongoDB support because the software 
licencing since 2018 violates Fedora's scrict FOSS only policies.

Apache CouchDB seems an excellent alternative and has added benefits:

- Mature project since 2005
- ACID compliant
- Document based model (like MongoDB)
- uses RESTful HTTP API (unlike MongoDB's proprietary API)

## Middleware

### NodeJS Express or Python Django

1. Express pros / cons

2. Django pros/ cons

[relevent post]
(http://leok.me/2013/05/02/what-you-need-to-know-couchdb-django/)