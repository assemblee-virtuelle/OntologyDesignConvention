# OntologyDesignConvention

Ontology design convention followed by Virtual Assembly

## Naming

* We use meaningful URI local names, in English
* We follow the CamelBack notation for class and property names: 
  * Class and individual names should start with a capital letter and should not contain spaces nor underscores, e.g. `WorkingGroup`
  * Object and data property names start with a lowercase, e.g. `isTypeOf`
  * Following words start with a capital letter
* Property names should start with an active verb, e.g. `knowsPerson`, `isKnownBy`, `hasName`

## Labeling

## Pitfalls catalogue

We follow the [OOPS! common pitfalls catalogue][4]:
* P01. **Creating polysemous elements**: An ontology element (class, object property or datatype property) whose identifier has different senses is included in the ontology to represent more than one conceptual idea or property.
* P02. **Creating synonyms as classes**: Several classes whose identifiers are synonyms are created and defined as equivalent (owl:equivalentClass) in the same namespace. This pitfall is related to the guidelines presented in [1], which explain that synonyms for the same concept do not represent different classes.
* P03. Creating the relationship "is" instead of using "rdfs:subClassOf", "rdf:type" or "owl:sameAs": The relationship "is" is created in the ontology instead of using OWL primitives for representing the subclass relationship (rdfs:subClassOf), class membership (rdf:type), or the equality between instances (owl:sameAs). When concerning a class hierarchy, this pitfall is related to the guidelines for understanding the "is-a" relation provided in [2].
* P04. **Creating unconnected ontology elements**: Ontology elements (classes, object properties and datatype properties) are created isolated, with no relation to the rest of the ontology.
* P05. **Defining wrong inverse relationships**: Two relationships are defined as inverse relations when they are not necessarily inverse.
* P06. **Including cycles in a class hierarchy**: A cycle between two classes in a hierarchy is included in the ontology. A cycle appears when some class A has a subclass (directly or indirectly) B, and at the same time B is a superclass (directly or indirectly) of A. This pitfall was first identified in [3]. Guidelines presented in [2] also provide recommendations to avoid this pitfall.
* P07. Merging different concepts in the same class: A class whose name refers to two or more different concepts is created.
* P08. Missing annotations: This pitfall consists in creating an ontology element and failing to provide human readable annotations attached to it. Consequently, ontology elements lack annotation properties that label them (e.g. rdfs:label, lemon:LexicalEntry, skos:prefLabel or skos:altLabel) or that define them (e.g. rdfs:comment or dc:description). This pitfall is related to the guidelines provided in [5].
* P09. Missing domain information: Part of the information needed for modeling the intended domain is not included in the ontology. This pitfall may be related to (a) the requirements included in the Ontology Requirement Specification Document (ORSD) that are not covered by the ontology, or (b) to the lack of knowledge that can be added to the ontology to make it more complete.
* P10. Missing disjointness: The ontology lacks disjoint axioms between classes or between properties that should be defined as disjoint. This pitfall is related with the guidelines provided in [6], [2] and [7].
* P11. Missing domain or range in properties: Object and/or datatype properties without domain or range (or none of them) are included in the ontology.
* P12. Equivalent properties not explicitly declared: The ontology lacks information about equivalent properties (owl:equivalentProperty) in the cases of duplicated relationships and/or attributes.
* P13. Inverse relationships not explicitly declared: This pitfall appears when any relationship (except for those that are defined as symmetric properties using owl:SymmetricProperty) does not have an inverse relationship (owl:inverseOf) defined within the ontology.
* P14. Misusing "owl:allValuesFrom": This pitfall consists in using the universal restriction (owl:allValuesFrom) as the default qualifier instead of the existential restriction (owl:someValuesFrom). Additional information about this pitfall is provided in [7].
* P15. Using "some not" in place of "not some": The pitfall consists in using a "some not" structure when a "not some" is required. This is due to the misplacement of the existential quantifier (owl:someValuesFrom) and the negative operator (owl:complementOf). (a) When to use a "some not" structure (DrelationshipS: ClassA): to state that there is at least one individual acting as object of the relationship "relationshipS" and such individual do not belong to class "ClassA". This implies that there must be at least one instantiation of the relationshipsS whose target does not belong to "ClassA". This does not prevent instances from ClassA acting as objects of the relationships. (b) When to use a "not some" structure ( DrelationshipS:ClassA): to state that no individuals in class "ClassA" act as objects of the relationship "relationshipS". This does not imply the existence of individuals from other classes acting as objects of the relationship. This pitfall is explained in more detail in [7].
* P16. Using a primitive class in place of a defined one: "Primitive" classes are those for which there are only necessary conditions [7]. They are described using rdfs:subClassOf. "Defined" classes are those for which there are necessary and sufficient conditions [7]. They are described using owl:equivalentClass. This pitfall implies creating a primitive class rather than a defined one in case automatic classification of individuals is intended. It should be clarified that, in general, nothing will be inferred to be subsumed under a primitive class by the classifier [7]. This pitfall is related to the open world assumption.
* P17. Overspecializing a hierarchy: The hierarchy in the ontology is specialized in such a way that the final leaves are defined as classes and these classes will not have instances. Authors in [e] provide guidelines for distinguishing between a class and an instance when modeling hierarchies.
* P18. Overspecializing the domain or range: This pitfall consists in defining a domain or range not general enough for a property, i.e, no considering all the individuals or datatypes that might be involved in such a domain or range. This pitfall is related to the guidelines provided in [2] and [7].
* P19. Defining multiple domains or ranges in properties: The domain or range (or both) of a property (relationships and attributes) is defined by stating more than one rdfs:domain or rdfs:range statements. In OWL multiple rdfs:domain or rdfs:range axioms are allowed, but they are interpreted as conjunction, being, therefore, equivalent to the construct owl:intersectionOf. This pitfall is related to the common error that appears when defining domains and ranges described in [7].
* P20. Misusing ontology annotations: The contents of some annotation properties are swapped or misused. This pitfall might affect annotation properties related to natural language information (for example, annotations for naming such as rdfs:label or for providing descriptions such as rdfs:comment). Other types of annotation could also be affected as temporal, versioning information, among others.
* P21. Using a miscellaneous class: This pitfall refers to the creation of a class with the only goal of classifying the instances that do not belong to any of its sibling classes (classes with which the miscellaneous problematic class shares a common direct ancestor).
* P22. Using different naming conventions in the ontology: The ontology elements are not named following the same convention (for example CamelCase or use of delimiters as "-" or "_") . Some notions about naming conventions are provided in [2].
* P23. Duplicating a datatype already provided by the implementation language: A class and its corresponding individuals are created to represent existing datatypes in the implementation language.
* P24. Using recursive definitions: An ontology element (a class, an object property or a datatype property) is used in its own definition. Some examples of this would be: (a) the definition of a class as the enumeration of several classes including itself; (b) the appearance of a class within its owl:equivalentClass or rdfs:subClassOf axioms; (c) the appearance of an object property in its rdfs:domain or range rdfs:range definitions; or (d) the appearance of a datatype property in its rdfs:domain definition.
* P25. Defining a relationship as inverse to itself: A relationship is defined as inverse of itself. In this case, this relationship could have been defined as owl:SymmetricProperty instead.
* P26. Defining inverse relationships for a symmetric one: A symmetric object property (owl:SymmetricProperty) is defined as inverse of another object property (using owl:inverseOf).
* P27. Defining wrong equivalent properties: Two object properties or two datatype properties are defined as equivalent, using owl:equivalentProperty, even though they do not have the same semantics.
* P28. Defining wrong symmetric relationships: A relationship is defined as symmetric, using owl:SymmetricProperty, when the relationship is not necessarily symmetric.
* P29. Defining wrong transitive relationships: A relationship is defined as transitive, using owl:TransitiveProperty, when the relationship is not necessarily transitive.
* P30. Equivalent classes not explicitly declared: This pitfall consists in missing the definition of equivalent classes (owl:equivalentClass) in case of duplicated concepts. When an ontology reuses terms from other ontologies, classes that have the same meaning should be defined as equivalent in order to benefit the interoperability between both ontologies.
* P31. Defining wrong equivalent classes: Two classes are defined as equivalent, using owl:equivalentClass, when they are not necessarily equivalent.
* P32. Several classes with the same label: Two or more classes have the same content for natural language annotations for naming, for example the rdfs:label annotation. This pitfall might involve lack of accuracy when defining terms.
* P33. Creating a property chain with just one property: The OWL 2 construct owl:propertyChainAxiom allows a property to be defined as the composition of several properties (see http://www.w3.org/TR/owl2-new-features/F8:_Property_Chain_Inclusion for additional details). In this sense, when an individual "a" is connected with an individual "b" by a chain of two or more object properties (specified in the antecedent of the chain), it is necessary to connect "a" with "b" by using the object property in the consequent of the chain. This pitfall consists in creating a property chain (owl:propertyChainAxiom) that includes only one property in the antecedent part.
* P34. Untyped class: An ontology element is used as a class without having been explicitly declared as such using the primitives owl:Class or rdfs:Class. This pitfall is related with the common problems listed in [8].
* P35. Untyped property: An ontology element is used as a property without having been explicitly declared as such using the primitives rdf:Property, owl:ObjectProperty or owl:DatatypeProperty. This pitfall is related with the common problems listed in [8].
* (*Linked Data Feature*) P36. URI contains file extension: This pitfall occurs if file extensions such as ".owl", ".rdf", ".ttl", ".n3" and ".rdfxml" are included in an ontology URI. This pitfall is related with the recommendations provided in [9].
* (*Linked Data Feature*) P37. Ontology not available on the Web: This pitfall occurs when the ontology code (OWL encoding) or its documentation (HTML document) is missing when looking up its URI. This pitfall deals with the first point from the Linked Data star system that states "On the web" ([10] and [11]). Guidelines in [12] also recommends to "Publish your vocabulary on the Web at a stable URI". This pitfall is also related to the problems listed in [8] and [5].
* P38. No OWL ontology declaration: This pitfall consists in not declaring the owl:Ontology tag, which provides the ontology metadata. The owl:Ontology tag aims at gathering metadata about a given ontology such as version information, license, provenance, creation date, and so on. It is also used to declare the inclusion of other ontologies.
* (*Linked Data Feature*) P39. Ambiguous namespace: This pitfall consists in declaring neither the ontology URI nor the xml:base namespace. If this is the case, the ontology namespace is matched to the file location. This situation is not desirable, as the location of a file might change while the ontology should remain stable, as proposed in [12].
* (*Linked Data Feature*) P40. Namespace hijacking: It refers to reusing or referring to terms from another namespace that are not defined in such namespace. This is an undesirable situation as no information can be retrieved when looking up those undefined terms. This pitfall is related to the Linked Data publishing guidelines provided in [11]: "Only define new terms in a namespace that you control" and to the guidelines provided in [5].
* P41. **No license declared**: The ontology metadata omits information about the license that applies to the ontology. One can use the licence property of the [dc/terms](http://purl.org/dc/terms/) ontology.


## References

[Ontology 101][1]

[Protege OWL Tutorial][2]

[Style Guidelines for Naming and Labeling Ontologies in the Multilingual Web][3]

[OOPS! common pitfalls catalogue][4]

[1]: https://protege.stanford.edu/publications/ontology_development/ontology101.pdf
[2]: http://mowl-power.cs.man.ac.uk/protegeowltutorial/resources/ProtegeOWLTutorialP4_v1_3.pdf
[3]: http://dcevents.dublincore.org/index.php/IntConf/dc-2011/paper/viewFile/47/15
[4]: http://oops.linkeddata.es/catalogue.jsp
