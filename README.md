Introduction
============

This repository is designed to hold crowdsourced genomics data for data relating to the UK ash dieback epidemic of 2012. It is a generic data structure designed to hold multiple instances of genomics data and links to external sources of data too large to store on GitHub. You can clone it and add your own data and push it back to GitHub for inclusion. To clone it you'll need to get git setup on your machine and be granted membership of our github organization (ash-dieback-crowdsource).

If you want to join in just follow these instructions or get in touch through dan.maclean@tsl.ac.uk

How to use this repository
--------------------------

##getting access

- First of all, you need to set up git; github help has a pretty good [guide on how to do it](http://help.github.com/set-up-git-redirect). 
- Then you need a github account, [sign up here](http://github.com)
- Last you need membership of our github organisation, just email dan.maclean@tsl.ac.uk with your github username and I'll add you.


## contributing data to the repo
###inital setup: getting data on your machine using github clients

github now provide some pretty nice GUI-based clients for using git. They can be found at the following links

- [Windows](http://windows.github.com)
- [Mac](http://mac.github.com)

The help files on the client pages will give full instructions on how to clone our repo and how to push back. 

### initial setup: getting the data at your machine via the command-line

You need to clone the ash-dieback-crowd-source/crowdsrc repo on your local machine, by typing:

```git
    git clone git@github.com:ash-dieback-crowd-source/crowdsrc.git
```

After a few minutes (depending on your internet connection), you have all the contents of the repo stored locally on the newly-created `crowdsrc folder. Note that this is _only_ for first-time setup; you don't need to do this every time you want to add/get data.

### adding data locally

whenever you want to add data, first of all you need to get the most recent version of the remote copy:

```git
    git pull
```

Now, add anything you'd like to add on your local copy by just copying files/creating folders, and issue
            
```git
    git add <whatever-new-file/folder>
```

you're ready to commit the changes:
            
```git
    git commit -m 'a message explaining briefly the changes introduced'
```

### pushing your changes to the remote side

you just need to type

```git
    git push origin master
```
        
We're trying to keep this as simple as possible (no branches, forks, whatever). However, if you're new to this kind of stuff all of this can be rather daunting. The other option is:

## ask for help!

If you have your data at some publicly available URL, and you are unable/confident to follow the steps above, we'll be happy to upload the data for you: just send an email to dan.maclean@tsl.ac.uk  and we'll see what we can do.

The directory (folder) structure
-----------------------
The folders in this structure are designed to be semantically organised, so that you should be able to follow them and find what you want easily and intuitively. They start off like this:

	.
	|____ash_dieback
		|____chalara_fraxinea
		|____h_albidus
		|____h_pseudoalbidus
		|____fraxinus_spp
		|____project.info
		|____README
		|____org.README
		|____strain.README
		|____reads.README
		|____assembly.README
		|____alignments.README
		|____annotations.README
		|____project.README
	
The base folder is called `project_name`, and it contains the project level information. Immediately inside this folder is a file called `README` (which is the file you are reading), `project.info` (which contains the project level metadata), a load of files ending in `.README` that define the metadata required for datatypes lower in the structure and one folder each for however many organisms you will have in this project (here we have two, `org_1` and `org_2`). The names of the folders aren't important, only what they contain. So if you want to work on E.coli then you could rename one of the folders to `e_coli`.

###organism folders

The organism folder contains all information about just one organism, `h_pseudoalbidus` or `fraxinus_spp` or whatever. It should look like this:

	org_x
	|____org.info
	|____strain_1
	|____strain_2

Details about the organism are in the org.info metadata file, one of which is required for every organism in the project. `org.README` in the project folder contains details on the required metadata for the org.info file.

The organism folder also holds the strain folders, where `strain_x` is a particular strain or isolate and could be renamed to 0104_H4, K12 or whatever. `strain.README` is a file that specifies the metadata require for each strain.

###strain folders

These folders are where the actual data are. The enclosing folders exist really to help stop all the data sets from getting mixed up with themselves. Once in the strain folder we find specific datasets. Each strain folder contains two metadata files and 4 sub-folders.

	strain_x
	|____alignments
	|____annotations
	|____assemblies
	|____reads
	|____strain.info

The metadata file `strain.info` contains the metadata for the strain/isolate/ecotype analysed in this folder. The metadata are specified in the `strain.README` file in the project folder. One `strain.info` is required for every strain folder. Each sub-folder holds all the different datasets for the different types of genomic data in the repository. Just four types of dataset are identified, (alignments, annotations, assemblies and reads) but this could be extended by adding a new folder for a new datatype.


###data folders
The four different types of data folder are able to hold the majority of datasets we expect a genomics project will generate. There is nothing stopping you from creating new ones of your own.

####reads
This folder is designed to contain _links_ to the raw read files, e.g fastq files at other locations around the web. These files are too large in general, to be hosted via GitHub, but text links to them aren't. If you want the actual reads you should follow instructions in the `read_set.info` file which should explain how to get them as well as containing the metadata specified in `reads.README` in the project folder. Each read set should have its own folder and its own `read_set.info`.

####assemblies.
This folder is designed to contain the results of assemblies carried out with reads in the `reads` folder e.g fasta files of contigs or AGP files of assemblies. In most circumstances the fasta files will not be too big for GitHub so can be directly in the repository and not just linked. The assembly could be of genomic or transcriptomic assembly or anything else exotic along those lines. The details of how each of these assemblies was made should go in the `assembly.info` according to the specification in `assembly.README`.

####alignments
This folder designed to contain the results of alignments of one data set against another. Usually this will be reads in the reads folder to assemblies in the assemblies folder, but can be some other combination as required. It may contain links to large and unwieldy files, such as BAM, or directly contain text based alignments of reasonable size, e.g SAM or even BLAST output files.  The details of how each of these alignments was made should go in the `alignment.info` according to the specification in `alignment.README`.

####annotations
This folder is designed to contain the results of annotations of assemblies in the assemblies folder. Annotations is used in a broad sense and could include gene calls in GFF format, or just SNP calls in a proprietary text format. It may contain links to very large files stored elsewhere on the web as well as those directly in the repository. As in the other folders, `annotation.README` in the project folder contains details on the required metadata for the annotation.info file. Every annotation folder should have one `annotation.info` file.

####other data types - extending the directory structure
Extending the structure to hold data types we haven't thought of should be dead easy, just add a new folder in the strain folder. Make sure there is a .info file for the new datatype and a metadata definition in a .README file in the project_name folder

###File address 

With this data structure, each data file has a unique, semantic and (hopefully) logical place and address. For example:
`project_name/org_1/strain_1/alignments/strain1_vs_strain2/my_bam_file` or `crowd_sourcing/e_coli/k12/reads/bgi_sequenced_100_paired_150_insert/lane1.fq`


The .info files
---------------
The files ending in `.info` contain metadata describing the data according to the specification in `.README` files. Each `.info` should describe one discrete unit of data, so a `read_set.info` might describe one sequencing run or set of reads from a few lanes on a sequencer for which all the metadata are the same. Different read sets should be in different folders and therefore need different `.info`. For example, 
`crowd_sourcing/e_coli/k12/reads/bgi_sequenced_100_paired_150_insert/` would be different from 
`crowd_sourcing/e_coli/k12/reads/tgac_sequenced_150_single/` so would need a different `.info` though all the reads of that type would be in the same folder so would be covered by the same `.info`


The .README files and metadata standards
-----------------
`.README` files are a place to specify what should be captured by the individual `.info` files and are very project specific, so are kept blank in this empty repository. You'll need to decide what is appropriate at a project level.

Citations
---------
The idea for and layout of this repository borrows very heavily from the repository created for the [E.coli 0104:H4](https://github.com/ehec-outbreak-crowdsourced/BGI-data-analysis/wiki) outbreak of 2011, which was managed by

 [@ehec_data](http://twitter.com/#!/ehec_data),

 - [Eduardo Pareja-Tobes](https://github.com/eparejatobes)
 - [Marina Manrique](https://github.com/marina-manrique)


And I stole an awful lot of content from them to bootstrap this into place. Many thanks to them.