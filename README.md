# subtype_express
HIV-1 Proviral Subtyping Express v1.0 is an R-based script for viral subtyping against a user-defined list of reference sequences. 

The reason we developed a new algorithm instead of using exiting programs such as RIP 3.0 and/or REGA was because proviral genomes often contain large deletions and/or internal inversions whereas RIP 3.0 and REGA are only able to process continuous (ie. non-truncated) HIV-1 sequences in the sense strand.  

Briefly, there are two parts in this code.  The first part of the code takes a query HIV-1 genome and tries to retrieve gag, pol (PR), pol (RT), pol (RNaseH), pol (INT), vif, vpr, tat/rev exon1, vpu, env (gp120), env (gp41) and nef from the query genome.  Each of the viral genes, if present in the query, are then pairwise-aligned with the HIV subtype reference sequences downloadable from the Los Alamos HIV Sequence databases.  Each pair of query-reference yield percentage identity (PID) calculation.  The subtype reference with the highest PID against the query is the viral subtype reported.

The second part of the code employs a sliding window approach:  The query genome is analyzed in a user-defined slice size (e.g. 400 nucleotides, user-defined).  Each slice is again pairwise aligned against the Los Alamos HIV subtype reference sequences, then each slice is assigned a subtype of the subtype reference that shared the highest percentage identity with the query slice.  This approach is more refined in terms of “pinpointing” a more accurate breakpoint.  However, this approach is just as sensitive to setting changes as the other recombination detection tools which cannot be used in for proviral genomes in batch because multiple sequence alignment is not possible for most of the defective proviral genomes. For more on the algorithm/settings-dependent nature of recombination breakpoints identification, please refer to algorithms such as RIP window sizes and SCUEAL settings.

1. To start, download and unzip **SubtypeExpress_v1.0.zip**
2. Ensure these files are in the run directory
  (1) HXB2_REF_Genes_ver01.fasta (these are the genes in the genome you wish to subtype)
  (2) LoMo_2021_SubtypeCon_NoRecomb_ver02.fasta (these are the subtyping references; change accordingly)
  (3) Test_Input_8E5_S1049.fasta (this is your input query in FASTA format)
  (4) R_ResSubtype_01_PID_ver03_HXB2startend.R
  (5) R_ResSubtype_02_Pivot_ver01.R
3. Install NCBI BLAST+, R Biostrings
4. Change the BLAST directory in R_ResSubtype_01_PID_ver03_HXB2startend.R under variable MyBlastnDir
5. First run **R_ResSubtype_01_PID_ver03_HXB2startend.R**
6. Then run **R_ResSubtype_02_Pivot_ver01.R**

Your results can be found in:
Output_01_Subtype_PID
Output_02_Subtype_Pivot 
