# YOLOV8-based-detection-segmentation-and-trackingObject Detection, tracking and segmentation assignment from perioko

## Problem statement:
Detection 3 objects, phone, tv and cup from source videos.
Track the detected objects.
Segment the detected objects

## Solution:
There are a lot of object detection, tracking and segmentation algorithms available in the field of computer vision to reach the goal. I have chosen yolov8 for below reasons:
Its state of art application and one stop go for all the requirements.
Different types of architecture are available for experimentation with a lot of variety in parameter tuning.
Integrity of visualization and accuracy measurement tools along with flexibility of CLI.
Availability of open source models and a great community to support.
Flexibility of fine tuning with additional data.
Availability of stream mode which helps in returning results as a generator function instead of list. Saves lots of RAM and can be used with a minimally configured system.   (It can run with 4GB Ram system with 4 GB graphics for interfacing)

## Code guide:
I have tried to make the codes self explanatory by nature. Discussing the environments and configurations used with reasoning here.
System: Colab with gpu/tpu (12GB RAM)
OS: Linux
Language: Python 3
Step by Step Code Guide:
1st we need to install ultralytics dependencies.
2nd we need to provide the files to be analyzed. Its can be done by using uploading the files in colab or by connecting drive to colab instance. I have connected the same directory as shared, so once you connect the drive please point out the directories as required.
Next we run the code to perform detection on individual video stacked in a directory. The code also allows us to produce the csv file as mentioned in the assignment. Csv files will be saved in root with the same name as the video file name. For step 2 and 3 the model used is yolov8n. Parameters are provided as per requirements which are discussed in the note section.
In this step we run the code to analyze a single video (combined video).
We move the results to drive using shutil.
Tracking on single video input performed. Model used yolov8n
Segmentation on single video is performed. Model used yolov8n-seg.

## Notes: 
I have used yolov8n, mainly because of its small size and quick runtimes. This model is trained on coco dataset enquiring which I have selected class ids=[41,62,67] which represents tv, cell phone and cup. Stream parameter is set to True to stop RAM bleeding and prevent system crash. The usage here helps return a generator object instead of a list when predicting the results. The data is then extracted and saved csv using pandas as per requirement.

## Future Improvements:
Observations:
It is obvious that the performance of the model could be fine tuned a lot. I have used the default confidence score which is 0.25. Watching the results it is clear a lot of detections are falling in the 0.30 to 0.60 range. Also occlusion is creating a lot of misdetection as usual. Also misclassification is happening when the object is very small compared to the image, for example in one scene the person carrying a cup is misdetected as a cellphone. Dark part of the videos are also not classified properly.
Probable Solution:
One can try with a slightly bigger version of yolov8 with bigger parameters provided with better hardware.
Fine tune the existing model with local data and annotation will improve the performance drastically.
For the occlusion part, segmentation based approach can help.
For the small object in a very big image sliding window based detection wrapper can be used, for example SAHI wrappers are very good examples to address this issue.
Some preprocessing on brightening the image in dark condition can be applied to gain superior detection on those dark scenarios.


