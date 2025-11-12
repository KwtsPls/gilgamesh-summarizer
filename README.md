# Gilgamesh Summarization Tool

# Overview

Gilgamehs is an LLM-based ontology summarizaton. Developed as a pipeline for optimization in Knowledge Graph Question Answering tasks, to reduce a KG's complexity and prune possible multi-hop questions, further increasing the QA system accuracy. This pipeline utilizes the capabilities of LLMs to create concise summaries and locate possible redundant key-value patterns in the target KG. Implemented as a PyPI package, this pipeline can be deployed to summarize knowledge graphs as an optimization for question answering tasks. 

# Install

__Basic requirements:__

- Python version greater or equal to **3.10**.

      pip install gilgamesh-summarizer

# 🔍 Basic Usage: Creating summaries based on Key-Value Pairs

Currently, the major functionality of our tool is in creating ontology summaries through discovering and condensing key-value pair formations in Knowledge Graph ontologies.

Our pipline initially:

1. Parses ontology file and knowledge graph data
2. Create clusters from initial knowledge graph data
3. Cluster numbers can be reduced by removing nodes with high degrees
4. Clusters can be further reduced in size by spliting and re-clustering large clusers (powered by PyJedAI)

```python
from gilgamesh_summarizer.KnowledgeGraph import KnowledgeGraph

kg = KnowledgeGraph(path_to_rdf_data,path_to_ontology)

clusters, triples_dict = kg.create_clusters(prune_top_nodes=16,max_cluster_size=200)
clusters
```

And provides an unsloth based fine-tuned model locates meaningful information that can be used to create summaries

```python
from gilgamesh_summarizer.Summarizer import Summarizer

classifier = Summarizer(kg)
results = classifier.classify_clusters(clusters, triples_dict)
```

# Notebook Demo

An end to end example of the tool's summarization pipeline is presented here: [Notebook](https://colab.research.google.com/drive/1Ti1-wZOoofBinBLMEDKrTipDonNBHIwI?usp=sharing)

# License

Released under the Apache-2.0 license (see [LICENSE.txt](https://github.com/AI-team-UoA/pyJedAI/blob/main/LICENSE)).

Copyright © 2025 AI-Team, University of Athens

<div align="center">
    <hr>
    <br>
    <a href="https://stelar-project.eu">
        <img align="center" src="https://stelar-project.eu/wp-content/uploads/2022/08/Logo-Stelar-1-f.png" width=180/>
    </a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <a href="https://ec.europa.eu/info/index_en">
        <img align="center" src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b7/Flag_of_Europe.svg/1200px-Flag_of_Europe.svg.png" width=140/>
    </a>
    <br>
    <br>
        <b>This project is being funded in the context of <a href="https://stelar-project.eu">STELAR</a> that is an <a href="https://research-and-innovation.ec.europa.eu/funding/funding-opportunities/funding-programmes-and-open-calls/horizon-europe_en">HORIZON-Europe</a> project.
        </b>
    <br>
</div>
