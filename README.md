# commandF
Command ⌘ F - Project CheckPoint
16423 - Designing Computer Vision Apps Cheng-Yang Liu, chengyal

Summary: 
Inspired by the function Command F in personal computer, we developed an iOS-platform based scene text localization and recognition 
application, and display the results onto the screen of the mobile. Our text localization algorithm exploits the Class-specific Extremal 
Regions (ER) [1]. On the other hand, we take advantage of an open source optical character recognition (OCR) engine, Tesseract, for the 
text recognition part. At the end, we show some results both localization and recognition separately.

Introduction
In terms of recognition, Tesseract OCR is an open source optical character recognition engine with almost 100% accuracy on documentary 
images [2]. It is written in the C++, which is platform independent and compatible with Objective C++ in Xcode. However, regarding to 
scene text (without taken any specific prior action to cause its appearance or improve its positioning / quality in the frame [2]), 
traditional OCR systems perform poorly due to relying on brittle techniques, such as binarization.
Therefore, a better text extraction technique is required. Text localization can be computationally very expensive because in an image of 
N pixels generally any of its 2^N subsets can correspond to text. I choose Class-specific Extremal Regions method due to its less 
complexity (O(1)) to compute the features [1].
My results are shown as two applications. However, a comprehensive app can be expected in the future work by combining two implementations.

Text Localization
Extremal regions is constructed by thresholding the image by step-by-step increasing the value from 0 to 255 and then linking the obtained
connected components from successive levels in a hierarchy by their inclusion relation, and then we can form a component tree, Figure 1.
In order to efficiently select suitable regions among all the ERs, the method use of a sequential classifier with two differentiated 
stages.
In the first stage incrementally computable descriptors (area, perimeter, bounding box, and euler number) are computed (in O(1)) for each 
region r and used as features for a classifier which estimates the class-conditional probability p(r|character). The testing image extremal
regions are classified into character and non-character [6].
After the ER filtering is done on each input channel, I implement the method proposed by Luis Gomez and Dimosthenis Karatzas for grouping 
arbitrary oriented text [7]. This part has been done in OpenCV.

Text Recognition
Tesseract is probably the most accurate open source
OCR engine available. It can recognize more than 60 languages, combing with the Leptonica Image Processing Library [8]. I implement this 
OCR engine in the traditional OCR app.

Here is the link to my GitHub to the project. The project includes my self-built opencv2 framework that I added OpenCV extra module, 
which is not in official release. https://github.com/peterliu1212/commandF.git
Here is the link to my YouTube Presentation. This 16mins video has more detail about the project, background and implementation.
https://youtu.be/zAgGw-hS5PQ
