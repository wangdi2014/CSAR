CSAR
====
A contig scaffolding tool using algebraic rearrangements.

Description
------------
CSAR is a contig scaffolding tool that can efficiently and accurately scaffold the contigs of a draft genome (i.e., target genome) based on an incomplete reference genome of a related organism.

System requirements
------------
CSAR is developed in PHP. When running, it requires the program NUCmer or PROmer from MUMmer's package to first identify conserved genetic markers between target and reference genomes and then uses these markers to do its scaffolding job. To run CSAR, therefore, the following packages must be installed on your system and also available in your $PATH.

1. PHP (from 5.1.6): http://php.net/downloads.php
2. MUMmer: http://mummer.sourceforge.net/

After that, the following command can be used to install CSAR if git is available in your $PATH:

	git clone https://github.com/ablab-nthu/CSAR.git

Another alternative way is to download the zip file CSAR-master.zip and upzip it on your system. 

Usage
-----
Options of running CSAR:

```
-t <string>   Target genome (i.e., draft genome to be scaffolded)

-r <string>   Reference genome

--nuc         Use NUCmer to identify conserved genetic markers between target and reference genomes
 
--pro         Use PROmer to identify conserved genetic markers between target and reference genomes

-o <string>   Output folder to contain all the files returned by running CSAR (default: ./csar_out)

-h            Show help message

```
Note that the target and reference genomes should be prepared in multi-FASTA format, and either --nuc or --pro but not both shall be used in one command line. If the -o option is omitted, then a ./csar_out is used as default. The following is an example of running CSAR.

	php csar.php -t example/M.luteus_contigs.fna -r example/GCA_001691605.1_reference.fna --nuc -o example_output
	
Output
------
After running CSAR, it will generate the following files in the output folder:

* `scaffolds.nuc.csar` (if NUCmer is used) or `scaffolds.pro.csar` (if PROmer is used):

The above file lists all the scaffolds returned by CAR. These scaffolds are numbered arbitrarily and each of them contains ordered contigs and their orientations as exemplified as follows.
		
```
>Scaffold_1
<contig_name_a> <orientation_a>
<contig_name_b> <orientation_b>
<contig_name_c> <orientation_c>
...

>Scaffold_2
<contig_name_d> <orientation_d>
<contig_name_e> <orientation_e>
<contig_name_f> <orientation_f>
...	
```

Note that the orientation of a contig is represented by an integer number 0 or 1, where 0 indicates that the original (i.e., forward) orientation of the contig is used in the scaffold, while 1 indicates that the reverse orientation of the contig is used.


* `scaffolds.nuc.csar.fna` (if NUCmer is used) or `scaffolds.pro.csar.fna` (if PROmer is used):

The above file contains DNA sequences of scaffolds in multi-FASTA format. In this file, a stretch of 100 undetermined bases (N) serving as a spacer will be inserted between any two adjecent contigs in a scaffold with multiple contigs.

* `*.delta, *.filter, and *.coords`:

The above delta, filter and coords files are generated by NUCmer or PROmer. 

