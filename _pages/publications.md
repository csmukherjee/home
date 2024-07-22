---
layout: archive
title: "Research"
permalink: /publications/
author_profile: true
---

I am primarily interested in the inference of structure both in statistical models and real-world data. Here, I describe my research explorations in further detail. 

## Unsupervised learning on statistical models (stochastic block model):
 At the start of my PhD, I wanted to explore random structures(such as random graphs) and learning theory. At this point, I came across a stochastic block model (SBM), one of the most fundamental statistical models for graph clustering. 
<details>
<summary> <b> Overview: </b> </summary>

The simple case can be defined as follows. A graph is built on n vertices, where the vertices have a "hidden" partition into two communities. Then, each pair of vertices belonging to the same community is connected by an edge with some probability p. Each pair of vertices from different communities is connected with probability q (with p>q; assume p=0.51 and q=0.49, for example). Then, given such a graph, the task is to recover these hidden communities with high probability.  
This is one of the most well-studied problems in clustering, with several important and beautiful results in the last 40 years (Read the citations in [1] for an in-depth review). However, we observed that some important problems are unresolved. 

### Unbalanced SBM: 
First, we focused on a problem known as the ``small cluster barrier'' in the literature. This refers to the fact that most community recovery algorithms for SBM graphs need *all* of the hidden communities to be significantly large. Even if one cluster is very small, the guarantees of these algorithms fail. In this direction, we designed a spectral algorithm that recovers large communities in the presence of arbitrarily small communities (improving on the state-of-the-art), resulting in the publication [2].  


### Vanilla algorithms: The "power" of power method: 
At this point, we observed that the algorithms that the previously state-of-the-art algorithms for the aforementioned problems, as well as our algorithms, were somewhat *complex*. For example, our algorithm involved partitioning the graph's adjacency matrix into 8 parts, then using two parts to get a partial clustering on some of the vertices and then using the other parts to filter and expand the clustering to other vertices. Similar complex steps are often observed in provable clustering algorithms for SBM. In contrast, practitioners often use very simple algorithms (such as spectral clustering) to recover clusters on real-world graphs. Thus, it seemed that the algorithms were complicated to simplify the proofs, and not to boost the actual performance of the algorithm! 

Indeed, this phenomenon was observed by mathematicians such as Emmanuel Abbe and Van Vu in different works, and they conjectured (and in some special cases resolved) that very simple algorithms should also have near-optimal provable guarantees compared to all existing works. Motivated by this, we showed that a simple power method is able to recover the communities and is logarithmically tight compared to best-known bounds [1]. Our algorithm is very simple. You first centralize the adjacency matrix of the graph and then take log(n)-th power of this matrix. We showed that in this powered matrix, rows belonging to vertices from the same community would have much less Euclidean distance than the inter-community rows. In fact, this algorithm was the first *parameter-free* algorithm that overcomes the small cluster barrier (previous works needed knowledge of the probability parameters p and q, for example). To prove the correctness of this simple algorithm, we devised certain *random partition* based ideas to analyze low-degree polynomials of random variables that we think may be of independent interest. 

</details>

## Modeling and analysis of real-world graphs:
Two of the primary reasons behind the popularity of SBM are its ability to capture certain real-world networks and its simplicity, which allows inference and understanding of various statistical and computational phenomena. However, the model can indeed be too simple to capture more complex graphs that may arise in real-world scenarios. Motivated by this, we aimed to explore the structural properties of real-world graphs with underlying communities.

<details>
<summary> <b> Overview: </b> </summary>
In this direction, we focused on single-cell RNA seq data, a very influential data type in biology that has been crucial in the identification of marker genes for different types of cancer, among many other applications. Here, each data point corresponds to a cell, and a fundamental task is to partition the cells according to their underlying cell type, which is costly to obtain through biological experiments alone, necessitating the use of clustering algorithms. Here a standard pipeline is\
\

<p align=center> Data(10,000+ features) ->PCA(50-100 dimensions)-> Embedding onto a graph->graph clustering. </p>





</details>



## Publications 

1.

2. Chandra Sekhar Mukherjee and Jiapeng Zhang, [Compressibility: Power of PCA in Clustering Problems Beyond Dimensionality Reduction](https://arxiv.org/abs/2204.10888). 2022.

3. Chandra Sekhar Mukherjee and Jiapeng Zhang, [Detecting Hidden Communities by Power Iterations with Connections to Vanilla Spectral Algorithms](https://arxiv.org/pdf/2211.03939.pdf). *SODA 2024*.

4. Chandra Sekhar Mukherjee, Pan Peng, and Jiapeng Zhang, [Recovering Unbalanced Communities in the Stochastic Block Model With Application to Clustering with a Faulty Oracle](https://arxiv.org/abs/2202.08522). *Neurips 2023*.


---
## Some pre-PhD works





1. Subhamoy Maitra, Chandra Sekhar Mukherjee, Pantelimon Stanica, and Deng Tang, [On Boolean Functions with Low Polynomial Degree and Higher Order Sensitivity](https://arxiv.org/abs/2107.11205), 2021.

2. Suman Dutta, Subhamoy Maitra, and Chandra Sekhar Mukherjee, [Following Forrelation -- Quantum Algorithms in Exploring Boolean Functions' Spectra](https://www.aimsciences.org/article/doi/10.3934/amc.2021067), Advances in Mathematics of Communications. 2021.

3. Ajeet Kumar, Subhamoy Maitra, and Chandra Sekhar Mukherjee, [On approximate real mutually unbiased bases in square dimension](https://link.springer.com/article/10.1007/s12095-020-00468-6), Cryptography and Communications, 2021.

4. Chandra Sekhar Mukherjee, Subhamoy Maitra, Vineet Gaurav, and Dibyendu Roy, [Preparing Dicke States on a Quantum Computer](https://ieeexplore.ieee.org/abstract/document/9275336), IEEE Transactions on Quantum Engineering. 2020.

## Monographs

1. Chandra Sekhar Mukherjee, Dibyendu Roy, and Subhamoy Maitra, [ Design and Cryptanalysis of ZUC--A Stream Cipher in Mobile Telephony](https://link.springer.com/book/10.1007/978-981-33-4882-0), SpringerBriefs on Cyber Security Systems and Networks. 2021.



