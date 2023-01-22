<h1 align="center"> Classification of pills according to production deficiency</h1>
<h2 align="center">See what the human cannot see </h2>

>Image

> __Note__
> About the project.
>
> this project is realized in a workshop in the presence of companies that offer real problems from the professional field to the participants in order to approach the real professional world to them.

<h1> $\textcolor{brown}{\text{I. context of this project :}}$ </h1>

  The company that proposed theis use case is a world leader in pill inspection systems for the pharmaceutical Industry. Its machines aim to eliminate the defects created by medication production lines: broken pills, stains, discolorations, printing or engraving problems. The defects targeted are of the order of 100 microns for the smallest ones. To perform this operation, the tablets are in single file on conveyors and cameras take color and 3D images of each drug. By image processing, they perform a real-time analysis to determine in real time if the tablet is good or bad. In the latter case, this machine eject the defective tablet from the production flow. The equipment allow them to reach very high production rates of 160 to 200 tablets per second for machines equipped with two inspection lines.

<h1> $\textcolor{brown}{\text{II. project objectives :}}$ </h1>

  In the context of AI-based in-line control of pharmaceutical tablets, the objective is to succeed in using Deep Learning models to correctly classify the images according to the type of defect present and to reduce the false detection rate compared to compared to conventional image processing. 
A powerful model has been developed this company with its collaborators and gives very good results with an accuracy of about 99.7%, however to reach this figure the model needs to be trained with 30,000 tablet images. Nevertheless, in order to reach this figure, the model needs to be trained with 30 000 images of tablets
including 15 000 good tablets and 15 000 defective tablets distributed on the different types of which represents a huge work for the user to label the 30 000 images without any forgetting the significant risk of error of such a manual operation. And this operation should be repeated with every pill production. 
It is necessary to understand that to have 30,000 defects of each type takes a lot of time because we are dealing with a hign precision industry and the defects are very rare and caused by maintenance problems specific to each defect. 
So, the objective of this work is to achieve the same result with only 1000 images of 500 good and 500 distributed on the different types of defects by using data augmentation methods or other methods. this improvement will help the company to train other models with less data and give them a financial advantage. 

<h1> $\textcolor{brown}{\text{II. Undestanding Data :}}$ </h1>

<h2> $\textcolor{Orange}{\text{II.1 Overall view of the machine}}$ </h2>
You will find below the operating principle of the high speed visual inspection and classification machine for pharmaceutical tablets 


>image

It is composed of the following subsystems: 

Top belt : A belt transports the tablets from the feeding device to the tablet turning system. 

>image 

Turning System: The tablets are turned using a wheel, the upper belt transports the tablets and holds them against the lower belt during the rotation and at the end of the rotation the tablets remain on the lower belt.

Lower belt: A second belt allows the rotation and transports the tablets to the exit. 

>image

<h2> $\textcolor{Orange}{\text{II.2 Vision stations :}$ </h2>

One line of the equipment has 2 RGB stations (each consisting of 5 matrix cameras) and 2 linear laser profilometers used to detect any type of aspect defects. 
- The 5 cameras and the laser placed on the upper belt are used to inspect the first side of the tablets.
- The 5 cameras and the laser placed on the lower belt are used to inspect the other side of the tablets - The 5 cameras and the laser placed on the lower belt are used to inspect the other side of the tablets after the tablets are turned over.
- Two ejection stations, one at the top and one at the bottom, blowing air, are used to reject the tablets as soon as as soon as one of the stations detects a defect. If a tablet is considered to be in conformity by all If a tablet is considered compliant by all the vision stations, it will be collected at the exit of the conveyor in a specific container.

<h2> $\textcolor{Orange}{\text{II.2 RGB station from which the images are taken :}$ </h2>

The RGB stations are composed of 5 matrix cameras trigged at the time when the tablet passes under the station, each of the two stations of the machine allows to have images of one side of the tablet. Pass under the station, each of the two stations of the machine allows to have images of a face of tablet (top of the tablet and the 4 upper corners for the station located on the upper belt and the bottom of the tablet and the 4 lower corners for the station located on the lower belt)

>Image 

When a tablet passes under an RGB station, 5 images of the face are taken in offset, this in order to be able to switch on the right lighting for each view. 

>Image



 
