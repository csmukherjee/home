---
layout: archive
title: "Research"
permalink: /research/
author_profile: true
---

In my PhD so far, I have focused on unsupervised learning, starting with statistical models and extending to real-world data. 

## Unsupervised learning on statistical models (stochastic block model):
 At the start of my PhD, I wanted to explore random structures(such as random graphs) and learning theory. At this point, I came across a stochastic block model (SBM), one of the most fundamental statistical models for graph clustering. 
<details>
<summary> <b> Overview: </b> </summary>

The simple case can be defined as follows. A graph is built on n vertices, where the vertices have a "hidden" partition into two communities. Then, each pair of vertices belonging to the same community is connected by an edge with some probability p. Each pair of vertices from different communities is connected with probability q (with p>q; assume p=0.51 and q=0.49, for example). Then, given such a graph, the task is to recover these hidden communities with high probability.  
This is one of the most well-studied problems in clustering, with several important and beautiful results in the last 40 years (Read references in [1] for an in-depth review). However, we observed that some important problems are unresolved. 

<h3> Unbalanced SBM: </h3>

<br/>
<center>
<img src="https://github.com/user-attachments/assets/ea7653a8-19aa-49b2-b5c2-95fac9598b4c" style="width: 40vw" 
class="center">
</center>
 
First, we focused on a problem known as the ``small cluster barrier'' in the literature. This refers to the fact that most community (cluster) recovery algorithms for SBM graphs need <i>all</i> of the hidden communities to be significantly large. Even if one cluster is very small, the guarantees of these algorithms fail. In this direction, we designed a spectral algorithm that recovers large communities in the presence of arbitrarily small communities (improving significantly on the state-of-the-art), resulting in the publication [2].  



 
<h3> Vanilla algorithms: The "power" of power method: </h3>

At this point, we observed that the algorithms that the previously state-of-the-art algorithms for the aforementioned problems, as well as our algorithms, were somewhat <i>complex</i>. 
In contrast, practitioners often use simple algorithms (such as spectral clustering) to recover clusters on real-world graphs. Thus, it seemed that the algorithms were complicated in simplifying the proofs and not boosting the actual performance of the algorithm! 
<br/><br/>

Indeed, this phenomenon was observed by mathematicians such as Emmanuel Abbe and Van Vu when considering spectral algorithms. They conjectured that a simple SVD-based projection of the adjacency matrix should separate the communities. 
<br/><br/>

Motivated by this, we showed that a simple power method can recover the communities and is logarithmically tight compared to best-known bounds [1]. Our algorithm is very simple. You first centralize the adjacency matrix of the graph and then take log(n)-th power of this matrix. We showed that in this powered matrix, rows belonging to vertices from the same community would have much less Euclidean distance than the inter-community rows. 
As a consequence,
<br/><br/>
i) We resolved the conjecture of Vu when the size of all communities is the same (balanced SBM) via a connection between SVD projection and the power of a matrix. 
<br/>
ii) Obtained the <i>first parameter-free</i> algorithm that overcomes the small cluster barrier. In comparison, previous works needed knowledge of the probability parameters p and q to recover large clusters in the presence of small clusters. 
<br/><br/>
Thus, our analysis had new implications both in the balanced and unbalanced SBM. To prove the correctness of this simple algorithm, we devised certain <i>random partition</i> based ideas to analyze low-degree polynomials of random variables that we think may be of independent interest. 

</details>

## Modeling and analysis of real-world graphs:
Two of the primary reasons behind the popularity of SBM are its ability to capture certain real-world networks and its simplicity, which allows inference and understanding of various statistical and computational phenomena. However, the model can be too simple to capture more complex graphs that may arise in real-world scenarios. Motivated by this, we aimed to explore the structural properties of real-world graphs with underlying communities.

<details>
<summary> <b> Overview: </b> </summary>
In this direction, we focused on single-cell RNA seq data, a very influential data type in biology that has been crucial in identifying genes responsible for different types of cancer, among many other applications. Here, each data point corresponds to a cell, and a fundamental task is to partition the cells according to their underlying cell type, which is costly to obtain through biological experiments alone, necessitating the use of clustering algorithms. The standard pipeline is
<br/><br/> 
  

<p align=center> Data(10,000+ features) ->PCA(50-100 dimensions)-> Embedding onto a graph->graph clustering. </p>

The data is first passed through PCA to reduce dimensionality and noise (due to experimental error and biological variance). In this direction in [2] we captured the denoising ability of PCA via a novel metric called <i>compression ratio</i>. We designed an outlier detection algorithm that improves the separability of the underlying communities in the data. We proved the effectiveness of our algorithm in a novel random vector mixture model and verified it extensively on several real-world datasets.

<h3> Multi-core-periphery with communities (MCPC) </h3>

In the aforementioned pipeline, once the data is embedded onto a graph (with a datapoint-vertex correspondence), one applies graph clustering algorithms to recover the underlying communities (cell-type). Here, it is important to note that the clustering algorithm's success depends on the correctness of our assumption about the graph's communities. One of the most popular assumptions is <i>community structure</i> where all vertices from a community have more intra-community edges than inter-community edges (For example, SBM graphs follow this assumption). However, algorithms based on this assumption often have subpar performance on real-world datasets. 
<br/><br/>

<img src="https://github.com/user-attachments/assets/87aa1f31-bc69-4108-9d6b-a4f021c3cf3f">

To mitigate this issue, we proposed a novel graph structure named ``multiple core-periphery with communities'' (<b>MCPC</b>) by combining <i>community structure</i> with <i>core-periphery(CP) </i> structure [1]. Here, each community has a dense <i>core</i> and a sparser <i>periphery</i>, with inter-community edges more prevalent between peripheral vertices. In such a scenario, if we could identify just the cores from each community, they should be more separable (as they have fewer inter-community edges). To achieve this goal, we coined a new concept, called <i>relative centrality</i>, to rank the vertices of a graph such that the top-ranked vertices are core vertices of their respective communities. 
<br/><br/>
We applied our algorithms to a large set of real-world single-cell datasets. We observed that the top-ranked vertices contain sufficient vertices from all the underlying (ground truth) communities. Yet, they are better separable by popular graph clustering algorithms than the whole graph. 
<br/><br/>
Currently, we are working on further improving the algorithms and better understanding the presence of MCPC structures in real-world graphs.

</details>



## Publications 

1. Chandra Sekhar Mukherjee and Jiapeng Zhang, [Balanced Ranking with Relative Centrality: A multi-core periphery perspective](https://openreview.net/pdf?id=21rSeWJHPF). *ICLR 2025*

2. Chandra Sekhar Mukherjee, Nikhil Deorkar, and Jiapeng Zhang, [Capturing the Denoising Effect of PCA via Compression Ratio](https://arxiv.org/abs/2204.10888). *NeurIPS 2024*.

3. Chandra Sekhar Mukherjee and Jiapeng Zhang, [Detecting Hidden Communities by Power Iterations with Connections to Vanilla Spectral Algorithms](https://arxiv.org/pdf/2211.03939.pdf). *SODA 2024*.

4. Chandra Sekhar Mukherjee, Pan Peng, and Jiapeng Zhang, [Recovering Unbalanced Communities in the Stochastic Block Model With Application to Clustering with a Faulty Oracle](https://arxiv.org/abs/2202.08522). *Neurips 2023*.


---
## Some pre-PhD works

Previously, I worked under the guidance of Prof. Subhamoy Maitra during my time at ISI Kolkata, working on quantum computation and information.



1. Subhamoy Maitra, Chandra Sekhar Mukherjee, Pantelimon Stanica, and Deng Tang, [On Boolean Functions with Low Polynomial Degree and Higher Order Sensitivity](https://arxiv.org/abs/2107.11205), 2021.

2. Suman Dutta, Subhamoy Maitra, and Chandra Sekhar Mukherjee, [Following Forrelation -- Quantum Algorithms in Exploring Boolean Functions' Spectra](https://www.aimsciences.org/article/doi/10.3934/amc.2021067), Advances in Mathematics of Communications. 2021.

3. Ajeet Kumar, Subhamoy Maitra, and Chandra Sekhar Mukherjee, [On approximate real mutually unbiased bases in square dimension](https://link.springer.com/article/10.1007/s12095-020-00468-6), Cryptography and Communications, 2021.

4. Chandra Sekhar Mukherjee, Subhamoy Maitra, Vineet Gaurav, and Dibyendu Roy, [Preparing Dicke States on a Quantum Computer](https://ieeexplore.ieee.org/abstract/document/9275336), IEEE Transactions on Quantum Engineering. 2020.

## Monographs

1. Chandra Sekhar Mukherjee, Dibyendu Roy, and Subhamoy Maitra, [ Design and Cryptanalysis of ZUC--A Stream Cipher in Mobile Telephony](https://link.springer.com/book/10.1007/978-981-33-4882-0), SpringerBriefs on Cyber Security Systems and Networks. 2021.



