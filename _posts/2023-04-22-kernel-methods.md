---
layout: post
title: "Kernel Methods Applied in Protein Related Problems"
date: 2023-04-22
categories: jekyll update
toc: true
---

* TOC
{:toc}

## 1. Background

We all know that our DNAs encodes our genetic information. In 1958, Francis Crick brought up the central dogma theory, which was saying that the genetic information flows in on direction from DNAs to RNAs to make functional products, proteins. Eventhough nowadays researchers found exceptions in some species like viruses, central dogma explained the most common way of how proteins are generated. The three DNA nucleotides will be transcripted to three mRNA nucleotides, and then will be translated to a single amino acid.  A chain of amino acid will form a protein sequence, and folding the protein sequence will generate a protein in 3D structure. 

![iShot_2023-04-27_02.28.24](/assets/img/iShot_2023-04-27_02.28.24.png)

With the evolution of high throughoutput sequencing, it's much easier now for researchers to gain protein sequence and protein structure information. [UniProt](https://www.uniprot.org/) is one of the public database that benifits from the genome sequencing project. The plenty of protein sequences and a large amount of informations about their biological functions make UniProt the most commonly used public database for machine learning models that are trained based on the protein sequences. 

[AlphaFold](https://github.com/lucidrains/alphafold2) is an AI system developed by DeepMind that predicts a protein's 3D structure from its amino acid sequence. With the protein sequences in the UniProt, AlphaFold will be able to generate their folding structures that can be used to train graph related machine learning models. 

![iShot_2023-04-27_03.08.07](/assets/img/iShot_2023-04-27_03.08.07.png)

## 2. Motivations

It has been estimated that every person contains around 30 nucleotide mutations in their gamete that will be passed to the next generation. The outcomes of these mutations are hard to predict, not to even mention the existing variants in a population. The mutations could result in beneficial proteins for evolution or cause deficiant proteins that contribute to sever rare diseases. Therefore, the ability to predicting such outcomes is essential for discovering genetic variants disease association and even drug design. However, current biophysical prediction methods cannot distinguish the functional level of closely related proteins, and experimental assays are expensive and time consuming. Compared to experimental approach, machine-learning models reduce the cost and the time of prediction, and they can be predictive even when the underlying biophysical mechanisms are not well understood. Therefore, machine learning approaches became more and more popular in solving protein related problems.

The prediction of protein function reduces to the follwing questions: (1) prediction of the biological function of the molecule (2) prediction of protein-protein interactions (PPI). Most proteins perform their functions by interacting with other proteins. For example, the affinity between the antigens and the T cells can be used to determine if the antigen have the function to activate naive T cells to cytotoxic T cells. The biological functions of  proteins, such as participating in metabolism, will be helpful in understanding cellular pathways.

## 3. Kernel Methods

Kernel methods calculate the similarities between pairs of inputs. The kernel methods usually project the input feature into a high-dimensional feature space without explicitly calculate the coordinate in the new space. The similarities between proteins or protein residue is determinant, because the composition of protein sequences and structures has a large impact on the protein function. Similar proteins tend to have similar domains, thus are more possible to have similar functions. This report will review the string kernel methods proposed by A. Ben-Hur *et al.* [1] and graphlet kernel methods proposed by LUGO-MARTINEZ *et al.* [2].

### 3.1 String Kernel Methods

The string kernels raised by A. Ben-Hur *et al.* was based on three sequence kernels, the spectrum kernel, the motif kernel, and the Pfam kernel. The spectrum kernel models a sequence in the space of all kmers, and its features count the number of times each kmer appears in the sequence [3]. The sequence models for the motif kernel are discrete sequence motifs, providing a count of how many times a discrete sequence motif matches a sequence [4]. The Pfam kernel uses a set of hidden Markov models (HMMs) to represent the domain structure of a protein, and is computed by comparing each protein sequence with every HMM in the Pfam database [5].

However, the sequence kernels are not sufficent to solve protein-protein interaction problems, because they only provide similarities between a pair of proteins instead of tw pairs of proteins. Therefore, A. Ben-Hur *et al.* proposed the pairwise kernel, which is constructed by expressing the similarity between pairs of proteins in terms of similarities between individual proteins. In this approach, two pairs of proteins are similar similar to one another when each protein of one pair is similar to one protein of the other pair.

![iShot_2023-04-27_05.10.18](/assets/img/iShot_2023-04-27_05.10.18.png)



A. Ben-Hur *et al.* also mentioned that the pairwise kernel can be used alternatively when similarity within the pair is directly related to the likelihood that a pair of proteins interact. Such kernel is called non-sequence kernel. This kernel is a valid kernel even if K is not a kernel, because in this formulation *K'* is simply a feature of the pair of proteins. For example, it could be GO annotation, local properties of the interaction network, or homologous interactions in other species. In the paper, the author used a Gaussian kernel for *K'*.

![iShot_2023-04-27_05.15.34](/assets/img/iShot_2023-04-27_05.15.34.png)

A. Ben-Hur *et al.* also provided an option to combine all the kernels to improve the performance. Assuming that the sequene kernels are denoted as *K* and the pairwise kernel is denoted as *K<sub>p</sub>*, the final kernel can be defined as the summation of all the pairwise kernels taking sequence kernels as input. An alternate combination is a pairwise kernel taking the summation of all the sequence kernels. In practice, the results from these two different approaches were very close, and the mixing approach was used because of its lower memory requirement.

### 3.2 String Kernel Methods Evaluation

The author used 5-fold cross-validation and compared the ROC and ROC<sub>50</sub> of all ther string kernels. The ROC<sub>50</sub> is the normalized area under that curve up to the first 50 false positives. The ROC<sub>50</sub> can be useful on a low-throughput method. A predictor that maximizes the quality of the high-confidence interactions is going to be more useful and will have higher ROC<sub>50</sub>. 

It is obvious from the table that the spectrum kernel achieves a higher ROC score of 0.81 than the motif and Pfam kernels. However, it's ROC<sub>50</sub> score is extremly lower than the other two kernels. It suggests that the motif and Pfam kernels are likely to be more accurate with data that offer a good  description of a sequence. Combining the non-sequence features with the pairwise sequence kernel yielded better performance than any method by itself in both performance metrics.

![iShot_2023-04-27_05.37.34](/assets/img/iShot_2023-04-27_05.37.34.png)



![iShot_2023-04-27_05.32.00](/assets/img/iShot_2023-04-27_05.32.00.png)

### 3.3 Graphlet Kernel Methods

Comparing to sequence, graphs provides more information of protein in structures. LUGO-MARTINEZ *et al.* proposed an edit distance graphlet kernel which is based on the graphlet kernel [6], aiming at predicting the protein-protein interaction based the similarity between the vertices. 

A graphlet to be a small, simple, connected, rooted graph. A graphlet with n vertices is referred to as an n-graphletThe feature space of the graphlet kernels are the counts of graphlets on acyclic graphs or proteins. The figure below  represents graph lets enumerated up to isomorphism when the size of Σ is 1, where Σ is a finite alphabet that represents the node label, usually the amino acids. The *n<sub>i</sub>* means the i-th graphlet of order n. For example, the 3<sub>2</sub> represents a graphlet with three vertices, where the middle one is the root. 

![iShot_2023-04-27_06.36.20](/assets/img/iShot_2023-04-27_06.36.20.png)

When the size of Σ is larger than 1, there will be even more isomorphic labeled graphlets. The sizes of the isomorphic labeled graphlets for each base graphlets are not equivalent due to the symmetry of the graphlets. For example, the AAB and the BAA graphlets in the B panel are the identical graphlets.

![iShot_2023-04-27_06.47.16](/assets/img/iShot_2023-04-27_06.47.16.png)

To counts the graphlets on a graph, all the isomorphic labeled graphlets need to be listed.  For example, in the figure below, the panel A is the graph of a simplified protein, and the panel B is the feature space for the graphlet kernel. The count of the AAA of 3<sub>1</sub> base graphlet is two, because there are two isomorphic labeled graphlets that contain vertices v<sub>1</sub>, v<sub>3</sub>, v<sub>4</sub>, and v<sub>1</sub>, v<sub>3</sub>, v<sub>5</sub> with v<sub>1</sub> as the root. 

The edit distance kernel counts the graphlets in the same way, except that it allows for a substitution of one vertex label or the insertion/deletion of a edge. For example, when considering vertex v<sub>1</sub> and base graphlet 3<sub>3</sub>, the graphlet with labels AAB will lead to incremented counts for graphlets AAA, ABB and BAB, and same logic for the indel of the edges.

![iShot_2023-04-27_06.49.45](/assets/img/iShot_2023-04-27_06.49.45.png)

The graphlet kernel function is defined as:

 ![iShot_2023-04-27_07.03.43](/assets/img/iShot_2023-04-27_07.03.43.png)

or as a normalized kernel:

![iShot_2023-04-27_07.04.55](/assets/img/iShot_2023-04-27_07.04.55.png)

Finally, Support vector machines (SVMs) and K-nearest neighbor (KNN) classifiers were used to construct all predictors and perform comparative evaluation.



### 3.4 Graphlet Kernel Methods Evaluation

It's worth to mention that the complexity of the graphlet kernel is not ideal, considering the growth pattern of vertex-labeled graphlets. The author summarized the growth pattern of the graphlets whose n ∈ {1, 2, 3, 4, 5}.

![iShot_2023-04-27_07.10.04](/assets/img/iShot_2023-04-27_07.10.04.png)

which can be generalized as:

![iShot_2023-04-27_07.10.36](/assets/img/iShot_2023-04-27_07.10.36.png)



It is obvious that the edit distance kernel takes exponential time complexity and are applicable only to sparse graphs when relatively small values of nodes and edit distance are used.



The author used human protein-protein interaction (PPI) network to predict gene-disease associations, which are prediction of (1) cancer vs. other disease genes (Can), (2) metabolic disorder vs. other disease genes (Met), and (3) metabolic disorder vs. cancer genes (Met/Can). In the PPI network, proteins are represented as vertices and proteins that physically interact are linked by undirected edges. 

![iShot_2023-04-27_08.17.47](/assets/img/iShot_2023-04-27_08.17.47.png)

![iShot_2023-04-27_08.18.18](/assets/img/iShot_2023-04-27_08.18.18.png)

The table shows that edit distance kernels outperformed both graphlet kernels and random walk kernels. Edit distance kernels achieved the highest AUCs on all nine data sets with SVM classifiers (Table 5) and eight data sets with KNN classifiers (Table 6). Relative to the standard graphlet kernels, an increase in performance was observed in all nine cases with both SVMs and KNNs.   



## 4. Experiments

LUGO-MARTINEZ *et al.* only performed vertex classification using the standard graphlets instead of graph classification, which can be used for the prediction of protein functions. I wondered if the performance of the graphlet kernel will stay the same when applying to the graph classification, since the logic behind the protein functions prediction and protein-protein interaction prediction are similar. 

Therefore, I trained the standard graphlets using the adjacency matrices generated from AlphaFold that takes protein sequence in the UniProt. I added the counts in vertices that have same feature id together to get the feature space of a protein, and use SVM to construct all the predictors. There are 67,000,000 features generated, and it took me half day to trained the model with 2000 proteins. The AUC of the standard graphlet kernel over 2000 protein (half positive, half unlabeled) is 96.52%, when predicting if the protein involves in catalytic activity. The AUC is much higher than the AUCs in the previous section, so I'm planning to do a 4-fold cross-validation to test the stability of the results.

## 5. Conclusion

The common shortcomming of the string kernels and graphlet kernels is the complexity, due to the computation of the inner products of the feature space and the permutation of the isomorphic labeled graphlets. It's the obstacle of protein function prediction for years, and the possible future work would be to improve the computational efficiency of the graphlet kernels. The potential solution are applying the efficient graphlet kernels [7] and using the multitask learning to partition the feature space. 

It's also worth to explore if the graph neural network would be a better option for protein function prediction. While I'm reading kernel related papers, I found that kernel methods from ten years ago were still widely used in the prediction of protein function nowadays. It's possible that the graph neural network would have a better performance than the graphlet kernels, due to the more advanced algorithms.

Although the kernel methods applied in protein related problems can still be improved from various perspective, it already contributed a lot in the protein function prediction. The vast majority (>98%) of available GO annotations are assigned using computational methods, impling that the kernel methods can still be widely used in the future.

## 6. References

[1]  A. Ben-Hur and W. S. Noble, “Kernel methods for predicting protein–protein interactions,” *Bioinformatics*, vol. 21, no. suppl-1, pp. i38–i46, 2005, doi: 10.1093/bioinformatics/bti1016.

[2]  J. LUGO-MARTINEZ and P. RADIVOJAC, “Generalized graphlet kernels for probabilistic inference in sparse graphs,” *Network science (Cambridge University Press)*, vol. 2, no. 2, pp. 254–276, 2014, doi: 10.1017/nws.2014.14.

[3] Leslie,C., Eskin,E. and Noble,W.S. (2002) The spectrum kernel: A string kernel for SVM protein classification. In Altman,R.B., Dunker,A.K., Hunter,L., Lauderdale,K. and Klein,T.E. (eds), Proceedings of the Pacific Symposium on Biocomputing, New Jersey. World Scientific, Singapore, pp. 564–575.

[4] Nevill-Manning,C.G., Sethi,K.S., Wu,T.D. and Brutlag,D.L. (1997) Enumerating and ranking discrete motifs. In Proceedings of the Fifth International Conference on Intelligent Systems for Molecular Biology, pp. 202–209.

[5] Sonnhammer,E., Eddy,S. and Durbin,R. (1997) Pfam: a comprehensive database of protein domain families based on seed alignments. Proteins, 28, 405–420.

[6] Vacic, V., Iakoucheva, L. M., Lonardi, S., & Radivojac, P. (2010). Graphlet kernels for prediction of functional residues in protein structures. Journal of Computational Biology, 17(1), 55–72.

[7] Sherashidze, N. & Vishwanathan, S.V.N. & Petri, Tobias & Mehlhorn, Kurt & Borgwardt, Karsten. (2009). Efficient Graphlet Kernels for Large Graph Comparison. 12th International Conference on Artificial Intelligence and Statistics (AISTATS), Society for Artificial Intelligence and Statistics, 488-495 (2009). 5. 

