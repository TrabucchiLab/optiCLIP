# optiCLIP

A computational framework to analyse Ago2-CLIP data.

Please always use the last release!


***  Requirements. ***

Required Python libraries are:

- Bio.Seq 

- Scipy


Required programs installed and available in the path:

- Prinseq -> http://prinseq.sourceforge.net/

- Novoalign -> http://www.novocraft.com/products/novoalign/

- Homer -> http://homer.salk.edu/homer/

- Meme Suite -> http://meme-suite.org/doc/download.html


Genome sequences in fasta files are required as well. You can download them from UCSC web site or you can find them in Homer folder. 


***  Installation. ***


Just simply untar the package in any destination folder:


         tar zxvf optiCLIP_v1.0.tar ./


You'll find four folders:


./scripts: contains all scripts included in the pipeline

./example_data: contains input files needed to run the pipeline

./example_temp and ./example_output: folders to be used to run the pipeline on the example files




*** Using the optiCLIP pipeline. ***


You can use the command line script optiCLIP.py to run the whole data analysis pipeline from raw data to miRNA binding sites identification.



Input files: 


list fastq file: List with paths of all the fastq files to be analyzed.

genome index: to be done using "novoindex".

miRNA sequences file: a file with the most expressed miRNA in fasta format (DNA encoded mandatory). Alphabet to use: A,C,G,T. 



Examples files are provided in the example_data folder. 



         usage: python ./optiCLIP.py [options] [listfastqfile] [indexgenome] [mirnafastafile]



Options:


          -h, --help            show this help message and exit

          -o OUTDIR, --outdir=OUTDIR
                                directory for output files. Default is current directory.
          
          -t TEMPDIR, --tempdir=TEMPDIR
                                directory for temporary files. Default is current directory.
                                
          -d GENOMEFASTADIR, --genomefastadir=GENOMEFASTADIR
                                directory with genome fasta file. Default is current directory.
                                
          -b FASTABG, --fastaBG=FASTABG
                                file with background sequences in fasta format. If file is not provided, sequence scrumble will be done. Check Homer parameters for more details.
          
          -p PVALUE, --pvalue=PVALUE
                                pvalue threshold for peaks selection. Default is 0.001.
                                
          -r READS, --reads=READS
                                minimum number of reads for peaks selection. Default is 5.
                                
          -g GENOME, --genome=GENOME
                                Genome of the organism, either mm10 or hg19. Default mm10.
          
          -a ADAPTER3, --adapter3=ADAPTER3
                                Sequence of the 3' adapter. Default is empty string.
          
          -e ADAPTER5, --adapter5=ADAPTER5
                                Sequence of the 5' adapter. Default is empty string.

                        
Example procedure:
Download the fastq files from GEO database and put them in example_data/raw_data folder

          cd /home/optiCLIP/
          python ./optiCLIP.py -o /home/example_output/ -a TTCTACAGTCCGACGAT -e TTCTCGGGTGCCAA -t /home/example_temp/ -p 0.1 -r 2 -d /home/homer/data/genomes/mm10/ -g mm10  /home/example_data/example_file_fastq.list /home/mm10.idx /home/example_data/mirna_fasta_seq.txt


Output files:


* mapped reads onto the reference genome for each replicate

* sequence, coordinates and annotation of the consensus peaks 

* meme_motif: folder containing the motif selected with the combined score in meme format

* results_table.txt: A table containing the information about the heteroduplex and the duplex score. The table can be loaded on excel.


For questions/comments please drop us an email: silvia.bottini@unice.fr

