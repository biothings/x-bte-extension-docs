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
                                       
useTemplating         Boolean         Indicate whether to use nu\
                                      njucks templating.       
                                      
templateImputs        Object          An object in which to delc\
                                      are any static variables t\
                                      o be used by templating.
                                      
requestBodyType        String         Set to 'object' to parse t\
                                      emplated request body as JSON.                     
                      
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
                    "drugs": "{inputs[0]}"
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
 
 Templated x-bte operations query
 ********************************
 
To use templated queries, first enable query templating with the property :code:`useTemplating: true`. :code:`queryInputs` takes the place of :code:`{inputs[0]}` to reference input IDs, while other variables, delcared in the annotation under :code:`templateInputs`, may be referenced.

Any part of :code:`parameters` or :code:`requestBody.body` will be rendered through Nunjucks, meaning that any Nunjucks recognized templating will be applied. Templates are rendered per-property of :code:`parameters` and :code:`requestBody.body`, unless :code:`requestBodyType: object` is set, in which case the entirety of :code:`body` is expected to be a string and will be parsed as JSON into an object after being rendered. This, in concert with :code:`header: application/json` allows JSON to be send as the body of a POST request.

A number of custom `filter functions <https://mozilla.github.io/nunjucks/templating.html#filters>`_ have been defined, as listed below:

- :code:`substr(begin, end)`: slice a string
- :code:`addPrefix(prefix, delim)`: add a prefix, with :code:`delim` between prefix and string defaulting to :code:`:`
- :code:`rmPrefix(delim)`: remove a prefix by splitting by delimiter and removing first string, with delimiter defaulting to :code:`:`. If no prefix is found, the string is returned.
- :code:`replPrefix(prefix, delim)` replace a prefix by using :code:`rmPrefix` and :code:`addPrefix` in order, using same delimiter.
- :code:`wrap(start, end)`: wrap the input string between :code:`start` and :code:`end`, or :code:`start` and :code:`start` if end is not provided.
- :code:`joinSafe(delim)`: Join the entries of an array by :code:`delim`, or :code:`,` if none is provided. If a string is provided instead of an array, the string is simply returned.

Templated Example
*****************

The following example defines one x-bte-kgs-operation in yaml format.

.. code-block:: yaml

    disease-gene-templated:
      - useTemplating: true ## flag to say templating is being used below
        inputs:
          - id: UMLS
            semantic: Disease
        templateInputs:
          desiredField: disgenet.genes_related_to_disease
        requestBodyType: object
        requestBody:
          body:
            requestBody:
              body: >-
                {
                  "q": [
                    {% for input in queryInputs %}
                      ["{{input}}", "Definitive"]{% if loop.revindex0 %},{% endif %}
                    {% endfor %}
                  ],
                  "scopes": ["entrezgene", "clingen.clinical_validity.classification"]
                }
          header: application/json
        parameters:
          fields: "{{ desiredField }}"
        outputs:
          - id: NCBIGene
            semantic: Gene
        predicate: related_to
        source: "infores:disgenet"
        response_mapping:
          "$ref": "#/components/x-bte-response-mapping/disease-gene"

:code:`useTemplating` Enables templating. :code:`templateInputs` allows us to define static variables to use in our templates. :code:`requestBodyType` states that the request body will be parsed as JSON, while the header allows the request to be sent as such. :code:`parameters.fields` makes use of our static veriable: :code:`fields` will evaluate to the value of :code:`desiredField`.

Our template generates a Biothings-compatible batch query in JSON format. if :code:`queryInputs` were an array such as :code:`['aaa', 'bbb']`, the request body would render as such:

.. code-block:: json

    {
        "q": [
            ["aaa", "Definitive"],
            ["bbb", "Definitve"]
        ],
        "scopes": ["entrezgene", "clingen.clinical_validity.classification"]
    }


We make use of a `for loop <https://mozilla.github.io/nunjucks/templating.html#for>`_ to dynamically create each :code:`[input, Definitive]` array, and an `if statement <https://mozilla.github.io/nunjucks/templating.html#if>`_ checking how many iterations until the final (0-indexed) in order to avoid inserting a comma at the end of the array of arrays.
