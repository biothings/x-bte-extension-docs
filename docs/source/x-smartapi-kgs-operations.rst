.. _x-smartapi-kgs-operations:

x-smartapi-kgs-operations Object
===========================

Describe list of single-hop knowledge graph retrieval operations that a single OpenAPI operation can perform.


====================  ==============  ===========================
   Properties
-----------------------------------------------------------------
Property name         Type            Description
====================  ==============  ===========================
x-smartapi-kgs-operations  [x-smartapi-kgs-op   A list of single-hop 
                      eration Object  knowledge graph retrieval
                      |Reference      operations that an OpenAPI
                      Object]         operation can perform. The
                                      list can use the Reference
                                      Object to link to x-smartapi-kgs
                                      operation defined in 
                                      components
====================  ==============  ===========================

x-smartapi-kgs-operations example
****************************

The following example defines two x-smartapi-kgs-operations (ChemicalSubstance – physically_interacts_with – Gene && Gene – physically_interacts_with -- ChemicalSubstance) associated with the GET operation of the /interactions endpoint.


.. code-block:: json

    {
        "interactions.json": {
            "get": {
                "parameters": [
                    {
                        "in": "query",
                        "name": "drugs"
                    },
                    {
                        "in": "query",
                        "name": "genes
                    }
                ],
                "x-smartapi-kgs-operations": [
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
                    },
                    {
                        "inputs": [
                            {
                                "id": "biolink:NCBIGene",
                                "semantic": "biolink:Gene"
                            }
                        ],
                        "outputs": [
                            {
                                "id": "biolink:CHEMBL.COMPOUND",
                                "semantic": "biolink:ChemicalSubstance"
                            }
                        ],     
                        "parameters": {
                            "genes": "$inputs[0]"
                        },
                        "predicate": "biolink:physically_interacts_with",
                        "supportBatch": False,
                        "responseMapping": {
                            "CHEMBL.COMPOUND": "matchedTerms.interactions.drugChemblId",
                            "publication": "matchedTerms.interactions.pmids"
                        }
                    }
                ]
            }
        }
    }