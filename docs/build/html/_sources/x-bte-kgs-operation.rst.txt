.. _x-bte-kgs-operation:

x-bte-kgs-operation Object
==========================

Describe a single-hop knowledge graph retrieval operation.

The x-bte-kgs-operation object contains 3 parts:

* Single-hop knowledge graph association

    Metadata information describing the knowledge retrieval operation, including the input, output, predicate and source. One kgs-operation may have more than one inputs or outputs, but it should have exactly one predicate to capture the relationship between the input(s) and output(s).

* API Operation

    Describe how to structure the API call in order to retrieve the knowledge, including request body and parameters. Other relevant information to perform API query, e.g. server URL, path, HTTP method can be inferred from the server object and path object.

* Response Mapping
    
    Map individual fields in the API response to their corresponding concepts in the Biolink model.

Properties
****************************

====================  ==============  ===========================
   Properties
-----------------------------------------------------------------
Property name         Type            Description
====================  ==============  ===========================
inputs                [x-bte-kgs-no\  A list of single-hop 
                      de Object]      knowledge graph retrieval
                                      operations that an OpenAPI
                                      operation can perform. The
                                      list can use the Reference
                                      Object to link to x-bte-kgs
                                      operation defined in 
                                      components
outputs               [x-bte-kgs-n\   A list of single-hop 
                      ode Object]      knowledge graph retrieval
                                      operations that an OpenAPI
                                      operation can perform. The
                                      list can use the Reference
                                      Object to link to x-bte-kgs
                                      operation defined in 
                                      components
predicate             String

source                String

parameters            x-bte-paramet\
                      er

requestBody           x-bte-request\
                      Body

supportBatch          Boolean

inputSeparators       String

responseMapping       x-bte-response
                      -mapping
                      Object
====================  ==============  ===========================

x-bte-kgs-operations example
****************************

The following example defines one x-bte-kgs-operation (ChemicalSubstance – physically_interacts_with – Gene).


.. code-block:: json

    {
        "x-bte-kgs-operations": [
            {
                "inputs": [
                    {
                        "id": "biolink:CHEMBL.COMPOUND",
                        "semantic": "biolink:ChemicalSubstance"
                    }
                ],
                "outputs": [
                    {
                        "id": "biolink:NCBIGene",
                        "semantic": "biolink:Gene"
                    }
                ],
                "parameters": {
                    "drugs": "$inputs[0]"
                },
                "predicate": "biolink:physically_interacts_with",
                "supportBatch": False,
                "responseMapping": {
                    "NCBIGene": "matchedTerms.interactions.geneEntrezId",
                    "publication": "matchedTerms.interactions.pmids"
                }
            }
        ]
    }
