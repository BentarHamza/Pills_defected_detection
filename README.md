<h1 align="center"> Classification of pills according to production deficiency</h1>
<h2 align="center">See what the human cannot see </h2>

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/Firstpicture.PNG">
</p>

> __Note__
> About this project.
>
> this project is realized in a workshop in the presence of companies that offer real problems from the professional field to the participants in order to approach the real professional world to them.

--------------------------------------
<h1 align="center"> Summary </h1>

## I. context of this project 
## II. Project objectives 
### II.1 Overall view of the machine
### II.2 Vision stations 
### II.3 RGB station from which the images are taken 
### II.4 Organization of training and test images  
## III. building the model 
### III.1 Model for detecting the six types of defects 
#### III.1.1 Approach 
#### III.1.2 Results 
### III.2 Model for detecting the six types of defects and the 3 classes of defects (16 classes) 
### III.3 Perspectives for the development of the model 
------------------------------------

# I. context of this project :

  The company that proposed theis use case is a world leader in pill inspection systems for the pharmaceutical Industry. Its machines aim to eliminate the defects created by medication production lines: broken pills, stains, discolorations, printing or engraving problems. The defects targeted are of the order of 100 microns for the smallest ones. To perform this operation, the tablets are in single file on conveyors and cameras take color and 3D images of each drug. By image processing, they perform a real-time analysis to determine in real time if the tablet is good or bad. In the latter case, this machine eject the defective tablet from the production flow. The equipment allow them to reach very high production rates of 160 to 200 tablets per second for machines equipped with two inspection lines.

 # II. Project objectives :

  In the context of AI-based in-line control of pharmaceutical tablets, the objective is to succeed in using Deep Learning models to correctly classify the images according to the type of defect present and to reduce the false detection rate compared to compared to conventional image processing. 
A powerful model has been developed this company with its collaborators and gives very good results with an accuracy of about 99.7%, however to reach this figure the model needs to be trained with 30,000 tablet images. Nevertheless, in order to reach this figure, the model needs to be trained with 30 000 images of tablets
including 15 000 good tablets and 15 000 defective tablets distributed on the different types of which represents a huge work for the user to label the 30 000 images without any forgetting the significant risk of error of such a manual operation. And this operation should be repeated with every pill production. 
It is necessary to understand that to have 30,000 defects of each type takes a lot of time because we are dealing with a hign precision industry and the defects are very rare and caused by maintenance problems specific to each defect. 
So, the objective of this work is to achieve the same result with only 1000 images of 500 good and 500 distributed on the different types of defects by using data augmentation methods or other methods. this improvement will help the company to train other models with less data and give them a financial advantage. 

# II. Undestanding Data :

## II.1 Overall view of the machine:
You will find below the operating principle of the high speed visual inspection and classification machine for pharmaceutical tablets 

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/PrincipeFonctionnement.PNG">
</p>


It is composed of the following subsystems: 

Top belt : A belt transports the tablets from the feeding device to the tablet turning system. 

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/uperbelt.PNG">
</p>

Turning System: The tablets are turned using a wheel, the upper belt transports the tablets and holds them against the lower belt during the rotation and at the end of the rotation the tablets remain on the lower belt.

Lower belt: A second belt allows the rotation and transports the tablets to the exit. 

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/lowerbelt.PNG">
</p>

## II.2 Vision stations :

One line of the equipment has 2 RGB stations (each consisting of 5 matrix cameras) and 2 linear laser profilometers used to detect any type of aspect defects. 
- The 5 cameras and the laser placed on the upper belt are used to inspect the first side of the tablets.
- The 5 cameras and the laser placed on the lower belt are used to inspect the other side of the tablets - The 5 cameras and the laser placed on the lower belt are used to inspect the other side of the tablets after the tablets are turned over.
- Two ejection stations, one at the top and one at the bottom, blowing air, are used to reject the tablets as soon as as soon as one of the stations detects a defect. If a tablet is considered to be in conformity by all If a tablet is considered compliant by all the vision stations, it will be collected at the exit of the conveyor in a specific container.

## II.3 RGB station from which the images are taken :

The RGB stations are composed of 5 matrix cameras trigged at the time when the tablet passes under the station, each of the two stations of the machine allows to have images of one side of the tablet. Pass under the station, each of the two stations of the machine allows to have images of a face of tablet (top of the tablet and the 4 upper corners for the station located on the upper belt and the bottom of the tablet and the 4 lower corners for the station located on the lower belt)

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/PBG%20.PNG">
</p> 

When a tablet passes under an RGB station, 5 images of the face are taken in offset, this in order to be able to switch on the right lighting for each view. 

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/PBG%20.PNG">
</p> 

## II.4 Organization of training and test images  : 

The images are taken on the 5 cameras and organized according to the type of defect and its severity: 

Types of defects:

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/Coating_Defects.PNG">
</p> 
<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/Edge_defects.PNG">
</p> 
<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/chip_broken_coated.PNG">
</p> 
<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/chip_broken_uncoated.PNG">
</p> 
<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/logo_defects.PNG">
</p>
 

Severity of defects: 

Class  |  explanation |
--- | --- |
Class I | High risk of complaint and risk of impact on the patient |
Class II | Risk of complaint, no risk for the patient |
Control | Low risk of complaint, no risk to the patient |

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/class_defect.PNG">
</p>

# III. building the model :
## III.1 Model for detecting the six types of defects :
### III.1.1 Approach :
Our approach was to build a model from scratch and compare it with pre-established models in <a href="https://www.tensorflow.org/api_docs/python/tf/keras">Module TENSORFLOW KERAS</a> in order to detect the six type of defects without detecting the 3 classes of defects. 

the best model is the result of simulation of several models (by experiment). this model is feeded with data from <a href="https://www.analyticsvidhya.com/blog/2020/08/image-augmentation-on-the-fly-using-keras-imagedatagenerator/">ImageDataGenerator class </a> that provides a quick and easy way to augment your images. It provides, in addition,  a host of different augmentation techniques like standardization, rotation, shifts, flips, brightness change, and many more. 
However, the main benefit of using the Keras ImageDataGenerator class is that it is designed to provide real-time data augmentation. Meaning it is generating augmented images on the fly while our model is still in the training stage. How cool is that!

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/BestModel.PNG">
</p>

We detect that our data are unbalanced because the type **Good** has 400 images and other types has 500 images. this imbalance effected our result so we use class weights balance our dataset.

### III.1.2 Results :

the result can be summarized as follows 

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/accuracy.PNG">
</p>

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/loss.PNG">
</p>

<p align="center">
<img src ="https://github.com/BentarHamza/Pills_defected_detection/blob/main/Photo/confusionMatrix.PNG">
</p>

>__interpretation :__
>
>It's difficult to have a good result (greater than 90%) with this number of dataset giving from this client with classical method of data augmentation (rotation, shifts, flips ...).

## III.2 Model for detecting the six types of defects and the 3 classes of defects (16 classes) :
this model will be shared with you after finishing the notebook. 

## III.3 Perspectives for the development of the model :

- Using new techniques of data augmentation like generative adversarial networks.
- Using a transfert learning using model trained by 30,000 images and add some layers to specific tablets. 

