# [Humann2 tutorial](https://bitbucket.org/biobakery/biobakery/wiki/humann2)

**HUMAnN2**: HMP Unified Metabolic Analysis Network
* Tool for determining presence, absence, and abundance of metabolic pathways from metagenomic data

### Install HUMAnN2
* With Homebrew  
`$ brew tap biobakery/biobakery`  
`$ brew install humann2`

**Error message:**

`Last 15 lines from /Users/sophierowland/Library/Logs/Homebrew/metaphlan2/04.python2:
customize IBMFCompiler
Could not locate executable xlf90
Could not locate executable xlf
customize IntelFCompiler
Could not locate executable ifort
Could not locate executable ifc
customize GnuFCompiler
Could not locate executable g77
customize G95FCompiler
Could not locate executable g95
customize PGroupFCompiler
Could not locate executable pgfortran
don't know how to compile Fortran code on platform 'posix'
building 'dfftpack' library
error: library dfftpack has Fortran sources but no Fortran compiler found`

*Curse you Fortran!*

* Xcode does not include a Fortran compiler
* [gfortran maintainers](https://gcc.gnu.org/wiki/GFortranBinaries#MacOS)
    * Download and install gfortran 6.3
    * Retry `$ brew install humann2`
    * Didn't work
* [Alternative gfortran downloads for Mac](http://hpc.sourceforge.net/)
* Following instructions on [this page](https://www.macinchem.org/reviews/cheminfo/cheminfoMac.php)

#### Trying to install Fortran compiler
Following instructions on [this page](https://www.macinchem.org/reviews/cheminfo/cheminfoMac.php)
1. Installing relevant packages
  `$ brew install pkg-config`  
  `$ brew install subversion`  
  `$ brew install gcc` - already installed  
  `$ brew install boost --build-from-source`  
    * Taking a *really long* time
      * 23 minutes 21 seconds, to be exact
  `$ brew install tcl-tk`
2. Check for gfortran (as part of gcc)
  `$ man -k fortran`  
      `gfortran(1) - GNU Fortran compiler`  
  `$ which gfortran`
      `/usr/local/bin/gfortran`
3. Retry `$ brew install humann2`
  * **Same error message**

* With pip
`$ pip install humann2`
    * What's with msgpack?
    `Successfully built humann2
    distributed 1.21.8 requires msgpack, which is not installed.
    Installing collected packages: humann2
    Successfully installed humann2-0.11.1`

[HUMAnN2 User Manual](https://bitbucket.org/biobakery/humann2/wiki/Home)

* `$ brew install humann2 --without-dependencies`
    * Same error message...

**Note:** HUMAnN2 will require full nucleotide or amino acid search databases (not used in this tutorial)
* Chocophlan - nucleotides
* UniRef90 - amino acids

*For this tutorial*
`$ humann2_databases --download chocophlan DEMO humann2_database_downloads`  
`$ humann2_databases --download uniref DEMO_diamond humann2_database_downloads`

* Test local HUMAnN2 environment `$ humann2_test`
    * Doesn't match abbrev. version on tutorial but looks ok

**Maybe open an issue on humann2 repo**

### Install Metaphlan2
`$ export PATH=$PATH:~/software/metaphlan2/`  
`$ export PATH=$PATH:~/software/metaphlan2/utils/`  
`$ chmod +x ~/software/metaphlan2/`  
      *Changed location & name of metaphlan2 folder (6/26/18)*

## Metagenome functional profiling

*Note:* To view .tsv files like more Excel files use `column -t -s $'\t' file.tsv | less -S`
    * '$ alias tsview = "column -t -s $'\t' file.tsv | less -S"'

### HUMAnN2 input formats
* Acceptable input file types:
  * Quality controlled shotgun metagenomes or metatranscriptomes
      * fastq, fastq.gz, fasta, or fast.gz
  * Mapping results
      * sam, bam, blastm8
  * Gene abundance tables
      * tsv, biom

#### Download demo inputs
~/gitrepos/humann_tutorial

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/humann2/input/demo.fastq`  
`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/humann2/input/demo.sam`  
`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/humann2/input/demo.m8`

### Running HUMAnN2: the basics
`$ humann2 --input demo.fastq --output demo_fastq`

**Error message:**
`CRITICAL ERROR: The diamond executable can not be found. Please check the install.`

So...the installation was not successful.
