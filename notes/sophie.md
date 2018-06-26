# Git Boot Camp
**Led by Kevin Bonham, PhD**

_Wednesday, June 6 2018_

_10:30 AM - ? PM_

_SCI 143_

## Set Up

1. [Git](https://git-scm.com/)
2. Python
    * Mac already has a system version of Python
    * To check version ...
3. [Homebrew](brew.sh)

    `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

4. Jupyter lab

    `$ brew install jupyter`

    `$ brew install python 2`

    `$ brew install python 3`

5. Biobakery
  * Metaphlan2
  * humann2
6. Text editor
  * [Atom](https://atom.io/)
  * [Sublime Text](https://www.sublimetext.com/)
  * [textwrangler](https://www.barebones.com/products/textwrangler/download.html) *not compatible with Mac OS 10.13 (High Sierra)*


## What is Git?
 **Git** = distributed version control system (dvcs)

 Allows you to keep track of the state of an entire folder

 **Repo** = folder, abbrev. repository

 **Commit** = snapshot of folder state

* git_tutorial-1/
  * notes/
    * sophie.md
    * danielle.md
    * kevin.md
  * bin/
    * myscript.py

_git_tutorial-1 because previously made git_tutorial_

### Organization of Repos
1. Local = own copy on your computer
2. Remote = another place to store files, like GitHub
3. Remote (upstream) = *Source of Truth*, main lab repo

## Terminal Tutorial
* Preview working directory = `$ pwd`
* Change directory = `$ cd {folder}/`
* Make directory  = `$ mkdir {new_folder}/`
* List files in directory = `$ ls` OR `$ ls -a`
* Remove folder = `rm -r git_tutorial` OR `rm -rf git_tutorial`
  * Use **sparingly**
* Move files and folders = '$ mv'
* View preview of file = `$ head`

### Create a remote repo
**_Don't do yet_**
`$ git remote add origin git@github.com:kescobo/git_tutorial.git`

## Create README.md file
`$ atom README.md`

*If using Atom text editor*

You created a new text file (.md = markdown)! You can save like a normal file but need to commit to add to local repo and push to remote repos.

Atom tracks your file status
* Green = not tracked by Git
* Yellow = tracked, but most recent version not committed

## Important Git Commands
* Create new repo = `$ git init {new_repo}/`
* Check status of local repo = `$ git status`
* Stage files = `$ git add {new_folder}/{filename}`
* Commit files = `$ git commit -m "Enter commit message here"`
    * `-m` = add message
* Push & set upstream = `$ git push --set-upstream origin master`
    * Push = `$ git push`
    * `origin master` = <remote repo name> <branch name>
* View commit history = `$ git log`
    * To make it look pretty `$ git log --graph --pretty=oneline --abbrev-commit`
* Create new branch = `$ git checkout -b {new_branch}`
* Check status of remote repo = `$ git fetch`
* Update local repo from remote repo = `$ git pull`
    * Specify which remote repo to pull from
* Set another remote repo = '$ git remote add upstream https://github.com/kescobo/git_tutorial.git'
    * "upstream" = repo name
    * https:// = url from clone or download on GitHub
* Pull from remote = `$ git pull`
    * Default pulls from "origin"
    * `$ git pull upstream master`
    * **Double-check** which branch you are on
* Make master branch match dev = `$ git checkout sophdev`
    `$ git merge master`

OR

* Make dev branch match master = `$ git checkout master`
    `$ git merge sophdev`

### Copy repo
1. Fork from origin on GitHub
2. Clone onto your computer
  * `git clone {insert url here}`

## **General Work Flow**
1. Make a branch  
      `$ git checkout -b {new_branch}`
2. Commit to branch  
      `$ git add {filename}`
      `$ git commit -m "Commit message"`
      `$ git push --set-upstream origin sophdev`
3. Pull request to upstream
        * Submit pull request on GitHub
        * Address comments
        * Commit and push any changes
        * **Do not merge yourself!** Kevin is in charge of merging pull request to upstream
    1. When merged, pull from upstream (_while in master branch_)  
        `$ git checkout master`  
        `$ git pull upstream master`
    2. Merge sophdev to master  
        `$ git checkout master`  
        `$ git merge sophdev`  
        *If doesn't work, switch sophdev and master*

# Biobakery
## Metaphlan2

### Install Metaphlan2
1. Go to [Biobakery](https://bitbucket.org/biobakery/biobakery/wiki/Home)
2. Click [Metaphlan2](https://bitbucket.org/biobakery/biobakery/wiki/metaphlan2)
3. Install
    * From Source
    `$ export PATH=$PATH:~/Downloads/biobakery-metaphlan2-e7761e78f362/`  
    `$ export PATH=$PATH:~/Downloads/biobakery-metaphlan2-e7761e78f362/utils`  
    `$ chmod +x ~/Downloads/biobakery-metaphlan2-e7761e78f362`  
    `which metaphlan2.py`  
    `metaphlan2.py -h`  
    * -h = help
    * If move from downloads, update PATH  
    `which bowtie2`

##  What is Metaphlan2 and What is it Used For
### Metagenomics
#### 16S rRNA Amplicon Sequencing
  1. Amplify through PCR
  2. NextGen Sequencing (Illumina)
  3. Output = fastq files (text file)
      * >identifier
      * AATCGCAT... (Genetic code)
      * +
      * FF-... (Quality Score)
  4. Computational analysis
      * clustering -> group similar sequences, counting
      * aligning -> compare to a reference database, classifying
          * Reference database only includes 16S rRNA sequences

#### Metagenomic Sequencing
  1. Sequence all DNA
  2. Output = fastq files
      * ~100-250 bps long
  3. Aligning to reference database
      * Includes full genomes
  4. Metaphlan2 calculates # of sequences aligning to reference genomes
      * Determine relative abundances  
**This method is only as good as your database**

### Metaphlan2 tutorial
1. Download files  
`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014476-Supragingival_plaque.fasta.gz
$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014494-Posterior_fornix.fasta.gz`
2. Run sample file  
`$ metaphlan2.py SRS014476-Supragingival_plaque.fasta.gz  --input_type fasta > SRS014476-Supragingival_plaque_profile.txt`
    * Error message:  
    `Traceback (most recent call last):
  File "/Users/sophierowland/Downloads/biobakery-metaphlan2-e7761e78f362/utils/read_fastx.py", line 9, in <module>
    from Bio import SeqIO
ModuleNotFoundError: No module named 'Bio'
Traceback (most recent call last):
  File "/Users/sophierowland/Downloads/biobakery-metaphlan2-e7761e78f362/utils/read_fastx.py", line 9, in <module>
    from Bio import SeqIO
ModuleNotFoundError: No module named 'Bio'
OSError: fatal error running '/Users/sophierowland/Downloads/biobakery-metaphlan2-e7761e78f362/utils/read_fastx.py'. Is it in the system path?`
