# Age-Progression

## Overview
The basic objective of the code is to be able to capture the analogy between an image and a filtered version of that image and then take that analogy and apply it on someother input image. This is then extended to be able to age a person if the analogy between the two input images is an age progression effect.

## Part 1 - Simple Analogy Transfer
Consider an 3 input images A, A', and B. We take each pixel of B and find the operation that must be taken on it so that pixel-by-pixel we are able to construct the output B'. We attempt to find a best match for each pixel in B with a pixel in A. This is done using two techniques. The **Best Approximate Match** will go through each pixel in A and compare the feature vectors of each pixel and the pixel selected in B using L2 norm. The feature vector is a list of attributes associated with each pixel such as luminosity and texture which make it a basis of comparison between pixels. Another technique is to find the **Best Coherent Match** which picks out a pixel from A which best matches with the neighborhood around the selected pixel in B by comparing the feature vectors of the pixels in the neighborhood. A parameter kappa is set to decide whether to use the Best approximate match or the Best Coherent Match. After a pixel is match the filter operation of the pixel in A to A' is matched to the pixel in B to obtain B'. 

## Examples of Simple Analogy Transfer
<img src="Images/blurA1.jpg" alt="Drawing" width="200" height="200"/><img src="Images/blurA2.jpg" alt="Drawing" width="200" height="200"/>

<img src="Images/blurB1.jpg" alt="Drawing" height="200"/><img src="Images/blurB2.jpg" alt="Drawing" height="200"/>

<img src="Images/pastelA1.jpg" alt="Drawing" height="200"/><img src="Images/pastelA2.jpg" alt="Drawing" height="200"/>

<img src="Images/pastelB1.jpg" alt="Drawing" height="200"/><img src="Images/pastelB2.jpg" alt="Drawing" height="200"/>

## Part 2 - Age Progression
Age Progression Required more localised feature mapping for each part of the face and then apply different operations for each feature. Some features chosen were: 
+ Forehead
+ Hair
+ Eyes
+ Undereyes
+ Upperlip
+ Cheeks
+ Lips
+ Chin
+ Underchin
+ Neck

The features were defined in both image A and B using a helper image in which each face component was mapped to a different color which made it easier for classification. The gradient of the aged input image is taken and compared with its younger self. The differences in the gradients are stored and and then a gradient is constructed for each feature part by considering only the region conrresponding to that part. Then the feature gradient of image A is morphed to fit the feature region of image B and the gradients are added to B'. The rest of B' is constructed by simple analogy transfer explained in part 1 in the localised feature regions. Special transformations are made for each part involving luminosity and color. Eg. The lips are made thinner, The chin and cheeks start to droop a bit, etc.

## Example of Age Progression
<img src="Images/youngA1.jpg" alt="Drawing" height="200"/><img src="Images/oldA2.jpg" alt="Drawing" height="200"/><img src="Images/coloredA.jpg" alt="Drawing" height="200"/>

<img src="Images/youngB1.jpg" alt="Drawing" height="200"/><img src="Images/oldB2.jpg" alt="Drawing" height="200"/><img src="Images/coloredB.jpg" alt="Drawing" height="200"/>

## Steps to Run
*Compile* using `opencv.sh`  
*Run* simple analogy transfer using `run.sh` 0 A A' B  
*Run* age progression using `run.sh` 1 A A' A'' B B''  
Here A'' and B'' are the colored feature images of A and B respectively

## Author
* [Nikhil Gupta](https://github.com/NikhilGupta1997)

Course Project under [**Prof. Prem Kalra**](http://www.cse.iitd.ernet.in/~pkalra/)
