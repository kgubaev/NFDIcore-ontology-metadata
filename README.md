# NFDIcore-ontology-metadata
Describing the metadata of semantic resources (repositories?) with NFDIcore

## TOC
 - intro
 - harvester tool description
 - ontology structure
 - describing metadata
 - class definitions


## Intro

Ontologies are crucial for knowledge sharing and reuse on the Semantic Web, but finding suitable ontologies can be challenging.  Effective ontology discovery and reuse depend on comprehensive metadata descriptions, but current metadata schemas have limitations, including limited scope, lack of harmonization, and maintenance issues.  This paper introduces a metadata schema for ontology repositories based on the Basic Formal Ontology (BFO) 2020 and the NFDIcore ontology new release 3.0.  This schema leverages BFO's standardized framework and NFDIcore's promising approach to knowledge graph managing, to address the limitations of existing schemas and enhance semantic interoperability and reasoning over metadata items.

## Harverster
h1 - we treat the you're right of the ontology at the unique identifier. Hence, 1 uri = 1 ontology object. Some people put number of the versions there either in fair slash release variant, etc., or even file extensions, which is the incorrect usage of URI.

## Ontology structure

1. Ontology object
   
Class:
The central object about which we discuss here is the ontology - an abstract concept, which stands for the designation and incorporates all its components: versions/modules/variants/ other artifacts. We treat the namespace of the ontology at the unique identifier. Hence, 1 namespace uri = 1 ontology object. Some people put number of the versions there either in fair slash release variant, etc., or even file extensions, which is the incorrect usage of namespace.  
3 Properties:
As proprties of the ontology, apart from the namespace URI, we have two types of text entities here: title and description.

2. 


## Describing metadata

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
