.. x-smartapi extension doc documentation master file, created by
   sphinx-quickstart on Fri Jun  5 11:28:45 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Working with Translator Knowledge Graph Operation extension
=======================================================================


************
Introduction
************
The goal of this extension is to facilitate the automatic retrieval of single-hop knowledge graph data in the format of subject-predicate-object (e.g. ChemicalSubstance – treats – Disease) from APIs by intelligent agents, such as `BioThings Explorer <https://github.com/biothings/biothings_explorer/>`_. This is achieved through documenting single-hop knowledge graph retrieval operations that an individual `OpenAPI operation <https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#operation-object>`_ can perform. The knowledge graph retrieval operation should be defined using the `BioLink Data Model <https://biolink.github.io/biolink-model/>`_, e.g. each input/output node should be categorized using Biolink classes and ID prefixes, edges should be labeled using valid Biolink relationship types.


*****************************
Topics
*****************************
.. toctree::
   :maxdepth: 1

   x-smartapi-kgs-operations
   x-smartapi-kgs-operation
   x-smartapi-kgs-node
   x-smartapi-parameter
   x-smartapi-requestBody
   x-smartapi-response-mapping


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
