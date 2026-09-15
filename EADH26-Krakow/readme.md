# EADH 2026 Conference - Knowledge Graphs and Linked Open Data made (quite) easy: OntoME, SHACL, Logre

## Abstract

The workshop aims to provide a hands-on introduction to information management and analysis in the form of knowledge graphs (KG) and linked open data (LOD). It will cover all the relevant steps, from harvesting existing open data from various sources (e.g. Wikidata, DBPedia, IdRef/SUDOC and Data BNF), to transforming and integrating it into a common and refined repository. Finally, it will demonstrate how to query the data to obtain initial insights relating to specific research questions.

## Useful links

Docker desktop
- install: https://docs.docker.com/get-started/get-docker/

Logre
- instal: https://github.com/lod4hss-apps/logre/tree/dev/

OntoME
- main page: https://ontome.net/
- login page: https://ontome.net/login

Introduction slides
- https://docs.google.com/presentation/d/174juy0Lm9cX6xIAJZgBu-AvYngTVz2Lx9R5QuDo-77M/edit?usp=sharing

Walkthrough (OntoME and LOGRE tutorial):
- https://outline.lod4hss.org/s/225a54b8-ccb1-4822-9802-ad5bbf381019

## Workshop description

### Aims and set up of the workshop

Knowledge Graphs (KG) and Linked Open Data (LOD) have enormous potential for publishing and reusing research data. They could contribute to the ongoing paradigm shift in the way humanities and social sciences research is conducted digitally, notably by increasing the amount of information available to answer research questions and making it more easily reusable for new research agendas [Beretta 2023]. However, this process requires specific skills that are difficult to acquire through self-study. This applies not only to the computational methods that enable the analysis of vast amounts of information but also to the management of complex and extensive datasets that exceed the capability of spreadsheets and necessitate the implementation of appropriate information systems. Although KG, based on RDF and ontologies (i.e. shared, formalised conceptualisations of research domains), can provide an adequate and flexible framework, the learning curve is quite steep.

The workshop provides participants with a ‘learning by doing’ experience through a preconfigured course that introduces them to concepts and tools they could use individually or collectively in future research. It also aims to promote and develop the LOD4HSS initiative as a community of practice where interested researchers and projects can access tools and documentation, and contribute to their development (see below).
Participants will work on a project examining the evolution of the disciplines of astronomy and physics in the 19th and 20th centuries. Traditionally, analogue scholarship involves case studies contextualised through existing literature, producing a narrative model limited by the fragmented nature of the analysed information, without the possibility of empirically testing research hypotheses. In the new research paradigm, the reuse and integration of available information in the form of distributed knowledge graphs will enable the modelling of the evolution of scientific disciplines using computational methods. This will produce statistical models and visualisations that challenge, enrich and foster traditional analogue scholarship.

Participants will discover how to understand the meaning of the data available on Wikidata, DBPedia, Data BNF, IdRef/SUDOC, etc., regarding a population of scientists, and how to harvest the data using SPARQL. This publicly available data is linked in the logic of LOD, so that the information about the same persons and organisations is split across different repositories. We will provide a shared online repository where the information will already be imported in order to skip this step (which can be time-consuming) and explain the principles of this task. 

Participants will also learn about the fundamental principles of the SDHSS ontology ecosystem (see below), and how these cover prosopographic information modelling regarding births and origins of a population of scientists, the organisations where they were active, their memberships and publications. This ontological discovery will take advantage of the OntoME (ontome.net) platform, allowing the easy exploration of the classes and properties, and observation on how they are collected in application profiles (https://ontome.net/project/201#profiles) that can be reused for data integration, production and publication.

The available information previously collected, conceptualised with different conceptual models, will then be wrangled, integrated and enriched using SPARQL with the aim of preparing a consistent, SDHSS-based dataset in view of data analysis. We will raise the issue of redundant and contradictory information about the same facts, and how to cope with it. At this stage, we will introduce Logre (https://github.com/lod4hss-apps/logre), a SHACL-based, open-source data editor that allows users to explore and manually edit data available in any triplestore. Participants will be introduced to the basic principles of the RDF language SHACL and then to the way of importing SHACL application profiles available in OntoME into Logre, regarding births, memberships, occupations and publications, in order to inspect existing data and produce new ones.

Finally, participants will use pre-written Python notebooks to explore how querying the integrated data works and how basic analyses and visualisations can be produced. After an inspection of the available information with univariate distributions, we will propose bivariate and multivariate analysis of the features of the population and the publications of the scientists, as well as an analysis of the network of the institutions they belonged to,  observing the evolution in time of both aspects.
Because the workshop aims to provide a basic experience of the whole workflow, some hands-on exercises will be provided for each major step. In the analysis part, we will explore with the participants the Python notebooks about the relations between origins and activities, and invite them to modify and experiment on other features.

### Academic background for the work

The LOD4HSS initiative (https://lod4hss.org/) aims to help researchers learn and use KG and LOD technologies, andto produce and publish their research data in accordance with the FAIR principles. The initiative also aims to facilitate the reuse of existing data, thereby realising the full potential of these technologies for research with digital analysis tools.

This initiative is based on twenty years of experience in collaborative data management and analysis, initiated in 2008 by the Digital History Research Team and the symogih.org project at LARHRA (Lyon). Since 2016, we have adopted the vision of the Semantic Web and developed a suitable methodology and an ontology ecosystem, the Semantic Data for Humanities and Social Sciences (SDHSS) project (sdhss.org), collaboratively managed in the ontome.net web application. SDHSS relies on CIDOC CRM as a core ontology, adding the extensions needed for HSS research [Beretta 2024a]. In line with the approach  of LOD, the LOD4HSS initiative promotes the connection of research data to authority files (such as IdRef, BNF, GND, Wikidata) as well as other project’s open data repositories. 

This LOD4HSS initiative is built on two main pillars:
- On the one hand, we have adopted he Wiss-KI research and data publication infrastructure (https://wiss-ki.eu/), which totally fits in the semantic web and LOD vision. We are also working to improve its connection to the OntoME platform to make it easier to use.
- On the other hand, by adopting or developing open-source innovative semantic tools (like the Local Graph Editor LOGRE), in order to establish a community of best practices and standardise workflows to foster a distributed approach to KG and LOD (https://github.com/lod4hss-apps).

The present workshop builds upon the experience and learnings of the workshop at the DH 2025 Lisbon conference, where we tested the data collection and integration workflow (https://github.com/lod4hss-projects/workshops/tree/main/DH25-Lisbon). It is also based on Francesco Beretta’s five-year practice of teaching digital methodology in the humanities Master course at the Universities of Neuchâtel and Fribourg, where a similar workflow was applied [Beretta 2024b].

### Bibliography

- [Beretta 2023] Beretta, Francesco, «Données ouvertes liées et recherche historique : un changement de paradigme», Humanités numériques 7, 01.07.2023, https://doi.org/10.4000/revuehn.3349.
- [Beretta 2024a] Beretta, Francesco, «Conceptualising Information Production in the Context of the SDHSS Ontology Ecosystem», Methodos : savoirs et textes 24, 16.12.2024, https://doi.org/10.4000/12xqn.
- [Beretta 2024b] Beretta, Francesco, «Contributing to a Paradigm Shift in Historical Research by Teaching Digital Methods to Master’s Students», Digital History Switzerland 2024, 13.09.2024, https://doi.org/10.5281/zenodo.13907693.
- [Hart/Beretta 2025] Hart, Stephen / Beretta, Francesco, The LOD4HSS Initiative: Developing FAIR Knowledge Graph Practices in the Humanities and Social Sciences, (Blogreihe: Open Science in der Schweiz),15. September 2025, https://www.infoclio.ch/de/node/190093.
