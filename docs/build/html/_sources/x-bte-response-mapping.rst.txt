.. _x-smartapi-response-mapping:

x-smartapi-response-mapping Object
=============================

Provide one-to-one map between individual field in the API response and the corresponding concept in the Biolink model.

Properties
****************************

====================  ==============  ===========================
   Properties
-----------------------------------------------------------------
Property name         Type            Description
====================  ==============  ===========================
biolinkConceptName    String          Map between individual fie\
                                      field in API response and \
                                      corresponding concept name\
                                       in Biolink model. Nested \
                                      fields should be represent\
                                      ed using the dot notation.
====================  ==============  ===========================

x-smartapi-response-mapping example
******************************

The following example represents a x-smartapi-response-mapping object, where the nested field “go.CC.id” correspond to the Biolink concept GO, and the “go.CC.pubmed” correspond to the Biolink concept publication.
.. code-block:: json

        {
            “GO”: “go.CC.id”,
            “publication”: “go.CC.pubmed”
        }


