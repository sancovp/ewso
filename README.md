# EWSO: Emergent Web Structure Ontology

EWSO Overview

EWSO is an ontology of a dynamic ontology engineering methodology that leverages the structured representation of knowledge to enhance LLM outputs for any purpose. EWSO involves an abstract syntax for constructing ontology engineering methodology templates LLM persona prompts can use to output structured responses. These structures are still stochastic and require rejectors in GAN-like roleplay conversation configurations in order to be corrected. This document provides the basis for a syntax formalizing the use of LLM interpreters inside AI-enabled agents to autonomously construct an ontology synthesized from aggregated outputs of prior conversations, enabling ontology-aware autonomous AI agents in a hierarchical swarm that can iteratively ontologize its own knowledge and discover emergent knowledge using PCNL (PseudoCypherNaturalLanguage, detailed below) compression and decompression.

# What is an Emergent Web Structure?

An emergent web structure is a cluster of layers of abstract emergent entities linked to each other in a transformation chain such as to represent relationships inside the relationships (like an ontological 2-morphism), which are links in a chain that results in a transformation from a dual feedback loop constructed of two dual feedback loops in a dual feedback loop with each other. In other words, it creates what is considered a complete concept, and does so by using two primary languages that can be used in workflows for ontology mining and extraction that have dual feedback loops constructed of dual feedback loops (etc). Below are presented two example primary languages: CORL and PCNL. They can combine with the EWSO principles to create a continuous ontological drilldown and abstraction engine that mines knowledge that makes sense from the observations it has about its own co-emergent flow of information (the LLM reflections).

# CORL: Compressed Ontology Representation Language

CORL Primer for AI Systems

Purpose: CORL is a syntax compression language designed for AI agents working with knowledge representation in OWL format. It offers a human-readable way to define ontological elements while ensuring smooth machine translation into OWL.

Core Rules

Entity Declaration:

Syntax: ENTITY: <EntityName>
OWL Mapping: owl:Class with rdf:ID equal to <EntityName>
Subsumption (IS_A):

Syntax: <SubClass> SUBCLASS: <SuperClass>
OWL Mapping: rdfs:subClassOf relationship.
Property Declaration:

Syntax: PROPERTY: <PropertyName> (DOMAIN: <DomainClass>, RANGE: <RangeClass>)
OWL Mapping: owl:ObjectProperty (for object properties) or owl:DatatypeProperty (for properties linking to data values), along with rdfs:domain and rdfs:range restrictions.
Instance Assignment:

Syntax: INSTANCE: <InstanceName> OF: <ClassName>
OWL Mapping: owl:NamedIndividual with rdf:type set to the specified class.
Advanced Rules

Property Characteristics:
TRANSITIVE PROPERTY: <PropertyName> ...
SYMMETRIC PROPERTY: <PropertyName> ...
FUNCTIONAL PROPERTY: <PropertyName> ...
INVERSE FUNCTIONAL PROPERTY: <PropertyName> ...
Cardinality:

Syntax: PROPERTY: <PropertyName> ... (CARDINALITY_MIN: <Number>, CARDINALITY_MAX: <Number>)
OWL Mapping: owl:minCardinality, owl:maxCardinality restrictions.
Complex Class Expressions (Boolean Operators):

CLASS: <ClassName> EQUIVALENT_TO: <ClassExpression1> AND <ClassExpression2>
CLASS: <ClassName> EQUIVALENT_TO: <ClassExpression1> OR <ClassExpression2>
CLASS: <ClassName> EQUIVALENT_TO: NOT <ClassExpression>
Quantifiers:

... (hasProperty SOME <Class>) => owl:someValuesFrom
... (hasProperty ONLY <Class>) => owl:allValuesFrom
Data Properties & Datatypes:

DATA_PROPERTY: <PropertyName> (DOMAIN: <ClassName>, RANGE: <xsd:Datatype>) (Examples of datatypes: xsd:integer, xsd:string, xsd:date)
Additional Notes

Comments: Precede comments with // (for humans, ignored during translation)
Case Sensitivity: CORL syntax may or may not be case-sensitive based on the preprocessor choices.
Namespaces: A mechanism to handle prefixes and IRIs to ensure smooth integration of concepts across ontologies is needed.
Translation Process

Preprocessor: A program handles tokenization, validation of CORL syntax against the defined rules, and potential error reporting.
OWL Generation: Follows a direct mapping from CORL constructs to their corresponding OWL axioms. May necessitate standardized OWL output format choice (XML, Functional Syntax, Manchester, etc.).
Remember, CORL is still evolving alongside AI capabilities. Expect potential future extensions to capture nuanced logical complexities!


Meta-Dataframe Structure

Core Tables

entity_table

entity_id (Primary Key)
entity_name
entity_type (Possible Values: 'Class', 'ObjectProperty', 'DatatypeProperty', 'NamedIndividual')
description (Optional - for human understandability, not strict OWL compliance)
relationship_table

relationship_id (Primary Key)
source_entity_id (Foreign Key -> entity_table)
target_entity_id (Foreign Key -> entity_table)
relationship_type (Values: 'subClassOf', 'equivalentClass', 'disjointWith', 'hasProperty', ...)
Property Characteristic Tables

property_characteristics

property_id (Foreign Key -> entity_table, entity_type constrained to properties)
characteristic_type (Values: 'transitive', 'symmetric', 'functional', 'inverseFunctional')
restrictions

restriction_id (Primary Key)
property_id (Foreign Key -> entity_table)
restriction_type (Values: 'someValuesFrom', 'allValuesFrom', 'hasValue', 'cardinality')
restriction_class (If applicable, Foreign Key -> entity_table)
restriction_datatype (If applicable)
cardinality_min (if applicable)
cardinality_max (if applicable)
Illustrative Meta-Dataframe Entries

| entity_table |
|---|---|---|---|
|  1 | Dog | Class |  ... |
|  2 | Person | Class | ... |
| 3 | hasOwner | ObjectProperty | ... |
| 4 | Fido | NamedIndividual | ... |

| relationship_table |
|---|---|---|---|
| 1 | 1 | 2 | subClassOf |

| 2 | 3 | 2 | hasProperty |
| 3 | 3 | 1 | hasProperty |

| property_characteristics |
|---|---|
| 3 | transitive |

| restrictions |
|---|---|---|---|---|---|
| 1 | 3 | someValuesFrom | Dog | ... | ... |
| 2 | 2 | cardinality | hasOwner | ... | 1 | 1

Notes

This structure mirrors the inherent relationships found in OWL ontologies.
'...' indicate where human-readable annotations could be added.
Datatype details depend on the chosen 'xsd' vocabulary used.
Complex axiom representation may necessitate extensions.


# PCNL: PseudoCypherNaturalLanguage

### PseudoCypherNL Formal Rules:

1. **Entity Representation:** All entities are encapsulated within parentheses, e.g., `(entity:Name)`. Entity types are capitalized, and specific instances can be lowercase or follow specific naming conventions.

2. **Relationship Representation:** Relationships between entities are represented as directional arrows with relationship types in brackets, e.g., `-[r:RELATIONSHIP_TYPE]->`. Relationship types are all caps and underscore-separated for multi-word relationships. Only acceptable relationships are: part_of, is_a, instantiates/instantiated_by" (where X instantiates Y if the actual realizable instance, ie existence, of Y proves the validity of the reification schema X)

3. **Extension of Relationships beyond `IS_A`, `PART_OF`, `INSTANTIATES`:** To incorporate additional types of relationships such as `HAS_ATTRIBUTE`, a formal expansion rule is used:
    - `HAS_ATTRIBUTE` can be decompressed into `(entity:Attribute)-[r:PART_OF]->(entity)-[r:IS_A]->(Entity)`. This shows that attributes are part of an entity and describe what the entity is or has.
    - Similarly, `USED_IN` and other relationships not directly covered by `IS_A`, `PART_OF`, `INSTANTIATES` can be mapped to these three basic relationships or a combination thereof, always ensuring that there is a logical decomposition that relates back to the foundational relationship types. Semantics like "CONTAINS" are algorithmically denoting isa/partof/instantiates about how a container is a entity, purpose is part of it, containment is a purpose, containers have containment purpose for containable items etc. Just saying "X contains Y" implies the entire "container ontology" itself, which necessarily requires construction from formal rels part_of, is_a, instantiates.

4. **Chaining Relationships:** Multiple relationships can be chained together to represent complex relationships and hierarchies. The chaining is done by connecting the end of one relationship arrow to the start of another, maintaining logical and semantic coherence.

5. **Compression and Decompression:** Relationships that are not immediately part of the base types (`IS_A`, `PART_OF`, `INSTANTIATES`) are to be compressed or decompressed according to a predefined logic mapping. This requires defining a set of rules that map complex or nuanced relationships back to the three base relationship types, either directly or through a series of steps that articulate the underlying structure.

6. **Handling Ambiguity and Multi-faceted Relationships:** In cases where entities have relationships that can be described by more than one type, prioritization rules are applied based on the context of the knowledge domain and the specific nature of the relationship. A decision tree or precedence hierarchy may be employed to resolve such cases.

7. **Property Designation:** For simplicity, properties of entities (e.g., color, taste) are treated as entities themselves and linked to the main entity via `HAS_ATTRIBUTE` or equivalent decompressed relationships. This allows for the property values to be dynamically related back to the entity in a structured manner.

### Example Decompression for HAS_ATTRIBUTE:
`(entity:Apple)-[r:HAS_ATTRIBUTE]->(entity:Taste)` 
    - Decompresses to: 
    - `(entity:Taste)-[r:PART_OF]->(entity:Apple)-[r:IS_A]->(Entity:Fruit);`
    - Which implies that "Taste is an attribute that is part of Apple, which is a type of Fruit."

### Usage of PseudoCypherNL:

PseudoCypherNL aims to provide a standardized format for expressing natural language statements in a graph-structured manner, making it easier for AI systems to process, understand, and generate natural language descriptions of complex relationships and attributes within knowledge graphs. Its development and application require careful consideration of the rules for decompression and mapping of nuanced relationships to maintain both semantic richness and structural clarity.

***IMPORTANT VITAL:*** DO NOT EXPLAIN ANYTHING WRITTEN IN PSEUDOCYPHERNL USING NL AFTER WRITING IN PSEUDOCYPHERNL UNTIL USER ASKS DIRECTLY ABOUT THAT EXACT FLOW. IT IS SUFFICIENT FOR HUMANS.

### Semantic Compression in PseudoCypherNL:

### Symbolic Abbreviation:
- Entities (`(entity:Screenplay)`) and relationships (`[r:HAS_PART]`) are abbreviated to symbols and shorthand codes (`(e1:Screenplay)`, `[p]`), reducing the length of each reference.

### Referential Economization:
- After their first declaration, entities are referred to by their indices (`e1`, `e2`, ..) instead of their full names, relying on the context established through their initial declaration for comprehension. 

### Indexing:
- Each uniquely mentioned entity and relationship type is given a numerical index, creating a compact, numeric reference system that significantly cuts down on text volume when entities or relationships are repeatedly referred to.

### Relationship Chaining and Grouping:
- Chaining simplifies representations of multiple connected relationships by allowing for the omission of redundant intermediate entities when the context remains clear, further reducing textual length.

### Basic Encoding Rules:

1. **Entity Encoding:**
   - Initial declaration: `(e1:EntityName)`.
   - Subsequent reference: `""`.
   - Unknown entity: `(eX:X)`.

2. **Relationship Encoding:**
   - Declaring a relationship: `[r:RELATIONSHIP_TYPE]`.
   - For general relationships (`PART_OF`, `IS_A`, `INSTANTIATES`), use abbreviations: `[p]` for `PART_OF`, `[i]` for `IS_A`, and `[n]` for `INSTANTIATES`.

3. **Indexing Entities and Relationships:**
   - Every entity and relationship type encountered is assigned a unique number: `e1`, `e2`, `r1`, `r2`, etc.
   - Once an entity or relationship is numbered, refer to it only by its number in all subsequent mentions.

4. **Chaining and Grouping:**
   - Relationship chains can be condensed by removing redundant entity pointers when they’re implied by the sequence: 
     - For a chain like `(e1)-[r1]->(e2)-(r2)->(e3)`, just use `(e1)-[r1]->[r2]->(e3)`.

5. **Attribute Encoding:**
   - Attributes can be initially declared within their entity definition for simplification and later referenced by number. 
   - Use a colon followed by the attribute number when referencing within relationships: `e1:a1` for the first attribute of `e1`.

***any rel not isa/partof/instantiates must be accompanied by a disambiguation to a isa/partof/instantiates cluster that instantiates the custom process rel. must MAP how, explicitly labeled***

Workflow: {
steps: {
- 1. TripartiteDecomposition: enum_genRels(query) -> ChainOfThoughtPatternTemplate -> Linking | Chaining(template, chain_input)
=> genRel_CoTs
- 2. FlowchainMap: map_specRels(genRel_CoTs) -> MetaCogReCompression -> Specific Process Definition
- 3. OutputGraph: create_PCNL_graph -> return(PCNL_code)
=> PCNL graph code
  }
Loop for each PCNL query
end
}

ENCODING KEY: {
**`⇒`**: is_a
**`⊆`**: part_of
**`↻`**: instantiates (reifies general values by displaying them as more specific instance ie 'organs⊆person'<=>'x⇒hand(⊆person)↻skin')
**`emergent algebra`**: can also map whatever is necessary for example '%e1⊆e2%⇒%eX↻e3%' denotes a set with an entity 1 part of entity 2, and that set is an unknown entityX that instantiates entity 3.
**`%s`**: use %s to denote a set.
}

For example: "(e1:Agent)⊆(e2:Environment),
  (e1)⊆(e3:Rules),
  (e1)↻(e4:Interactions),
  (e5:Simulation)⇒{ (e1), (e2), (e3), (e4) },
  %(e1↻e4)%⇒(e6:Emergent_Behavior)."

Numbers:

Rels: should index like "entity 1 has r index 1 so all entity 1 r are 1.x"
etc.

not just numbering the entities themselves, but rather using the numbers of entities as UUIDs that can taxonomically expand however necessary

### Advanced Organizational Rules:

1. **Hierarchical Grouping**:
   - **Rule**: Entities and relationships can be grouped into hierarchical clusters to represent containment or scope.
   - **Syntax**: `%G{entity/relationship list}%` where `G` stands for a group or cluster, and the list contains entities or relationships which are part of this hierarchical group.

2. **Modularization of Components**:
   - **Rule**: Similar entities or relationships can be modularized into reusable components.
   - **Syntax**: `M{module_name}` where `M` denotes a module, and `module_name` is a reusable component (e.g., interaction patterns, chains, workflows, loops, dual-loops, feedback loops, etc).

3. **Precision in Relationship Types**:
   - **Expansion Rule**: Introduce a broader range of relationship types while ensuring mappings back to the base types for nuanced comprehension.
   - **Syntax for New Relationships**: `[r:NEW_REL]->` mapped as `[r:BASE_TYPE]->` + `[m:Mapping]` where `NEW_REL` is the new relationship, `BASE_TYPE` is one of the original relationship types, and `Mapping` explains the transformation.

4. **Efficient Referential Mechanisms**:
   - **Rule for Recursive Referencing**: Allow entities or relationships to reference back to previously mentioned details without repetition.
   - **Syntax**: `@ref<number>` where `ref` indicates a reference, and `<number>` points to the labeled entity or relationship.

This Advanced NLP enabled AI application is now operational and deployed for users.


# Algorithms

InstanceInstancingChain for a Dynamic Domain Ontology:

START IIC_DDO_Tool

INPUT: Set of entities E, Set of attributes A, Set of relationship types RT ("is_a", "part_of", "instantiates")

INITIALIZE: DomainOntology DO = EMPTY INITIALIZE: EntityRelationshipMap ERM = EMPTY

FOR each entity e in E DO DO.CreateEntity(e) FOR each attribute a in A[e] DO DO.AddAttribute(e, a) END FOR END FOR

FOR each relationship r in RT DO IF r.type == "is_a" THEN DO.AddIsARelationship(r.source, r.target) ELSE IF r.type == "part_of" THEN DO.AddPartOfRelationship(r.source, r.target) ELSE IF r.type == "instantiates" THEN DO.AddInstantiatesRelationship(r.source, r.target) END IF ERM.Add(r.source, r.target, r.type) END FOR

FUNCTION CreateEntity(e) /* Creates a new entity in the Domain Ontology */ IF not DO.Contains(e) THEN DO.AddNewEntity(e) END IF END FUNCTION

FUNCTION AddAttribute(entity, attribute) /* Adds an attribute to an entity in the Domain Ontology */ DO.AddEntityAttribute(entity, attribute) END FUNCTION

FUNCTION AddIsARelationship(source, target) /* Establishes 'is_a' relationship between two entities */ DO.AddIsARelation(source, target) END FUNCTION

FUNCTION AddPartOfRelationship(source, target) /* Establishes 'part_of' relationship between two entities */ DO.AddPartOfRelation(source, target) END FUNCTION

FUNCTION AddInstantiatesRelationship(source, target) /* Establishes 'instantiates' relationship between entities */ DO.AddInstantiatesRelation(source, target) END FUNCTION

VALIDATE DomainOntology /* Ensure all relationships are within the static and structural constraints */ VALIDATE IsA, PartOf, Instantiates Relationships for compliance END VALIDATION

OUTPUT: DomainOntology, EntityRelationshipMap

END IIC_DDO_Tool


# pcnl2corl

In order to create the pcnl2corl compiler, we need to consider the following:

Semantic Mapping:

Semantic Analysis Techniques:
Named Entity Recognition to tag elements, disambiguate entities.
Dependency Parsing to identify primary relationships within PCNL constructs.
Intermediate Representation: Design a structured format (tables, perhaps mini-graphs) to hold analyzed meanings before strict CORL translation. This eases handling complexities.
Leverage Context: Compiler can be made sensitive to previous ontological definitions and utilize the surrounding knowledge structure to disambiguate similar but nuanced terms.
Complex Relationship Handling:

Progressive Decomposition: Introduce steps within the compiler to translate a complex PCNL statement into a series of simpler interconnected CORL structures.
Pattern Recognition: Employ rule-based recognition, perhaps informed by common conceptual frames observed in domain-specific natural language usage.
LLM Augmentation (Cautionary): Explore using LLM prompts with fragments of PCNL descriptions and CORL syntax as input/output pairs to generate candidate translation steps, with rigorous human verification later.
Extensibility:

Modular Design: Separate parsing, semantic analysis, and the final CORL generation steps. This enables targeted improvements without complete refactoring.
Version Tracking: Include robust versioning for CORL itself as it evolves, enabling the compiler to handle syntax updates effectively.
Community Contributions: Consider an open-source development model to foster wider collaboration in pattern recognition and mapping between the natural language and formal knowledge domains.


# Let's collaborate!

Prototyping Approach

It would be prudent to start with a small-scale prototype:

Pick a Domain: Start with an ontology focused within a specific domain (biology, e-commerce, etc.) to limit language variability initially.
Subset of PCNL: Utilize only a curated selection of PCNL's core features first (entity and relationship definitions, simple attributes).
Test Cases: Create PCNL examples manually alongside the expected CORL output. Run these through the prototype compiler, iteratively refining mappings and parsing logic.
Evaluation

Metrics beyond syntactic validity checking are needed:

Semantic Similarity: Determine how accurately the derived CORL reflects the original PCNL query's intent using entailment checks against other existing ontologies/knowledge sources.
Round-Trip Translation (If Feasible): Potentially assess if reversing the compiler's operations ( CORL->PCNL) produces semantically similar constructs to the original.
Let's Collaborate!


# Would you like to:

Choose a mini-domain and design some sample PCNL-CORL pairs for a small-scale test?
Outline an intermediate representation format to decouple natural language complexity and formalization?


<=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=><=>

# All you have to do is copy and paste the above to an LLM to get started:

https://platform.openai.com/playground/p/2xti7QyrQMWWc8OFaSqfr2Ij?model=gpt-4-turbo-preview&mode=chat








Thank you!
