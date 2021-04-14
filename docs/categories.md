Most moved to:

https://ioticlabs.atlassian.net/wiki/spaces/DT/pages/208601108/Categories

# Categories

Categories are used to organize items described in the Iotic Knowledge Graph.
Such items can be digital twins, their feeds or other entities.
By adding a category to a descriptions of an entity, it is easier to search for.

## Search Usage

Example: weather stations around Cambridge.

A SPARQL query:

```ttl
    PREFIX iotb:    <http://purl.org/net/iotic-labs#>
    PREFIX cat:     <http://data.iotics.com/category/>
    # Example - category items for location.
    PREFIX loc:     <http://data.iotics.com/category/location/>

    SELECT * { 
       # Look for a match to both "cat:Weather" and "loc:Cambridge"
       ?entity iotb:category cat:Weather ;
               iotb:category loc:Cambridge ;
    }
```

## Definition

where the `cat:Weather` category is defined as:

```ttl
cat:Weather        rdf:type  skos:Concept ;
    skos:prefLabel "Weather" ;
    rdfs:label     "Weather";
    .
```

and `loc:Cambridge`:

```ttl
loc:Cambridge      rdf:type  skos:Concept ;
    skos:prefLabel "Cambridge" ;
    rdfs:label     "Cambridge"
    .
```

Categories do not have to be in the "Iotics" namespace or sub-namespace.

## SKOS

Categories are [SKOS](https://www.w3.org/TR/skos-primer/), the "Simple Knowledge
Organization System". An item is in a category just by the fact that it has
property `iotb:category` giving the category. An item can have several
categories.

The SKOS vocabulary:

```ttl
PREFIX skos:    <http://www.w3.org/2004/02/skos/core#>
```

```ttl
<did:....>
        a                   iotb:Entity ;
        iotb:advertises     ...
        iotb:category       category:Weather ;       ## Category
        iotb:category       loc:Cambridge ;          ## Category
        .
```

Categories can be structured into a hierarchy with SKOS "broader"/ "narrower".

"Concept A has broader concept concept B."

```ttl
ex:mammals rdf:type skos:Concept;
  skos:broader ex:animals.
```

(It is not "Concept A is broader than concept B.")

Categories do not have to allocated by Iotics, nor exclusively use `http://data.iotics.com/category/`.

```ttl
PREFIX ex: <http://example/>
ex:GoodSource      rdf:type  skos:Concept ;
    skos:prefLabel "Good data"
    .
```

Data sources can provide their own categories and concept schemas.
