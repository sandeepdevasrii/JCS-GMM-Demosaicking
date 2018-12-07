# JCS-GMM-Demosaicking
The MATLAB codes corresponding to the letter 'Joint Color Space GMMs for CFA Demosaicking' published in IEEE Signal Processing Letters

## How To Run Demosaicking Experiments

Save the test images in the directory 'TestImages' and run the MATLAB script 'RunDemosaicking.m'. The demosaicked
results will be available in the directory 'Results'. Please see the following description about the directory
 structure and MATLAB files for more information. In our work, demosaicking experiments are carried out on the
images from three different databases. The links to theses databases are given below.
Kodak database - http://r0k.us/graphics/kodak/
IMAX (McMaster) database - http://www4.comp.polyu.edu.hk/~cslzhang/CDM_Dataset.htm
Laurent Condat's database - https://www.gipsa-lab.grenoble-inp.fr/~laurent.condat/imagebase.html

## How To Run GMM Training
-----------------------
Save the training images in the directory 'GMMTraining/ImageDatabase', and run 'GMMTraining/TrainGMM.m'.
The GMM parameters are stored in three '.mat' files, namely, 'ModelWeights.mat', 'ModelMeans.mat' and 
'ModelCovs.mat'. For more information about GMM Training, please see the separate ReadMe file available in the
directory 'GMMTraining'. In our work, the GMM parameters are learnt from the images available in the Berkley Segmentation database BSDS500, which can be downloaded from the link:
https://www2.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/


## Directory Structure
-------------------
All the MATLAB files required for reproducing the results reported in the paper mentioned above are
located in the root directory of this archive. The contents of the sub-directories included in this
archive are as follows:

1) Params:      This directory contains the JCS-GMM parameters learnt from an external database of clean
                natural images. The parameters are stored in MATLAB's .mat file format. This directory
                also contains the mask structures stored in .mat format. This is used to speed up the
                algorithm by avoiding the simulation of masks each time while running the algorithm.
                Presently, the masks correspond to the GRBG structure of the Bayer Pattern. The MATLAB
                function named 'CreateMask.m' located in this folder can be appropriately modified to
                simulate other CFAs.

2) TestImages:  The test images used for the demosaicking experiments must be stored in this directory. If you
                wish to use a different directory, please change the 'testdir' variable in the MATLAB script 
                'RunDemosaicking.m'. Presently, PNG files are used for running demosaicking experiments. If 
                you wish to use a different image file format, please modify line No. 9 of 'RunDemosaicking.m' accrodingly.				

3) Results:     The MATLAB code will store the demosaicked results in this directory.
			   
4) GMMTraining: This directory contains the MATLAB scripts for learning the JCS-GMM parameters from a
                database of color images. Please check the ReadMe.txt file contained in this directory for more information.

## MATLAB Files

A short description of the MATLAB files included in the root directory of this archive is given
below:

1) RunDemosaicking.m: This file can be executed to reproduce all the results corresponding to a given
                      database (Kodak, IMAX or Laurent Condat's database).

2) PatchEstimation.m: This file contains the MATLAB function corresponding to the Patch Estimation step
                      of the proposed JCS-GMM demosaicking algorithm.

3) ComputeZ.m:        Contains a subfunction used by the PatchEstimation step.

4) loggausspdf1.m:    This MATLAB function computes the posterior responsibility values of a given set of
                      full color concatenated patches.

5) loggausspdf2.m:    This MATLAB function computes the posterior responsibility values of a given set of
                      mosaicked concatenated color patches. The computation of posterior responsibilities
                      using the available pixels from a masked concatenated color patch requires that the
                      JCS-GMM parameters also to be masked accrodingly. The precomputed masked JCS-GMM
                      parameters corresponding to the four types of masks appearing in the Bayer pattern
                      speeds up the algorithm.

6) updateGMM.m:       The MATLAB function contained in this file performs the GMM Adaptation step
                      described in the paper.


7) myim2col.m:        This MATLAB function extracts concatenated color patch vectors from a given
                      color image.

8) Patch2Image.m:     The MATLAB fucntion contained in this file extracts the Red, Green and Blue patches
                      from the concatenated vectors, and average the overlapping patches from the respective
                      color channels.
