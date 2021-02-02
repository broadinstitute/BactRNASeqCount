# BactRNASeqCount


The scripts and codes in this repository have been used to determine the number of sequencing reads derived from features in bacterial genomes.

The gff_parse4.sh script converts .gff files to a list of features.  Below is an summary of feature types:

Features representing transcribed regions include all annotated protein coding sequences (CDS:), ncRNAs (ncRNAs:), miscellaneous RNAs (misc_RNAs), rRNAs (rRNA:), and tRNAs (tRNA:).  By default the boundaries of CDSs are extended 20 and 30 bp 5’ and 3’, respectively, to ensure that fragments aligning to the UTRs of mRNAs are assigned to their associated gene.  These extensions can be modified on the command line.  Intergenic features (IGR:) represent the intervening regions between annotated genes.  Each transcribed feature also has a cognate antisense feature (AS_*:) that corresponds to the opposite strand from which the feature is transcribed.  By default IGR features are assigned to the plus strand and AS_IGRS to the minus strand.  For fragments spanning 2 or more features, the fragment count for each feature is incremented by the fraction of the fragment length covering that feature.

The script is launched using the following command line:

sh gff_parse4.sh <.gff and .fna directory path> <output file directory> <temp file directory >  <# of bases to extend 5’ UTR> <# of bases to extend 3’ UTR> <accession number of .gff and .fna files>

Requirements:
1)	.gff and .fna accession IDs must match
2)	.gff and .fna file names must be exactly the accession number entered in the command line followed by the file type suffix
3)	This script was built based on .gff files generated prior to 2019.  Parsing .gff files with newer formatting may require modifications of the script and/or gff file
4)	The gff file must contain the following annotations:
a.	“locus_tag=”
b.	“gene=”
c.	“product=”
d.	“ID=”
5)	The feature types (field 3) must be one of the following:
a.	CDS
b.	tRNA
c.	rRNA
d.	miscRNA
e.	misc_RNA
f.	ncRNA
g.	tmRNA


The SAM_to_counts2.sh script uses FEATURE_COUNT_COORDS and SAM_PARSE to generate counts per feature from a feature file and SAM formatted sequencing read alignment file.  The scripts are designed to work with SAM files aligned using BWA but other aligners may work.  The accession header(s) of the fasta file used to align the sequencing reads should matech exactle to the accession(s) in the .gff file (field 1).

The script is launched using the following command:

sh / SAM_to_counts2.sh <path  to SAM file> <path to feature file> <path to directory where FEATURE_COUNT_COORDS and SAM_PARSE are located> <path to directory for temporary files> <path and name of file into which counts per feature will be written> 


