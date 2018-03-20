# Virtual Assembly's ontology design convention

This document describes the ontology design convention and evaluation followed by Virtual Assembly.
The usefulness of such evaluation process is motivated in [5][5].
In addition, we recall the [OOPS! common pitfalls catalogue][15] and provide additional remarks.

## Table of Contents
- [Conventions](#conventions)
  - [Domain of the ontology](#domain)
  - [Naming](#naming)
  - [Labeling and annotations](#labeling)
  - [Class definition](#class-definition)
  - [Class hierarchy](#class-hierarchy)
  - [Properties and datatypes](#properties-and-datatypes)
  - [Ontology definition](#ontology-definition)
  - [Ontology extension](#ontology-extension)
  - [Designing a thesaurus](#designing-a-thesaurus)
- [Pitfalls in PAIR](#pitfalls-in-pair)
- [TODO](#todo)
- [References](#references)

## Conventions

### Domain of the ontology

In the context of the Virtual Assembly, we see two main purposes in the design of ontologies:
* Offer a lightweight and open API allowing to make understandable some data to some machine (see the RDF standard) thanks to explicit assertions
* Use descriptive logic to make inferences about new meta-relationships (see the OWL standard).
There is a tradeoff between the power provided by inferences in complex models and the rapidity of the extraction of information from triplet banks.

Keep in mind that the domain of the ontology depends on its purpose.
Indeed, there is a tradeoff between the universality of the ontology and the precision of what is described by the ontology
(e.g. in the definition of the domain and range of properties).
Where the cursor is chosen to be put should be made explicit in an annotation describing the domain of the ontology.

* Pitfall 09. **Missing domain information**: Part of the information needed for modeling the intended domain is not included in the ontology. This pitfall may be related to (a) the requirements included in the Ontology Requirement Specification Document (ORSD, [18][18]) that are not covered by the ontology, or (b) to the lack of knowledge that can be added to the ontology to make it more complete.

### Naming

* Meaningful URI local names are used, in English
* The CamelBack notation is followed for class and property names: 
  * Class and individual names should start with a capital letter and should not contain spaces nor underscores, e.g. `WorkingGroup`
  * Object and data property names start with a lowercase, e.g. `isTypeOf`
  * Following words start with a capital letter
* Object property names start with an active verb, e.g. `knowsPerson`, `isKnownBy`, `hasName`
* Data property names need not start with an active verb, e.g. `address`
* The singular is used.
* Pitfall 01. **Creating polysemous elements**: An ontology element (class, object property or datatype property) whose identifier has different senses is included in the ontology to represent more than one conceptual idea or property.
* Pitfall 22. **Using different naming conventions in the ontology**: The ontology elements are not named following the same convention (for example CamelCase or use of delimiters as "-" or "_") . Some notions about naming conventions are provided in [2][2].

### Labeling and annotations 

We follow the recommendations of [4][4]:
* All objects, properties and individuals are labeled
* Provide labels that guarantee human readability and that can be easily matched in free text
* We also recommend to add comments to provide more complete descriptions of the classes and properties
* Labels for classes should be as short as possible, self-contained, meaningful, and concise (see [1][1])
* For properties, use verbal phrases and the addition of the predicate or range of the relation for disambiguation purposes.
For example `(Organization) hasSiteAt (Site)`.
* The language of the label is given
* Labels are at least given in English and in the natural language of the developer
* The traduction of labels in other languages is highly recommended
* Follow language conventions (e.g. upper case for city names)
* Use singular form
* Use the genders corresponding to the classes labels, e.g. `(Personalité) est affiliée à (Organisation)`
* Include as many labels as useful for the final applications
* Labeling of similar concepts should be made in a coherent way. For instance, use either `chicken` and `beaf` or `chicken meat` and `beaf meat` rather than `chicken` and `beaf meat`.
* Pitfall 08. **Missing annotations**: This pitfall consists in creating an ontology element and failing to provide human readable annotations attached to it. Consequently, ontology elements lack annotation properties that label them (e.g. rdfs:label, lemon:LexicalEntry, skos:prefLabel or skos:altLabel) or that define them (e.g. rdfs:comment or dc:description). This pitfall is related to the guidelines provided in [5][5].
* Pitfall 20. **Misusing ontology annotations**: The contents of some annotation properties are swapped or misused. This pitfall might affect annotation properties related to natural language information (for example, annotations for naming such as rdfs:label or for providing descriptions such as rdfs:comment). Other types of annotation could also be affected as temporal, versioning information, among others.
* Pitfall 32. **Several classes with the same label**: Two or more classes have the same content for natural language annotations for naming, for example the rdfs:label annotation. This pitfall might involve lack of accuracy when defining terms.

### Class definition 

* Pitfall 02. **Creating synonyms as classes**: Several classes whose identifiers are synonyms are created and defined as equivalent (owl:equivalentClass) in the same namespace. This pitfall is related to the guidelines presented in [2][2], which explain that synonyms for the same concept do not represent different classes.
* Pitfall 03. **Creating the relationship "is" instead of using "rdfs:subClassOf", "rdf:type" or "owl:sameAs"**: The relationship "is" is created in the ontology instead of using OWL primitives for representing the subclass relationship (rdfs:subClassOf), class membership (rdf:type), or the equality between instances (owl:sameAs). When concerning a class hierarchy, this pitfall is related to the guidelines for understanding the "is-a" relation provided in [2][2].

   *Remark: In particular, use sub-classes for fixed concepts rather than introducing a class Type. For example, `Document` with sub-class `Tutorial`, `Scientific Article`, etc. For sub-concepts that vary, use relationships between individuals, such as `hasThema`. When extending new sub-classes, care should be taken to preserve backward compatibility.*

* Pitfall 14. **Misusing "owl:allValuesFrom"**: This pitfall consists in using the universal restriction (owl:allValuesFrom) as the default qualifier instead of the existential restriction (owl:someValuesFrom). Additional information about this pitfall is provided in [7][7].
* Pitfall 15. **Using "some not" in place of "not some"**: The pitfall consists in using a "some not" structure when a "not some" is required. This is due to the misplacement of the existential quantifier (owl:someValuesFrom) and the negative operator (owl:complementOf). (a) When to use a "some not" structure (DrelationshipS: ClassA): to state that there is at least one individual acting as object of the relationship "relationshipS" and such individual do not belong to class "ClassA". This implies that there must be at least one instantiation of the relationshipsS whose target does not belong to "ClassA". This does not prevent instances from ClassA acting as objects of the relationships. (b) When to use a "not some" structure ( DrelationshipS:ClassA): to state that no individuals in class "ClassA" act as objects of the relationship "relationshipS". This does not imply the existence of individuals from other classes acting as objects of the relationship. This pitfall is explained in more detail in [7][7].
* Pitfall 16. **Using a primitive class in place of a defined one**: "Primitive" classes are those for which there are only necessary conditions [7][7]. They are described using rdfs:subClassOf. "Defined" classes are those for which there are necessary and sufficient conditions [7][7]. They are described using owl:equivalentClass. This pitfall implies creating a primitive class rather than a defined one in case automatic classification of individuals is intended. It should be clarified that, in general, nothing will be inferred to be subsumed under a primitive class by the classifier [7][7]. This pitfall is related to the open world assumption.
* Pitfall 21. **Using a miscellaneous class**: This pitfall refers to the creation of a class with the only goal of classifying the instances that do not belong to any of its sibling classes (classes with which the miscellaneous problematic class shares a common direct ancestor).
* Pitfall 34. **Untyped class**: An ontology element is used as a class without having been explicitly declared as such using the primitives owl:Class or rdfs:Class. This pitfall is related with the common problems listed in [8][8].

### Class hierarchy

* Avoid including abstract classes used in a preliminary design phase in the final ontology when these classes are not practical.
* Pitfall 06. **Including cycles in a class hierarchy**: A cycle between two classes in a hierarchy is included in the ontology. A cycle appears when some class A has a subclass (directly or indirectly) B, and at the same time B is a superclass (directly or indirectly) of A. This pitfall was first identified in [3][3]. Guidelines presented in [2][2] also provide recommendations to avoid this pitfall.
* Pitfall 07. **Merging different concepts in the same class**: A class whose name refers to two or more different concepts is created, e.g. `GoodOrService`
* Pitfall 10. **Missing disjointness**: The ontology lacks disjoint axioms between classes or between properties that should be defined as disjoint. This pitfall is related with the guidelines provided in [6][6], [2][2] and [7][7].
* Pitfall 17. **Overspecializing a hierarchy**: The hierarchy in the ontology is specialized in such a way that the final leaves are defined as classes and these classes will not have instances. Authors in [e] provide guidelines for distinguishing between a class and an instance when modeling hierarchies.
* Pitfall 24. **Using recursive definitions**: An ontology element (a class, an object property or a datatype property) is used in its own definition. Some examples of this would be: (a) the definition of a class as the enumeration of several classes including itself; (b) the appearance of a class within its owl:equivalentClass or rdfs:subClassOf axioms; (c) the appearance of an object property in its rdfs:domain or range rdfs:range definitions; or (d) the appearance of a datatype property in its rdfs:domain definition.

   *Remark: class constraints should only be used to characterize the class and not as repetition of properties with a given domain and range.
As an example, the dectionary definition of a "person" does not state that a person is a "thing" that "knows" a "person".
Rather, this relationship is described in the definition of "know".*

* Pitfall 30. **Equivalent classes not explicitly declared**: This pitfall consists in missing the definition of equivalent classes (owl:equivalentClass) in case of duplicated concepts. When an ontology reuses terms from other ontologies, classes that have the same meaning should be defined as equivalent in order to benefit the interoperability between both ontologies.

	*Remark: Note  that owl:sameAs and owl:equivalentClass are different. owl:sameAs means that the two classes are identical. Two classes may have different definitions, but refer to the same individuals, and should thus be defined as equivalent.*

* Pitfall 31. **Defining wrong equivalent classes**: Two classes are defined as equivalent, using owl:equivalentClass, when they are not necessarily equivalent.

### Properties and datatypes

* Pitfall 05. **Defining wrong inverse relationships**: Two relationships are defined as inverse relations when they are not necessarily inverse.
* Pitfall 11. **Missing domain or range in properties**: Object and/or datatype properties without domain or range (or none of them) are included in the ontology.

	*Remark: when designing a universal ontology, one can give a general domain or range such as owl:thing
or, better, introduce an abstract general concept which is different and more specific than owl:thing (while remaining vague).*

* Pitfall 12. **Equivalent properties not explicitly declared**: The ontology lacks information about equivalent properties (owl:equivalentProperty) in the cases of duplicated relationships and/or attributes.
* Pitfall 13. **Inverse relationships not explicitly declared**: This pitfall appears when any relationship (except for those that are defined as symmetric properties using owl:SymmetricProperty) does not have an inverse relationship (owl:inverseOf) defined within the ontology.

	*Remark: there may be occasions when an inverse is not semantically relevant. In this case, the latter could be omitted.*
	
* Pitfall 18. **Overspecializing the domain or range**: This pitfall consists in defining a domain or range not general enough for a property, i.e, no considering all the individuals or datatypes that might be involved in such a domain or range. This pitfall is related to the guidelines provided in [2][2] and [7][7].
* Pitfall 19. **Defining multiple domains or ranges in properties**: The domain or range (or both) of a property (relationships and attributes) is defined by stating more than one rdfs:domain or rdfs:range statements. In OWL multiple rdfs:domain or rdfs:range axioms are allowed, but they are interpreted as conjunction, being, therefore, equivalent to the construct owl:intersectionOf. This pitfall is related to the common error that appears when defining domains and ranges described in [7][7].

   *Remark: Unions of different concepts in the domain and/or the range of a property should be avoided. For instance this may lead to allowing one to link a concept in the domain to another unrelated one in the range. Instead, properties should be specialized. For example, `knowsPerson` and `knowsThema` instead of `knows`. This is related to Pitfall 01.*

* Pitfall 23. **Duplicating a datatype already provided by the implementation language**: A class and its corresponding individuals are created to represent existing datatypes in the implementation language.
* Pitfall 25. **Defining a relationship as inverse to itself**: A relationship is defined as inverse of itself. In this case, this relationship could have been defined as owl:SymmetricProperty instead.
* Pitfall 26. **Defining inverse relationships for a symmetric one**: A symmetric object property (owl:SymmetricProperty) is defined as inverse of another object property (using owl:inverseOf).
* Pitfall 27. **Defining wrong equivalent properties**: Two object properties or two datatype properties are defined as equivalent, using owl:equivalentProperty, even though they do not have the same semantics.
* Pitfall 28. **Defining wrong symmetric relationships**: A relationship is defined as symmetric, using owl:SymmetricProperty, when the relationship is not necessarily symmetric.
* Pitfall 29. **Defining wrong transitive relationships**: A relationship is defined as transitive, using owl:TransitiveProperty, when the relationship is not necessarily transitive.n
* Pitfall 33. **Creating a property chain with just one property**: The OWL 2 construct owl:propertyChainAxiom allows a property to be defined as the composition of several properties (see [16][16] for additional details). In this sense, when an individual "a" is connected with an individual "b" by a chain of two or more object properties (specified in the antecedent of the chain), it is necessary to connect "a" with "b" by using the object property in the consequent of the chain. This pitfall consists in creating a property chain (owl:propertyChainAxiom) that includes only one property in the antecedent part.
* Pitfall 35. **Untyped property**: An ontology element is used as a property without having been explicitly declared as such using the primitives rdf:Property, owl:ObjectProperty or owl:DatatypeProperty. This pitfall is related with the common problems listed in [8][8].

### Ontology definition

* (Pitfall 04. **Creating unconnected ontology elements**: Ontology elements (classes, object properties and datatype properties) are created isolated, with no relation to the rest of the ontology).

    *Remark: we leave this pitfall in brackets, as it may be useful to collect disconnected concepts in one coherent ontology (e.g. the Dublin Core ontology).*

* (*Linked Data Feature*) Pitfall 36. **URI contains file extension**: This pitfall occurs if file extensions such as ".owl", ".rdf", ".ttl", ".n3" and ".rdfxml" are included in an ontology URI. This pitfall is related with the recommendations provided in [9][9].

* (*Linked Data Feature*) Pitfall 37. **Ontology not available on the Web**: This pitfall occurs when the ontology code (OWL encoding) or its documentation (HTML document) is missing when looking up its URI. This pitfall deals with the first point from the Linked Data star system that states "On the web" ([10][10] and [11][11]). Guidelines in [12][12] also recommends to "Publish your vocabulary on the Web at a stable URI". This pitfall is also related to the problems listed in [8][8] and [5][5].

	*Remark: the ontology should be at the same address as that pointed by the URI in the definition of the ontology.*

* Pitfall 38. **No OWL ontology declaration**: This pitfall consists in not declaring the owl:Ontology tag, which provides the ontology metadata. The owl:Ontology tag aims at gathering metadata about a given ontology such as version information, license, provenance, creation date, and so on. It is also used to declare the inclusion of other ontologies.
* (*Linked Data Feature*) Pitfall 39. **Ambiguous namespace**: This pitfall consists in declaring neither the ontology URI nor the xml:base namespace. If this is the case, the ontology namespace is matched to the file location. This situation is not desirable, as the location of a file might change while the ontology should remain stable, as proposed in [12][12].
* (*Linked Data Feature*) Pitfall 40. **Namespace hijacking**: It refers to reusing or referring to terms from another namespace that are not defined in such namespace. This is an undesirable situation as no information can be retrieved when looking up those undefined terms. This pitfall is related to the Linked Data publishing guidelines provided in [11][11]: "Only define new terms in a namespace that you control" and to the guidelines provided in [5][5].
* Pitfall 41. **No license declared**: The ontology metadata omits information about the license that applies to the ontology.

	*Remark: One can use the license property of the [dc/terms](http://purl.org/dc/terms/) ontology.*

### Designing a thesaurus

See the [SKOS reference][17].

### Ontology extension

* Prefer extending existing universal ontologies rather than developing new ones. Some of them can be found on [LOV][http://lov.okfn.org/dataset/lov/].
* Favor modular designs. When extending an ontology, import the ontology but do not modify it.
Instead, use `owl:sameAs` to define equivalent classes to be developed.
For example, the `PAIR` ontology can be extended with a `project management` module,
but `PAIR` remains a federating ontology that can be used by various types of organizations.
* When defining a class or a property as equivalent to one of an external ontology,
the more specifications than the ones from the external ontology should be added.
To add more specifications, define the class or property as, respectively, a subClassOf or a subPropertyOf instead.

## Pitfalls in PAIR

* Several naming conventions are used.
* Some properties do not use active verbs.
* Many domain and ranges are missing.
* Labels are missing.
* Too many constraints defining classes. Defining the domain and range of a relationship is sufficient.
* isTypeOf should be replaced by either:
  * Sub-classes, if the later are known and fixed (e.g. `Association` and `Company` as sub-classes of `Organization`)
  * The addition of a property allowing to specify the difference between individuals (e.g. the property `hasThema` from `WorkingGroup` to `Thema`)
* Import the PAIR ontology without modifying it when extending it.
* `GoodOrService` merges different concepts in one class.
* `Good` is polysemous.
* A license is missing.
* The domain is not well described.
* Disjointness is missing.
* Domains and ranges make the uninion of different concepts. Properties should be specialized.
* Remove abstract classes What, When, etc.
* Remove extension from URI of PAIR ontology

## TODO

* Regarder comment les ontologies qui font reference respectent ou non ces indications, e.g.:
  * DC
  * FOAF
  * SCHEMA
  * ORG
* Talk about modifications of PAIR with Seb et Simon for SemApps


## References

[Aguado-De Cea, G., Montiel-Ponsoda, E., Poveda-Villalón, M., and Giraldo-Pasmin, O.X. (2015). *Lexicalizing Ontologies: The issues behind the labels. In Multimodal communication in the 21st century: Professional and academic challenges*. 33rd Conference of the Spanish Association of Applied Linguistics (AESLA), XXXIII AESLA.][1]

[Noy, N. F., McGuinness, D. L., et al. (2001). *Ontology 101.*][2]

[Gómez-Pérez, A. (1999). *Evaluation of Taxonomic Knowledge in Ontologies and Knowledge Bases.*][3]

[Montiel-Ponsoda, E., Vila Suero, D., Villazón-Terrazas, B., Dunsire, G., Escolano Rodríguez, E., Gómez-Pérez, A. (2011). *Style Guidelines for Naming and Labeling Ontologies in the Multilingual Web.*][4]

[Vrandecic, D. (2010). *Ontology Evaluation*. PhD thesis.][5]

[Gómez-Pérez, A. (2004). *Ontology evaluation*. In Handbook on ontologies, pages 251-273. Springer.][6]

[Rector, A., Drummond, N., Horridge, M., Rogers, J., Knublauch, H., Stevens, R., Wang, H., and Wroe, C. (2004). *OWL pizzas: Practical experience of teaching owl-dl: Common errors & common patterns. In Engineering Knowledge in the Age of the Semantic Web*, pages 63-81. Springer.][7]

[Hogan, A., Harth, A., Passant, A., Decker, S., and Polleres, A. (2010). *Weaving the pedantic web. In Proceedings of the WWW2010 Workshop on Linked Data on the Web*, LDOW 2010, Raleigh, USA, April 27, 2010.][8]

[Archer, P., Goedertier, S., and Loutas, N. (2012). *D7. 1.3-study on persistent URIs, with identification of best practices and recommendations on the topic for the Mss and the EC*. PwC EU Services.][9]

[Bernes-Lee Tim. (2006). *Linked Data - Design issues*.][10]

[Heath, T. and Bizer, C. (2011). *Linked Data: Evolving the Web into a Global Data Space*. Morgan & Claypool, 1st edition.][11]

[Vatant, B. (2012). *Is your linked data vocabulary 5-star?*.][12]

[*Protege OWL Tutorial*][13]

[OOPS! common pitfalls catalogue][15]

[W3C Property Chain Inclusion][16]

[SKOS reference][17]

[Suárez-Figueroa, M.C., Gómez-Pérez, A., Villazón-Terrazas, B. (2009). *How to Write and Use the Ontology Requirements Specification Document.* Proceedings of the Confederated International Conferences, CoopIS, DOA, IS, and ODBASE 2009 on On the Move to Meaningful Internet Systems: Part II. Berlin: Springer. pp. 966-982. doi:10.1007/978-3-642-05151-7_16.][18]

[1]: https://ac.els-cdn.com/S1877042815056608/1-s2.0-S1877042815056608-main.pdf?_tid=23358f4e-6ec2-438d-9cf1-b9a483f225ab&acdnat=1520009653_d6e0957f9026bd3294065aa761477e57
[2]: https://protege.stanford.edu/publications/ontology_development/ontology101.pdf
[3]: http://oa.upm.es/6456/1/Evaluation_of_Taxonomic_K.pdf
[4]: http://dcevents.dublincore.org/index.php/IntConf/dc-2011/paper/viewFile/47/15
[5]: http://www.aifb.kit.edu/images/b/b5/OntologyEvaluation.pdf
[6]: https://www.springer.com/us/book/9783540709992
[7]: http://www.cs.man.ac.uk/~rector/papers/common_errors_ekaw_2004.pdf
[8]: http://ceur-ws.org/Vol-628/ldow2010_paper04.pdf
[9]: https://joinup.ec.europa.eu/sites/default/files/document/2013-06/Study%20-%20Study%20on%20persistent%20URIs_4.pdf
[10]: http://www.w3.org/DesignIssues/LinkedData.html
[11]: http://linkeddatabook.com/editions/1.0/
[12]: http://bvatant.blogspot.fr/2012/02/is-your-linked-data-vocabulary-5-star_9588.html
[13]: http://mowl-power.cs.man.ac.uk/protegeowltutorial/resources/ProtegeOWLTutorialP4_v1_3.pdf
[15]: http://oops.linkeddata.es/catalogue.jsp
[16]: http://www.w3.org/TR/owl2-new-features/#F8:_Property_Chain_Inclusion
[17]: https://www.w3.org/TR/2009/REC-skos-reference-20090818/
[18]: http://oa.upm.es/5474/1/INVE_MEM_2009_64393.pdf
