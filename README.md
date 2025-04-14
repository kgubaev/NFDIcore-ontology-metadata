# NFDIcore-ontology-metadata
Describing the metadata of semantic resources (repositories?) with NFDIcore

## TOC
 - intro
 - ontology metadata
 - describing metadata
 - harvester tool description
 - class definitions


## Intro

Ontologies are crucial for knowledge sharing and reuse on the Semantic Web, but finding suitable ontologies can be challenging.  Effective ontology discovery and reuse depend on comprehensive metadata descriptions, but current metadata schemas have limitations, including limited scope, lack of harmonization, and maintenance issues.  This paper introduces a metadata schema for ontology repositories based on the Basic Formal Ontology (BFO) 2020 and the NFDIcore ontology new release 3.0.  This schema leverages BFO's standardized framework and NFDIcore's promising approach to knowledge graph managing, to address the limitations of existing schemas and enhance semantic interoperability and reasoning over metadata items.

## Describing ontology metadata

### 1. Ontology object
   
Clases:
* ``nfdicore:Ontology``  <br/>
* ``nfdicore:NameSpace``  <br/>
* ``nfdicore:Title``  <br/>
* ``nfdicore:Description``  <br/>

Properties:

* ``obo:is about``  <br/>
  
The central object about which we discuss here is the ontology - an abstract concept, which stands for the designation and incorporates all its components: versions/modules/variants/ other artifacts. We treat the namespace of the ontology at the unique identifier. Hence, 1 namespace uri = 1 ontology object. Some people put number of the versions there either in fair slash release variant, etc., or even file extensions, which is the incorrect usage of namespace.  

As proprties of the ontology, apart from the namespace URI, we have two types of text entities here: title and description.

### 2. Ontology versions, variants and formats
   
Classes:

* ``nfdicore: Ontology Release Version``  <br/>
* ``nfdicore: Ontology Variant``  <br/>
* ``nfdicore: File Data Item``  <br/>

Properties:

* ``obo:is about``  <br/>
* ``obo:continuant part of``  <br/>
* ``nfdicore: has value``  <br/>

Similarly to what we have in software engineering repository for ontologies can contain different release versions with different features, e.g., ver. 0.1, ver. 1.2. This corresponds to the ontology release version class, which is connected with the property of or has continued part of ontology object. Each release version should ideally be characterized by its version IRI, for which we use nfdicore: has value data property. sometimes version iris are used incorrectly, containing information about file extensions or arbitrary comments. In turn, release verions can be present in different variants, meaning, e.g., "reasoned", where the inferred axioms are included, "full", with incorporated import statements. This corresponds to nfdicore: Ontology Variant class, which is obo: continuant part of the release version. If not specified explicitly, the variant of any version is considered to be "main release". The versions with all their variants are located in the files, having certain extensions. For this we use energy core data item which is about variants (now version!). 
This way, **any** triplet-containig file, belonging to the ontology corresponds to **one variant** of **one version**, and has **one extension**. 

### 3. Ontology repository, files and documentation links
   
![doc_files_url](https://github.com/user-attachments/assets/105c13cd-d07f-4ed3-8cb2-b04bbb7d7abc)

Classes:
* ``nfdicore:Source Code Repository``  <br/>
* ``edam:Format``  <br/>
* ``nfdicore:Website``  <br/>
* ``nfdicore:Document``  <br/>

Properties:

* ``obo:is about``  <br/>
* ``dcat:download URL``  <br/>
* ``nfdicore:has url``  <br/>
* ``obo:continuant part of``  <br/>

Nowadays, GitHub is a cornerstone of data exchange, particularly in the context of software development and increasingly for other types of data and information. Ontology is not an exception and very often the ontology and its corresponding files either the triple files or corresponding documentation ATC leaves within contents of some GitHub (gitlab?) repository. Therefore is crucial to reflect this information in the ontology metadata schema. We use the NFDIcore class Source Code repository, since the principles of data organization share a lot in common between the organized collections of triplet file (ontology), and source code files.

The ontology repository contains files with the triplets that are the essence of the ontology. While each ``nfdicore: File Data Item`` ``is about`` ontology and its variant objects, it is also ``obo:continuant part of`` the nfdicore:Source Code Repository object. In this way we specify the belongings of the files to the repository. As each file contains has its download link in parentheses GitHub repository address, we use dcat:download URL object property to connect the file to its link object, which is of the nfdicore:Website class.  if present we instantiate the nfdicore:Document object standing for the ontology documentation, which obo:is about the ontology object. 

Then to provide the corresponding links objects they are string representation we use an FDI core as URL data property:
* The ``nfdicore:Source Code Repository`` repository object ``nfdicore:has url`` the string, e.g., ``https://github.com/my-ontology^xsd:string``.
* The ``nfdicore: File Data Item`` file object ``nfdicore:has url`` the string, e.g., ``github.com/my-ontology/file.ttl^^xsd:string``.
* The ``nfdicore:Document`` documentation object ``nfdicore:has url`` the string, e.g., ``github.com/my-ontology/documentation.html^^xsd:string``.

### 4. Ontology creators and contact points
   
Classes:

* ``nfdicore:Agent``  <br/>
* ``nfdicore:Person``  <br/>
* ``nfdicore:Organization``  <br/>
* ``nfdicore:Creator Role``  <br/>
* ``nfdicore:Creative Process``  <br/>
* ``nfdicore:Contact Point Role``  <br/>
* ``nfdicore:Contacting Process``  <br/>

Properties:

* ``bfo:concretizes``  <br/>
* ``bfo:realizes``  <br/>
* ``bfo:bearer of``  <br/>
* ``bfo:participates in``  <br/>
* ``nfdicore: has creator``  <br/>
* ``nfdicore: has contact point``  <br/>
* ``obo:is about``  <br/>

As ontology, in principle, should be always developing as a result of discussions with interested parties, developers and domain experts, maintaining connections to the relevant people is crucial. Therefore such information there as creator of ontology or a contact point of ontology is crucial to describe this type of semantic resource.
To describe that particular person or an organization is a creator or a contact point of some ontology we use the so-called role pattern which is typical for the bfo-based ontologies. This means instead of the intuitively obvious solution to define a class of contact point / creator, and create a corresponding individual of that class, we do the following: instantiate the so-called roles which are specifically dependent continuants, which describe certain functions which, e.g., perrson plays in certain situation, for example the role of a father at home, or the role of a teacher at school. 
Then we say that there is some agent and it is bearer of contact point and/or creator role, which is realized in contacting or creative process correspondingly. Ontology then participates in the corresponding process. As the shortcuts we have the corresponding properties has contact point and has creator which connect ontology to the corresponding agent. This approach solves the problem when one agent is creator and contact point of different ontologies. 
Returning to our teacher and father example: if we would use the class-based approach, i.e., declaring new individuals for teacher, father, driver, buyer and so on, then we would end up in a situation where many of these classes stand for one person. And if we want to specify, let's say, the name of that person we would need to do this for all of these classes, unecessarily multiplying the object properties, pointing to the name. And how to clearly distinguish between the situations when the buyer, teacher, and father are and are not the one person? This is further complicated by the fact that in different situations this person can be called by different names at home or at school, so comparison of the names is not that straightforward. 
The role-based pattern on the other hand helps to solve this problem by correctly modeling this aspect of reality: actually there is a person that bears the role which is realized in a particular situation (process). This way, we use the following schema:

## Harvester tool description

To facilitate the collection and structuring of information about ontologies do you use the automated 2 so-called GitHub repository harvester. It scans the repository checks the LDF containing files if any of them are apologies and then extracts the corresponding information which is to be put into the MSE knowledge graph. Some data curation of the automated output is still necessary however it is very minor part of work compared to the whole process this way it is by 90 to 95% automatized.



## Class definitions

Ontology - An (nfdi) ontology is a data item that coherently represents all components of an ontology, including its versions, variants, modules and other associated artifacts. It is typically denoted by a name and/or an acronym, which is the term we use to communicate about it.An (nfdi) ontology is a data item that coherently represents all components of an ontology, including its versions, variants, modules and other associated artifacts. It is typically denoted by a name and/or an acronym, which is the term we use to communicate about it.

O. Release Version - An (nfdi) ontology release version represents a particular release of an ontology.

O. Namespace - A namespace refers to a distinct, unique identifier that is used to distinguish concepts and entities within an ontology from those in other ontologies or systems. It's typically represented as a URL or URI (Uniform Resource Identifier) and ensures that each element within the ontology has a globally unique reference.

O. Variant - An ontology variant represents a self-contained, reusable subset of an ontology that provides a specific functionality while maintaining interoperability with the larger ontology. Typically, an ontology is released in different variants, which makes a variant a release artifact.

File Data Item - A file data item is a data item that represents a file stored on a hard drive. It might also include essential attributes like its name, location, download URL, size, type, and timestamps for creation, modification, and access. It might also capture permissions and ownership details to control how the file can be accessed or modified.

Source Code Repository - A document that organizes and stores source code files, associated metadata, and version history to facilitate the management, sharing, and collaborative development of software projects. It serves as a structured collection of information that tracks changes, maintains integrity, and supports workflows such as version control, branching, and merging.

Website - An information content entity that represents a collection of interconnected web pages, multimedia content, and digital resources accessible via the World Wide Web.

Title - A textual entity that denotes some resource.

Description  - A textual entity that describe some resource.

Contact Point - An agent that serves as a designated interface for communication, facilitating the exchange of information, support, or services between individuals, organizations, or systems.
