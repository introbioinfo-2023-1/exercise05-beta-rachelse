| Organization | Course | Exercise | Semester | Professor | T.A. | 
| --- | --- | --- | --- | --- | --- |
| Seoul National University | Introduction to Bioinformatics | Homology Search and Phylogenomics | Spring 2023 | Asst. Prof. M. Steinegger (martin.steinegger@snu.ac.kr) | Luna Jang (jse9512@snu.ac.kr) <br /> Rachel Kim (eunbelivable@snu.ac.kr)|

# Exercise05: Protein structure prediction and alignment.

The goals of this exercise are:
1. Perform structure prediction.
2. Remote homology search using protein stucture alignment.
3. Perform complex prediction.
> Let's say you want to investigate a novel protein, but it is not annotated. What you only have is its amino acid sequence. You tried to find homologs of the protein, but BLAST doesn't give you any matches because the sequence is too diverged from any sequence in the database. However, you may find homologs using the stucture information because protein stucture can be conserved even when homology is not detected in the protein sequence. 
> So, first predict the protein stucture, and use it to find remote homologs sharing similar stucture. Based on the predicted structure and annotations of the remote homologs, you may find some insights about your protein. Also you can test if the protein works as monomer or multimer by peforming a complex predcition.

## General Instructions
1. Upload (git push) only the files that are specified with "(Result file: file name)".
2. This exercise will be done in web environment.

## Tools for the exercise
### ColabFold: [link for manual](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb)
ColabFold is an easy-to-use environment for fast and convenient protein structure predictions. Its structure prediction is powered by AlphaFold2 and RoseTTAFold combined with a fast multiple sequence alignment generation stage using MMseqs2, which speeds up the MSA generation by a factor of 16 over the AlphaFold system.

### Foldseek: [link for manual](https://github.com/steineggerlab/foldseek) [link for webserver](https://search.foldseek.com/search)
Foldseek is a software suite for searching and clustering protein structures. It is 600,000 times faster than the fastest state-of-the-art aligners. Allowing to query millions of structures in seconds.

## About the exercise

To submit your result, follow these steps:

- Step 1. Save the result files. 
- Step 2. Add edited files to git and commit
   ```sh
   # e.g.
   git add "edited files"
   git commit -m "COMMIT MESSAGE"
   ```
- Step 5. Submit your answers by pushing the changes.
   ```sh
   git push origin master
   ```

---

### 1. Protein stucture prediction & remote homology search
Suppose you started an early research about Sars-Cov-2. At the beginnig of the pendemic, there was insufficient available information.

1. Suppose you got a protein sequence from Sars-CoV-2 which is stored in the data directory(**sars_cov_2_protein.faa**). Perform protein stucture prediction using ColabFold [webserver](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb), and store the first rank (rank_1) predicted stucture in result directory. (Result file: **predicted_structure.pdb**)
   > - You can upload a file in your PC to Google Cloud Shell. You can easily search how to do it.
   > - Scroll down in the Colabfold page, and you can find an instruction for quick start.  


2. Find the remote homology of the protein using Foldseek. Give the **predicted_structure.pdb** to [Foldseek](https://search.foldseek.com/search) as a query and search it against **only** to **PDB100** database using 3DI/AA mode.

   > - You can drag and drop the PDB file on the **Queries** window and choose the target database using the checkboxes in **Search Settings**.
   > - In the result, the diagrams showing which part is aligned will appear first. Scroll down and you can find some measures of each alignment. Click the rightmost icon of each line to see the superimposed picture and TM-score.


   2-1. Write the sequence identity, e-value, score, TM-score of the top hit in **remote_homolog.csv** in result directory (Result file: **remote_homolog.csv**)
   > - To see the score, Click **NUMERIC** rather than GRAPHICAL as a view option.
  
   ```
   e.g.
   13.1,547,2.132e-11,0.61154
   11,700,3.234e-11,0.56154
   ```
   
   2-2. Click the targets and see the annotations. Based on the functions of the homologs, choose the most possible function of your protein and write it in **function.txt** in result directory. (Result file: **function.txt**) (Write only the alphabet.)
   ```
    a. Capsid protein
    b. DNA dependent RNA polymerase
    c. Reverse transcriptase
    d. RNA dependent RNA polymerase.
    e. Host immune system invasion.
    f. Binding to viral receptor of host cell.
   ```

3. You want to find out the domains protein have. 
   3-1. What is the searching options you would choose to find the domains of homology? Write the options in **search_options.csv** in result directory. (Result file: **search_options.csv**)
   ```sh
   # Answer should ordered in Databases,mode
   # e.g.
   PDB100,3DI/AA
   ```

   3-2. What is the dominant domain found in the homologs? Write the domain ID in **domain.txt** in result directory. (Result file: **domain.txt**)
   ```
   e.g.
   1.10.8.10
   ```

---

### Multimerization test

1. Suppose you have a protein sequence **single_unit.faa** and you want to know if it could form a homo-oligomeric protein. 
First, using colabfold, perform complex prediction of homo-dimer, homo-trimer, and homo-tetramer consist of  **single_unit.faa**. 
Then, comparing the PAE plots of dimer, trimer, and tetramer, define the most promissing oligomer and describe the reason of your choice.
Write your interpretation in **multimerization.txt** result directory (Result file: **multimerization.txt**)
