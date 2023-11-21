# ID-compare-translate


Classifying species of microorganisms by their genetic material is a fast-growing subfield of bioinformatics.
&nbsp;

I'll start by using blast to classify sequences of runs that attempt to connect the disease of Necrotizing enterocolitis a devastating complication of prematurity to microbial composition of the gut
(using data from the Human Microbiome Project, HMP, Demonstration Projects that contain 1065 sequencing runs).
&nbsp;

FTP site for the data:  https://ftp.ncbi.nlm.nih.gov/blast/db/v5/
&nbsp;

First, I got all the SRR runs for the project (1065 runs in total):
```BASH
esearch -query PRJNA46337 -db sra | efetch -format runinfo > runinfo.csv
```
&nbsp;

I investigated the file and saw that the first run id is SRR1614899. Next, I got the data for it. This command will produce 3 files –
importantly SRR1614899_3.fastq which contains the primary dataset and for data analysis.
&nbsp;

![aaa](https://github.com/programweb/ID-compare-translate/assets/12736699/feed6d4c-2127-470d-9e25-262058b39f3f)
&nbsp;

I convert the SRR1614899_3.fastq file to a .fasta file:
```BASH
seqtk seq -A SRR1614899_3.fastq >  SRR1614899.fa
```
&nbsp;

I made a database for this:
&nbsp;

![bbb](https://github.com/programweb/ID-compare-translate/assets/12736699/ed4a824d-252c-41f3-9bf0-3107c4e41724)
&nbsp;

![ccc](https://github.com/programweb/ID-compare-translate/assets/12736699/007f2901-a4c0-40f5-8ced-b178d890fd70)
&nbsp;

Now to align the converted sequence with blastn
&nbsp;

![ddd](https://github.com/programweb/ID-compare-translate/assets/12736699/ba7f901d-1f0b-4435-8268-72657371decd)
&nbsp;

The problem with this approach is it produces a huge file with > 87 million rows!
Each sequence may contain hundreds if not thousands of hits to all other similar 16S genes. 
Of course, since all 16S genes are similar to one another the resulting file is humongous. 
Obviously, the method is extremely redundant. 
Never-the-less, many publications do use blast to classify sequences.
&nbsp;

![eee](https://github.com/programweb/ID-compare-translate/assets/12736699/98862581-13d6-4d73-9de4-034a4bd66621)
&nbsp;

Visualizing the 16S classification (SRR1614899.blastn 4.44 GB file which zips to 377 MB) with the Metagenome Analyzer (MEGAN).
MEGAN can draw a taxonomical tree with the number of reads assigned to a rank.
The classification stops at the Family level.
&nbsp;

![Megan6](https://github.com/programweb/ID-compare-translate/assets/12736699/34f349a5-b337-4461-8e43-6b0de3c9920a)



&nbsp;

--- --- --- _I PLAN TO ADD STILL MORE TO THIS CODE SAMPLE IN THE NEAR FUTURE._ --- --- ---
&nbsp;

&nbsp;


**Map related genes across species**
&nbsp;

The
[g:Profiler g:Orth tool](https://biit.cs.ut.ee/gprofiler/orth "g:Profiler tool")
allows the user to map a list of genes (you can use gene-list.txt in this git repo) of interest to homologous genes in another related organism.

Here is an example use: getting the gene ortholog names of the mouse genome using a list of Human genes.
![top](https://github.com/programweb/ID-compare-translate/assets/12736699/6eefa1bf-6e31-451d-ae79-316adc6e63fb)
&nbsp;

[some rows not shown]
&nbsp;

&nbsp;

![bottom](https://github.com/programweb/ID-compare-translate/assets/12736699/e8c870ff-474d-4042-a750-0672771c33be)

