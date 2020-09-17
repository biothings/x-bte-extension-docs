.. _x-bte-requestBody:

x-bte-requestBody Object
==========================

An object representing the request body. If the value of the requestBody parameter is constant for the single-hop knowledge graph operation, use the const value in the object. If the value of the parameter is not constant and correspond to one of the inputs of the knowledge graph operation, use the notation $inputs[index], where the index refers to the index of the input in the inputs list. For example, {inputs[0]} represents the first element of the inputs list.

Properties
****************************

====================  ==============  ===========================
   Properties
-----------------------------------------------------------------
Property name         Type            Description
====================  ==============  ===========================
parameterName         String          The value of the parameter.
====================  ==============  ===========================

x-bte-requestBody example
****************************

The following example represents a x-bte-requestBody object, where the scopes parameter takes a constant value “entrezgene”, whereas the q parameter corresponds to the first inputs.
.. code-block:: json

        {
            “q”: “{inputs[0]}”,
            
            “value”: “entrezgene”
        }


