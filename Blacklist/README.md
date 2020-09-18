[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1491733.svg)](https://doi.org/10.5281/zenodo.1491733)

# The ENCODE Blacklist: Identification of Problematic Regions of the Genome

Functional genomics assays based on high-throughput sequencing greatly expand our ability to understand the genome. Here, we define the ENCODE blacklist- a comprehensive set of regions in the human, mouse, worm, and fly genomes that have anomalous, unstructured, or high signal in next-generation sequencing experiments independent of cell line or experiment. The removal of the ENCODE blacklist is an essential quality measure when analyzing functional genomics data.

## If you use the blacklists, please cite:
Amemiya, H.M., Kundaje, A. & Boyle, A.P. The ENCODE Blacklist: Identification of Problematic Regions of the Genome. Sci Rep 9, 9354 (2019). https://doi.org/10.1038/s41598-019-45839-z


# Available Blacklists
For those interested in using the blacklists, a current version for dm3, dm6, ce10, ce11, mm10, hg19, and hg38 are available in the `lists/` folder.

# System Requirements

## Hardware Requirements
Generation of the Blacklist requires a significant amount of RAM and disk storage based on the size of the genome analyzed and the number of input data files being processed. For minimal performance, we recommend a computer with the following specs:

RAM: 64+ GB  
CPU: 24+ cores, 3.4+ GHz/core

The runtime on this minimal system is approximately 192 CPU hours. Compile time is approximately 1.1 seconds.

## Software Requirements

The package development version is tested on *Linux* operating systems. The developmental version of the package has been tested on the following systems:

Linux: Ubuntu 18.04  

## Demo

We include a small demo file of an unmapped chromosome from mm10 (chrUn_GL456392). Execution time of this demo is approximately 0.025 seconds. The expected output is a bed annotation of a abnormal region across the entire segment:
```
cd demo
./Blacklist chrUn_GL456392
chrUn_GL456392	5200	23600	High Signal Region
```

# Installation
Clone a copy of the Blacklist repository and submodules:

```
git clone --recurse-submodules https://github.com/Boyle-Lab/Blacklist.git
```

Build bamtools API (please see bamtools documentation for more information)
Note: bamtools requires zlib to be installed
```
cd Blacklist/bamtools/
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX:PATH=$(cd ..; pwd)/install ..
make
make install
cd ../..
```

Build Blacklist
```
make
```

The blacklist software relies on a certain directory structure relative to the executable to function properly. All input data tracks should sorted and indexed bam files.
* Blacklist execuatable
   * input/ - folder containing all bam and bam.bai files
   * mappability/ - folder containing all uint8 Umap files
   
# Usage information
The blacklist is built on a per-chromosome or contig level. The following example will build a blacklist for a contig labeled chr1 and output the regions to chr1.bed:
```
./Blacklist chr1 > chr1.bed
```

# Historical blacklist information
(these lists are also available in the lists/ folder)
- HUMAN (hg19/GRCh38): http://mitra.stanford.edu/kundaje/akundaje/release/blacklists/hg38-human/hg38.blacklist.bed.gz
   ENCODE portal link: https://www.encodeproject.org/annotations/ENCSR636HFF/ (Select GRCh38)
- HUMAN (hg19/GRCh37): ENCODE portal link: https://www.encodeproject.org/annotations/ENCSR636HFF/ (Select hg19)
   UCSC Genome browser track http://genome.ucsc.edu/cgi-bin/hgFileUi?db=hg19&g=wgEncodeMapability
   README on how this track of generated: http://mitra.stanford.edu/kundaje/akundaje/release/blacklists/hg19-human/hg19-blacklist-README.pdf
- MOUSE (mm10): http://mitra.stanford.edu/kundaje/akundaje/release/blacklists/mm10-mouse/mm10.blacklist.bed.gz
   ENCODE portal link: https://www.encodeproject.org/annotations/ENCSR636HFF/ (Select mm10)
- MOUSE (mm9): http://mitra.stanford.edu/kundaje/akundaje/release/blacklists/mm9-mouse/mm9-blacklist.bed.gz
- WORM (ce10): http://mitra.stanford.edu/kundaje/akundaje/release/blacklists/ce10-C.elegans/ce10-blacklist.bed.gz
- FLY (dm3): http://mitra.stanford.edu/kundaje/akundaje/release/blacklists/dm3-D.melanogaster/dm3-blacklist.bed.gz

![ENCODE](https://www.encodeproject.org/static/img/encode-logo-small-2x.png) 
