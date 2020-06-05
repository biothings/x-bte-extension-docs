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
inputs                [x-bte-kgs-no\  Specifies the list of inpu\
                      de Object]      ts for the single-hop know\
                                      ledge graph retrieval oper\
                                      ation, including the input\
                                      semantic type and input i\
                                      dentifier type.                         
outputs               [x-bte-kgs-no\   Specifies the list of inpu\
                      de Object]      ts for the single-hop know\
                                      ledge graph retrieval oper\
                                      ation, including the input\
                                      semantic type and input i\
                                      dentifier type.

predicate             String          Specifies the predicate fo\
                                      r the kgs operation, in ot\
                                      her words, the relationshi\
                                      p between the inputs and o\
                                      utputs.

source                String          Specifies the source datab\
                                      ase which provides the ass\
                                      ociation.

parameters            x-bte-paramet\  An object to hold paramete\
                      er              r names and their correspo\
                                      nding values. If the param\
                                      eter corresponds to one of\
                                       the inputs, should use th\
                                      e following notation $inpu\
                                      ts[index]. For example, $i\
                                      nputs[0] means this parame\
                                      ter correspond to the firs\
                                      t element of the inputs.
                      

requestBody           x-bte-request\  An object representing the\
                      Body             request body. If a parame\
                                      ter corresponds to one of \
                                      the inputs, should use the\
                                       following notation $input\
                                      s[index]. For example, $in\
                                      puts[0] means this paramet\
                                      er correspond to the first\
                                       element of the inputs.
                      

supportBatch          Boolean         Indicate whether the opera\
                                      tion support batch query.

inputSeparators       String          Describe the operator used\
                                       to separate inputs in a b\
                                      atch query. Only need to s\
                                      pecify when supportBatch i\
                                      s True. Default value is “,”.

responseMapping       x-bte-response  Provide one-to-one map bet\
                      -mapping Obje\  ween individual field in t\
                      t               he API response and the co\
                                      rresponding concept in the\
                                       biolink model.
                      
                      
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
