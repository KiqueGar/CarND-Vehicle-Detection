# **Vehicle Detection Project**

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier


[//]: # (Image References)
[image1]: ./output_images/colorspaces/YUV_Car[8185].jpg "YUV car"
[image2]: ./output_images/colorspaces/YUV_NonCar[8185].jpg "YUV nonCar"
[image3]: ./output_images/features_examples/Features[8185].jpg "Car features"
[image4]: ./output_images/features_examples/Features_nonCar[8185].jpg "Non car features"
[image5]: ./output_images/Long_distance.jpg "Long distance windows"
[image6]: ./output_images/Medium_distance.jpg "Medium distance windows"
[image7]: ./output_images/Short_distance.jpg "Neighborhood windows"
[image8]: ./output_images/Pipeline_example.PNG "Pipeline"
[image9]: ./output_images/non_max_supress.PNG "Pipeline with non max supression"
[image10]:
[video1]: ./project_video.mp4

## 1. HOG features and classifier.

First thing to try out was the use of different colorspaces, examples of
different channel separation for cars and not cars are located in
`output_images/colorspaces`.

![alt text][image1]
![alt text][image2]

As per visual examination, it seems like the YUV channel could be useful,
as it seems that car images have a greater dispertion than non cars, thus,
we´re using said channel.

As per spatial features and histogram bins, trial and error were used as to
find the best balance between execution time and accuracy.

9 orientations on HOG features are being used, as fewer got more false
positives.

Code for colorspaces is located in "Color spaces for classification" section
of the `.ipynb`

Code for feature extraction can be found on section "Basic functions" on 
`.ipynb`

### 1.2. Classifier

Results for the feature extraction are normalized using a normalizaer as can
be seen here:

![alt text][image3]
![alt text][image4]

With this features, a SVM classifier is trained on section "Model and training"
inside `.ipynb`

## 2. Sliding Window

A sliding window search was used, 3 sizes of window were used: (64,64), (72,72) 
and (128,128) as to detect closer, mid range and farther away objects, search areas can be seen here:

![alt text][image5]
![alt text][image6]
![alt text][image7]

Using the detector along the defined windows here are some examples of the pipeline:

![alt text][image8]

As for dupictaes trimming, Non maximum supression (section "Sliding windows
and non maximum supression") is used, resulting in:

![alt text][image9]



## 3. Video Implementation

A resulting video:

Here's a [link to my video result](https://youtu.be/V_8SWQt-V4A)

---

## Discussion

The pipeline assumes a correct placement of the window search, in this case,
placement was sone manually, in the furute, center of lane can be used,
however, a bad placement will derive in faulty detections.

A buffer for heatmap calculation is used, this buffer takes 30 frames,
so this pieline will fail if sudden changes appear.
