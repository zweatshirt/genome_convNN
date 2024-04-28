# Convolutional Neural Networks for Genome Accessibility Classification in T-cells and Lymphoblasts.
- This is to determine the locations of accessible regions in a bio sample's chromatin.
- The cell types used in testing were T-cell and lymphoblast.
- ATAC-seq method was used for accessibility profiling of the assays.
- Provided a user has an ATAC-seq T-cell or lymphocyte sequence, they can feed the sequence to the trained model and the model will
attempt to classify the passed in sequence as being from an accessible or inaccessible region of chromatin.

- email me for the reference genome files if needed: zach7307@gmail.com

Testing was done in conjuction with a peer at SIUe under the supervision of Dr. Manas Jyoti Das.
Necessary data is first collected and cleaned extensively.

## Data preprocessing and prep
1. Bed files are collected from a collection of biosamples.
2. The bed files are parsed for the ranges of the features where the chromatin is accessible.
3. The mean length of these regions is collected for each bed file.
4. These bed files are fed into bedtools getfasta to return the sequences from the accessible regions.  
   This is done by the help of utilizing reference genome hg38.
5. These sequences from the accessible region provided by the bed file are then chopped by the mean length of the regions (i.e. the mean sequence length)
6. The sequences are then stored in files relative to their original bed file.
7. The accessible regions are then used to determine the inaccessible regions of the chromatin.
8. These inaccessible regions are then fed into bedtools getfasta to retrieve the sequences of the inaccessible regions.
9. All the sequences from the inaccessible region are chopped to the mean length of the accessible regions, and the mean length is unique per initial bed file.
10. The data is then chopped to the mean of means of all the mean lengths of the accessible regions of every file.
11. This data is then labeled (0 for negative i.e. inaccessible, 1 for positive i.e. accessible)
12. The data is then shuffled for randomization in preparation of entering the CNN, and stored in one large file.
13. The data is one-hot-encoded for the purpose of testing in the convolutional neural network.

## Networks
- The data from both cell types were passed into NiN (Network in Network) and AlexNet networks.
- The trained NiN models performed with an accuracy of 91-94%
- The AlexNet models performed with 96-97% accuracy.
- I made slight modifications to NiN with for determining lymphocyte chromatin accessibily, and ultimately found an increase in accuracy from 91% to 94% and a precision of 96%.


## Steps to run:
NOTE: You must be on a Linux machine for this project. 
NECESSARY:
1. Run `source setup_env.sh` (use Python 3.9 when prompted and ensure the environment is activated after running the script)
2. Run `./installs.sh`
3. Run `./get_beds.sh` and enter the path of the text file containing links to bed files. 
4. Run `./prep.sh`
<<<<<<< HEAD
=======
5. Run `python3 prep_seqs.py`
6. Run genome_conv.ipynb as a jupyter notebook and run the cells.

Note to self:
Refactor file structure.
>>>>>>> cd249b72b5f92eee5120e3edef8d89e902b2ac23