# **Student-Led-Tutorial: Genome Annotation Using Prokka**
### **Task**: Annotate a Bacterial Genome and Submit to a Public Repository
### **Date**: April 17th

---

## **Objective**
Students will:
1. Use **Prokka** to annotate a bacterial genome.
2. Visualize the annotated genome in a genome browser.
3. Validate the annotations and prepare the genome for submission to a public database.
4. Discuss the significance of genome annotation for research and the community.

---

## **Software and Manuals**
1. **Prokka**: Rapid prokaryotic genome annotation.  
   - [Prokka GitHub](https://github.com/tseemann/prokka)  
   - [Prokka Documentation](https://github.com/tseemann/prokka#usage)  
2. **tbl2asn**: For GenBank submission formatting.  
   - [tbl2asn Documentation](https://www.ncbi.nlm.nih.gov/genbank/tbl2asn2/)  
3. **KEGG Mapper**: Pathway visualization.  
   - [KEGG Mapper](https://www.genome.jp/kegg/mapper.html)  

---

## **Dataset**
### **Genome**:  
A draft genome of a bacterial species relevant to agriculture, healthcare, or the environment. For this tutorial:  
- **Example**: A rhizobial bacterial genome involved in nitrogen fixation.  
- **Source**: Download a draft genome from **NCBI GenBank** or **JGI Genome Portal**.  
- **Example dataset**:  
  - NCBI Assembly: [*Bradyrhizobium japonicum* USDA 110 genome](https://www.ncbi.nlm.nih.gov/assembly/GCF_000011365.1/).  

---

## **Step-by-Step Tutorial**
### Fork and clone repository(?)
### **Step 1: Install Prokka**
The HPC server has Prokka pre-installed.
   ```bash
   module load prokka/1.14.5
   ```
### **Step 2: Download the Genome**
1. Download the genome FASTA file from NCBI or JGI.
``` bash
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/011/365/GCF_000011365.1_ASM1136v1/GCF_000011365.1_ASM1136v1_genomic.fna.gz
```
2. Decompress the genome file
``` bash
gunzip GCF_000011365.1_ASM1136v1_genomic.fna.gz
```
2. Rename genome file for simplicity
``` bash
mv GCF_000011365.1_ASM1136v1_genomic.fna genome.fasta
```
### **Step 3: Annotate the Genome Using Prokka**
1. Run Prokka to annotate the genome:
``` bash
prokka --outdir prokka_output --prefix bradyrhizobium --genus Bradyrhizobium --species japonicum genome.fasta
```
- --outdir: Directory for output files.
- --prefix: Prefix for output filenames.
- --genus and --species: Specify the organism's name.
2. Key output files in prokka_output/:
- bradyrhizobium.gff: General feature format file with annotations.
- bradyrhizobium.gbz: Compressed binary format.
- bradyrhizobium.faa: Predicted proteins.
3. Push .faa, .gff, .gbz files to GitHub



### **Step 4: Validate Annotations**
2. Check for functional annotations:
- Identify key genes, such as those involved in nitrogen fixation (e.g., nif genes).
Use KEGG Mapper to map annotated genes to metabolic pathways:
- Upload bradyrhizobium.faa to KEGG Blast Koala (https://www.kegg.jp/blastkoala/).
- Send results to your SVSU email.
- Enter blastkopala generated KO numbers into the KEGG MAPPER- RECONSTRUCT (https://www.genome.jp/kegg/mapper/reconstruct.html)

### **Step 5: Visualization Using IGV**
1. Navigate to IGV (https://igv.org/app/)
- Genome --> Local File and upload .gbz file
- Tracks --> Local File and upload .gff file (see names of genes)
- Explore coding regions, functional annotations, and structural features.

- Search bar: nif, rpoN, zur

   - nif or nifA (.gff): product:   Nif-specific regulatory protein
         Location   NC_004463.1:2,196,261-2,198,009
   - zur: product:   Zinc uptake regulation protein
         Location   NC_004463.1:1,021,394-1,021,888
   - rpoN: product:   RNA polymerase sigma-54 factor 2
         Location   NC_004463.1:771,986-773,599
   - nhaD: product:   Na(+)/H(+) antiporter NhaD
         Location   NC_004463.1:4,147,856-4,149,133
   - tyrs: product:   Tyrosine--tRNA ligase
         Location   NC_004463.1:4,787,647-4,788,900

- Hypothetical Proteins
      Hypothetical proteins are genes that were predicted by annotation software (like Prokka), but they don’t match any known proteins in reference databases.
      We could get the gene's amino acid sequence and BLAST it (blastp) to see if newer databases had more information. 
            EX: Location   NC_004463.1:2,248,811-2,249,869

### **Step 6: Results Discussion**


