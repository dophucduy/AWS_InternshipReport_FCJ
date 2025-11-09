---
title: " AWS collaborates with Chugai Pharmaceutical Co. on quantum-inspired and constraint programming methods for cyclic peptide-protein docking"
weight: 3.3
pre: " <b> 3.3. </b> "

---
## Quantum Technology Blog [AWS](https://aws.amazon.com/blogs/quantum-computing/) 

---

**AWS collaborates with Chugai Pharmaceutical Co. on quantum-inspired and constraint programming methods for cyclic peptide-protein docking**  
*Authors: Kyle Brubaker, Akihiko Arakawa, Fabian Furrer, Jayeeta Ghosh, Helmut Katzgraber, and Kyle Booth — September 24, 2025 at Amazon Quantum Solutions Lab, Quantum Technologies*

*Original link: https://aws.amazon.com/blogs/quantum-computing/aws-collaborates-with-chugai-pharmaceutical-co-on-quantum-inspired-and-constraint-programming-methods-for-cyclic-peptide-protein-docking/*

When we have a three-dimensional model of a potential drug target (binding site), what is the orientation of the candidate drug molecule that "fits" (docks) with that binding site? Structure-based drug design involves using computational tools primarily to answer this question!

Chugai Pharmaceutical Co., Ltd., a leading Japanese pharmaceutical company, specializes in research, development, manufacturing, and marketing of prescription drugs in the fields of oncology, immunology/allergy, neurology, and kidney disease. In an effort to advance molecular research through quantum computing technology, Chugai has partnered with Amazon Web Services (AWS) to explore the application of quantum-compatible computational techniques to cyclic peptide simulation, aiming to accelerate drug discovery.

Peptides are short chains of amino acids linked together by peptide bonds, typically containing about 2–50 amino acid residues. Cyclic peptides are peptides with a closed ring structure. Although cyclic peptide drugs have many advantages over traditional small molecules [1, 2], simulating their docking with exogenous proteins is time-consuming and error-prone due to the larger number of rotational bonds.

In this article, we summarize AWS's efforts in collaboration with Chugai to construct the cyclic peptide docking problem as a Quadratic Unconstrained Binary Optimization (QUBO) model, which is suitable for quantum computing. Modeling the problem as QUBO allows the application of both classical and quantum optimization methods, such as classical and quantum annealing, to optimize peptide particle positions. We also developed a Constraint Programming (CP) model used as a baseline method. These methods were tested on example cases from the Protein Data Bank (PDB), and we used an end-to-end framework to predict the three-dimensional structure of multiple cyclic peptides in environments with exogenous proteins. Both methods successfully predicted configurations, however, the QUBO-based method encountered scalability limitations when exceeding six peptides and 34 protein residues, while the CP method could solve all cases in the test set.

For more details, please refer to our scientific paper published in [Scientific Reports](https://www.nature.com/articles/s41598-025-05565-1).

**Representation of cyclic peptides and exogenous proteins**  
To represent peptides, we use a "coarse-grained" representation for each amino acid, where main atoms and side chains are represented by single particles. We use two particles for all amino acids except Glycine, which has no side chain and therefore requires only a single particle (Figure 1).

*Figure 1 – Example of coarse-grained representation of Glycine (G) with 1 particle and Lysine (K) with 2 particles. Blue is used for the main chain, and green for the side chain.*

We place these peptide particles on a three-dimensional tetrahedral lattice, as illustrated in Figure 2. Interactions between amino residues are calculated using the [Miyazawa-Jernigan (MJ) potential](https://pubmed.ncbi.nlm.nih.gov/8604144/) [3]. The goal is to find the optimal arrangement of particles on the lattice such that the total interaction energy is minimized, while ensuring cyclization conditions and avoiding particle overlap.

*Figure 2 – Feasible arrangement of cyclic peptide P-K-I-D-N-G on a tetrahedral lattice, with blue representing the main chain and green representing side chains. The cyclization bond is colored red. Some free vertices of the tetrahedral lattice are illustrated in white.*

We only consider the "active site" of the target protein – a concentrated region where the peptide is likely to bind. This helps reduce the problem space and increase the likelihood of finding the optimal peptide orientation. To identify the active site in the target protein, we identify amino residues within a specified distance (in this case 5Å) from the peptide's amino residues. The protein affects the peptide on the lattice in two ways: it blocks some positions that are too close (within 3.8Å) where the peptide cannot fit, and it creates interaction regions (within 6.5Å) where protein and peptide can interact. After removing blocked positions, we calculate the energy between each part of the peptide and nearby protein parts at interaction points. The distances chosen for the active site, blocked region, and interaction region will affect the solution the system finds.

**QUBO Model**

We investigate modeling and solving this problem using Quadratic Unconstrained Binary Optimization (QUBO), which is suitable for quantum properties. QUBO is a combinatorial optimization problem aimed at minimizing a quadratic function with binary variables (0 or 1). In this work, we start by representing the problem as high-order binary optimization, then use locality reduction techniques to convert to QUBO form.

Many Hamiltonian expressions for non-docking protein folding problems have been introduced and analyzed with different encoding strategies. The original work by Perdomo et al. [4] used spatial encoding to map protein positions to a 2D lattice. Later, researchers developed turn encoding methods [5], describing protein shape through sequences of steps, making it more efficient for long proteins. Many groups have improved this method: Babbush et al. [5] created the "turn ancilla" method, while other groups adapted it for different types of spatial lattices and quantum computing methods.

Our model is an extension of the "resource-efficient" turn encoding method [6]. The original model includes interactions between peptides, non-overlap constraints between non-consecutive particles, and no-return constraints to prevent consecutive particles from overlapping. Therefore, the Hamiltonian expression consists of two parts: Hcomb, handling interactions between peptides and non-overlap errors; and Hback, ensuring consecutive particles do not return to the same lattice point. To extend this model to integrate external proteins in cyclic peptides, we add two components: Hcycle to impose peptide cyclization conditions, and Hprotein to handle peptide–protein interactions and steric collisions.

The Hcycle component ensures cyclization between specific amino acid pairs by requiring them to be nearest neighbors (1-NN) on the lattice, using the distance function *d(x, y)* to calculate the number of lattice steps between vertices. For peptide–protein interactions, Hprotein includes MJ interaction energy for peptide residues within the protein's interaction region and penalties for blocked positions due to steric collisions.

The final expression combines all components, extending the original model to include cyclization factors and protein interactions:

*H = Hcomb + Hback + Hcycle + Hprotein* 

- Hcomb : Combines interaction energy between peptides with overlap penalties  

- Hback : Imposes no-return constraints for consecutive particles  

- Hcycle : Enforces cyclization constraints  

- Hprotein : Handles peptide–protein interactions and steric collisions

**Constraint Programming (CP) Model**

As a baseline, we built a Constraint Programming (CP) model for the problem. CP is a method for solving constraint satisfaction and optimization problems, including both problem modeling and backtracking-based solvers. Typically, users describe the problem with specific variables and constraints, then the search process tries different possibilities to find solutions. The term "programming" here means "planning" rather than "coding."

Main constraints in the CP model:

- Place amino residues at valid lattice points, excluding positions affected by steric collisions from external proteins  

- Maintain precise distances between bonded amino residues  

- Prevent overlap between amino residues  

- Impose cyclization bonds between amino residues  

The model's objective function is to minimize the total MJ interaction energy between adjacent particles. The CP model is designed to optimize interaction energy between amino residues on the lattice while complying with various spatial constraints. CP can flexibly handle logical constraints and nonlinear relationships that linear programming models find difficult to implement. The model ensures amino residues are placed correctly on the lattice, avoiding overlap, and considering interactions within allowable ranges.

**Results**

To evaluate the methods, we built a comprehensive processing pipeline for protein–peptide complexes from the Protein Data Bank (PDB) to predict the optimal three-dimensional structure of bound peptides. The PDB repository contains detailed and standardized atomic coordinates for ring protein complexes. The pipeline consists of the following steps, as illustrated in Figure 3:

- Separate the PDB file into two parts: peptide and target protein  

- Identify the protein's active site – the concentrated region where the peptide is likely to bind  

- Classify each atom in the peptide as main chain or side chain, then calculate the weighted center of mass of each group, creating a 2-particle representation for each amino acid  

- Create a tetrahedral lattice to discretize the search space for discrete optimization methods  

- Filter the lattice based on active site coordinates and steric collision radius to remove collision-causing vertices, creating the final lattice structure  

*Figure 3 – Conversion from atomic representation to coarse-grained 2-particle representation on tetrahedral lattice*

PDB serves as standard data for comparison with model predictions. However, the tetrahedral lattice has some limitations: actual peptides are not fixed to rigid structures, but their shapes are determined by natural forces. Therefore, comparing predicted structures with actual structures from PDB is not straightforward. Nevertheless, we evaluate the model's solutions based on two criteria: MJ interaction energy value and root mean square distance (RMSD) compared to actual peptide coordinates (from PDB files) in Euclidean space. RMSD measures the average distance between coarse particles of actual peptides and model-generated peptides. Any RMSD value exceeding 4Å is considered insufficiently accurate for practical use.

| PDB Code | Peptide Sequence | Number of amino residues |  |
| :---: | :---: | :---: | :---: |
|  |  | **Peptide** | **External Protein** |
| 3WNE | P-K-I-D-N-G | 6 | 26 |
| 5LSO | K-S-R-W-D-E | 6 | 34 |
| 3AV9 | S-A-K-I-D-N-L-D | 8 | 28 |
| 3AVI | S-L-K-I-D-N-M-D | 8 | 32 |
| 3AVN | S-H-K-I-D-N-L-D | 8 | 28 |
| 2F58 | H-I-G-P-G-R-A-F-G-G-G | 11 | 49 |

*Table 1: Peptide–protein complexes from the RCSB Protein Databank ([https://www.rcsb.org/](https://www.rcsb.org/)) used for our experimental analysis.*

We analyzed six peptide–protein complexes from PDB, with peptide amino residue counts ranging from 6 to 11 and protein active site amino residue counts ranging from 26 to 49, as shown in Table 1. For the QUBO model, we applied simulated annealing – a heuristic algorithm, implemented in an open-source Python hybrid framework. Hyperparameter optimization was performed using Bayesian optimization through Amazon SageMaker. The CP model was implemented using the OR-Tools library and solved optimally within a 300-second time limit on Amazon EC2 m5.4xlarge virtual machines.

| PDB ID | Without External Protein |  |  |  | With External Protein |  |  |  |
| ----- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  | **MJ potential** |  | **RMSD (Å)** |  | **MJ potential** |  | **RMSD (Å)** |  |
|  | **QUBO** | **CP** | **QUBO** | **CP** | **QUBO** | **CP** | **QUBO** | **CP** |
| 3WNE | -1.87 | -1.87 | 10.03 | 7.77 | -28.53 | -42.64 | 8.88 | 8.48 |
| 5LSO | -5.93 | -5.97 | 13.31 | 13.20 | -17.93 | -23.26 | 7.68 | 10.29 |
| 3AV9 | -6.18 | -6.64 | 11.36 | 9.92 | – | -40.44 | – | 8.98 |
| 3AVI | -7.43 | -8.34 | 9.65 | 9.39 | – | -62.34 | – | 8.74 |
| 3AVN | -6.52 | -6.88 | 10.60 | 10.75 | – | -55.12 | – | 8.34 |
| 2F58 | -6.18 | -13.61 | 11.52 | 11.39 | – | -4.02 | – | 10.42 |

*Table 2: Comparison of MJ interaction energy values and RMSD for QUBO and CP methods, with and without external protein.*

Table 2 compares performance metrics (MJ interaction energy and RMSD) between the two QUBO and CP methods for each peptide, with and without external protein, as there was no benchmark from previous studies to compare our results.

The QUBO method found feasible solutions for problems with peptides containing up to 6 amino residues and target proteins with 34 amino residues. A feasible solution is a configuration that satisfies all problem constraints but may not be optimal in terms of MJ interaction energy. However, for larger cases, QUBO often struggled and produced solutions that violated constraints, because in the QUBO model constraints must be incorporated into the objective function as penalty functions. When there was no external protein, QUBO successfully solved all test cases, achieving the lowest energy scores in 5/6 cases, except for the 2F58 complex which performed worse than CP. Both methods achieved equivalent accuracy (by RMSD) in matching actual structures. However, when protein was present, QUBO only succeeded with 2/5 peptides (3WNE and 5LSO), and achieved higher energy scores than CP in both cases. Notably, QUBO showed higher accuracy than CP for the 5LSO peptide based on RMSD.

Figure 4 illustrates how both QUBO and CP methods successfully modeled the 5LSO peptide in the presence of protein, producing valid structures compared to the actual structure in the protein database. This shows that optimizing energy scores does not always lead to more accurate structure prediction, especially when starting from non-optimal positions on the tetrahedral lattice model.

The CP method showed scalability, solving problems with up to 11 peptide amino residues and 49 target protein amino residues optimally.

*Figure 4: Results image of 5LSO peptide. Comparison of actual peptide in PDB (left) with QUBO model results (center) and CP-MJ 1-NN results (right). Peptides are represented by blue and green dots (corresponding to main chain and side chain), while red dots represent amino residues of the external protein.*

**Conclusion**

In this article, we introduced a binary model suitable for quantum properties for the cyclic peptide binding problem. Two QUBO and CP methods were compared on a set of peptide cases, where QUBO found feasible solutions for small problems (up to 6 peptide amino residues and 34 protein amino residues) with competitive MJ interaction energy, while CP showed better scalability by optimally solving larger problems (up to 11 peptide amino residues and 49 protein amino residues), as illustrated in the 5LSO peptide case.

The QUBO method worked effectively in protein-free environments, nearly equivalent to CP in solution quality. However, QUBO struggled to ensure feasibility when protein was present, along with inherent challenges in representing distance-dependent interactions in the model, suggesting that QUBO-based quantum optimization techniques may not be the most suitable approach for this specific application. Despite limitations, especially regarding scalability, the QUBO method remains a potential foundation for future research as quantum algorithms and hardware continue to develop.

The performance of the CP method also demonstrates the long-term suitability of traditional optimization methods in computational biology. As this field advances, hybrid methods combining quantum and classical techniques may be the most effective choice for solving complex biological molecular modeling problems. Looking ahead, the robust performance and scalability of the CP method make it a promising development direction in peptide–protein interaction research. These findings not only contribute to understanding computational protein modeling but also provide useful guidance for researchers in choosing appropriate methods for similar biological optimization problems.

The use of lattice structures to model cyclic peptide binding, while helping to simplify the problem, brings inherent limitations because actual peptides are not constrained to rigid structures but follow natural steric forces. This simplification contributes to significant RMSD (root mean square deviation) values when comparing model results with actual structures from the Protein Data Bank (PDB).

For those interested in peptide drug design or computational structural biology, this research provides valuable insights into current algorithmic methods and their associated trade-offs. It also emphasizes the importance of continued research to bridge the gap between simple computational models and the complex reality of biological molecular interactions. You can read our paper in [Scientific Reports](https://www.nature.com/articles/s41598-025-05565-1) to learn more about the methodology, implementation, and overall process. If you need support with similar challenges, please contact AWS to learn how [AWS Professional Services](https://aws.amazon.com/professional-services/) and [Amazon Quantum Solutions Lab](https://aws.amazon.com/quantum-solutions-lab/) can assist you.

**References**

[1] L. Wang, N. Wang, W. Zhang, X. Cheng, Z. Yan, G. Shao, X. Wang, R. Wang, C. Fu, "Therapeutic peptides: current applications and future directions". In Signal Transduction and Targeted Therapy, volume 7 (number 1), 2022.

[2] A. Ohta et al., "Validation of new methods for creating oral drugs that overcome the Rule of 5 for difficult-to-access intracellular targets". Journal of the American Chemical Society, volume 145 (number 44), 2023.

[3] S. Miyazawa, R. Jernigan, "Estimation of effective contact energy between amino residues from protein crystal structures: quasi-chemical approximation", Macromolecules, volume 18 (number 3), 1985.

[4] A. Perdomo, C. Truncik, I. Tubert-Brohman, G. Rose, A. Aspuru-Guzik, "Construction of model Hamiltonians for adiabatic quantum computation and its application to finding low-energy conformations of lattice protein models", Physical Review A, volume 78, article 012320.

[5] R. Babbush, A. Perdomo-Ortiz, B. O'Gorman, W. Macready, A. Aspuru-Guzik, "Construction of energy functions for lattice heteropolymer models: efficient encoding for constraint satisfaction programming and quantum annealing", Advances in Chemical Physics, John Wiley & Sons, Inc., 2014, pages 201–244.

[6] A. Robert, P. K. Barkoutsos, S. Woerner, I. Tavernelli, "Resource-efficient quantum algorithm for protein folding", npj Quantum Information, volume 7, article 38.

TAGS: [Amazon Quantum Solutions Lab](https://aws.amazon.com/blogs/quantum-computing/tag/amazon-quantum-solutions-lab/), [quantum algorithms](https://aws.amazon.com/blogs/quantum-computing/tag/quantum-algorithms/), [quantum computing](https://aws.amazon.com/blogs/quantum-computing/tag/quantum-computing/), [Quantum Technologies](https://aws.amazon.com/blogs/quantum-computing/tag/quantum-technologies/)

**Kyle Brubaker**

Kyle Brubaker is a Senior Applied Scientist at AWS's Advanced Solutions Lab. He received his Master's degree in Biomedical Engineering from New York University (NYU), specializing in brain–computer interfaces. Kyle has an industrial background in machine learning and machine learning engineering, and has recently transitioned to research in quantum computing, optimization, and hybrid machine learning solutions.

**Akihiko Arakawa**

Akihiko Arakawa is a data scientist at Chugai Pharmaceutical Company. He specializes in computational chemistry in small and medium molecule drug development research. Additionally, he leads a research group applying quantum computing to drug development processes. Akihiko received his PhD in structural biology from the University of Tokyo.

**Fabian Furrer**

Fabian Furrer is a Senior Researcher at AWS's Advanced Solutions Lab. Fabian is passionate about helping customers optimize business operations using classical and quantum optimization techniques. He holds a PhD in quantum information theory from Leibniz University Hanover, and was a postdoctoral researcher at the University of Tokyo and NTT Basic Research Laboratory in Japan. Fabian also has many years of industry experience as a quantitative risk manager in the energy economics field at a utility company.

**Jayeeta Ghosh**

As a Senior Data Scientist at AWS Professional Services, Jayeeta Ghosh collaborates with customers to solve complex business challenges across multiple engineering and industrial fields. She holds PhD and Master's degrees in Chemical Engineering from UC Davis, then conducted postdoctoral research at Rutgers University and the University of Illinois, Urbana-Champaign. Before transitioning to data science consulting roles at Trace3 and QuaEra, she was a Senior Scientist at Simulations Plus, where she developed machine learning and artificial neural network (ML/ANN) models for drug candidate screening using Cheminformatics.

**Helmut Katzgraber**

Dr. Helmut Katzgraber received his bachelor's degree in physics from ETH Zurich, and Master's and PhD degrees in physics from the University of California Santa Cruz. After postdoctoral research positions at the University of California Davis and ETH Zurich, he was awarded a professorship fellowship from the Swiss National Science Foundation. In 2009, he joined Texas A&M University as an assistant professor and became a full professor in 2015. Katzgraber joined Microsoft in 2018 as a senior research manager, before moving to Amazon in 2020. He was elected Fellow of the American Physical Society in 2021 and currently leads the Advanced Solutions Lab at AWS.

**Kyle Booth**

Kyle Booth is a Senior Applied Scientist at AWS's Advanced Solutions Lab. He received his PhD in Operations Research from the University of Toronto. His research focuses on constraint programming and integer programming to solve combinatorial optimization problems. Before joining AWS, he was a scientist at NASA Ames Research Center.