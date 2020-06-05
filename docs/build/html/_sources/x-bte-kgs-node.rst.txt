.. _x-bte-kgs-node:

x-bte-kgs-node Object
==========================

Describe a node in a meta knowledge graph. Used to describe the inputs and outputs of a single-hop knowledge graph retrieval operation.

Properties
****************************

====================  ==============  ===========================
   Properties
-----------------------------------------------------------------
Property name         Type            Description
====================  ==============  ===========================
id                    String          The identifier used to rep\
                                      resent the node, e.g. NCBI\
                                      Gene. The value should be \
                                      prefixed with "biolink:".
semantic              String          The semantic type used to \
                                      represent the node, e.g. G\
                                      ene. The value should be p\
                                      refixed with "biolink:".
====================  ==============  ===========================

x-bte-kgs-node example
****************************

The following example represents a x-bte-kgs-node object with identifier as “NCBIGene” from the biolink model and semantic type as “Gene” from the biolink model.

.. code-block:: json

        {
            “id”: “biolink:NCBIGene”,
            “semantic”: “biolink:Gene”
        }
