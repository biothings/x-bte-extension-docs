.. _x-smartapi-parameter:

x-smartapi-parameter Object
==========================

An object to hold parameter names and their corresponding values. If the value of the parameter is constant for the single-hop knowledge graph operation, use the const value in the object. If the value of the parameter is not constant and correspond to one of the inputs of the knowledge graph operation, use the notation $inputs[index], where the index refers to the index of the input in the inputs list. For example, $inputs[0] represents the first element of the inputs list.

Properties
****************************

====================  ==============  ===========================
   Properties
-----------------------------------------------------------------
Property name         Type            Description
====================  ==============  ===========================
parameterName         String          The value of the parameter.
====================  ==============  ===========================

x-smartapi-parameter example
****************************

The following example represents a x-smartapi-kgs-parameter, where the interaction_type parameter takes a constant value “gene2chemical”, whereas the value parameter corresponds to the first inputs.

.. code-block:: json

        {
            “interaction_type”: “gene2chemical”,
            “value”: “$inputs[0]”
        }

