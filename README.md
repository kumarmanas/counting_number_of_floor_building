# Internship-Master-Thesis-Software-Engineering---Human-Machine-Interaction---Kumar-Manas

# House Floor counter using AI 
This project is developed to find no of floors in building by their RGB front image.

Note:Weight file after training can't be added here.You can get it from [here](https://drive.google.com/drive/u/1/folders/1aGmnB_nDbAfu-gIwyk4ZGcNwnjulHd9c) in my Google drive.

### Steps for preparing training image

1. Pip install labelImg tool [link](https://pypi.org/project/labelImg/). Use yolov3 option to start labelling the floors in each of the training image.
2. If you have 5 floor building, you will mark 5 segement of floors in that specific image and so on.
3. This will create a .txt file for each image. This file consists all cordinate of floor which you have labelled in that specific image.
4. Zip all images and .txt file together(my zip file name is "training_images.zip") and upload in Goggle drive by creating a folder(my folder name is "floor_counter") to be used for training.
5. Based on your name of file/folder path make necessary changes in training code.

### Steps for training:
1. Make a folder in Google drive (meine is "floor_counter" so code usage this name)
2. Paste your training image and their labels as Zip file. Here that is _"training_images.zip"_. So upload this file under folder "floor_counter".
3. Open Google colab(https://colab.research.google.com)
4. Select Runtime as GPU. You can find this option under "Runtime" on google colab.
5. Run the notebook _"Training_script.ipynb"_. Same can be acessed and run on cloud [here](https://colab.research.google.com/drive/16-y43-Yg9XF8QCamSnjv_9bTqiAIj_Gf?usp=sharing).
6. You will need Google drive acess permission for running first cell, so that training can acess zip file.
7. Go to cell which is running the training-"./darknet detector train data/obj.data.." and you can monitor the training progress.

    _**Note 1:**_ This training keep on saving weight file as backup from time to time in Google drive(same folder as training image zip)
_**Note 2:**_ If you want to change .cfg file which provides configuration for training. Go to cell starting with "!sed -i '. so for example if you want to change no of classes from 80(actual no of classes in YOLO) to 1 (only _floor_ needs to be detected here so one) on line no 610 of .cfg file, use command-
	!sed -i '610 s@classes=80@classes=1@' cfg/yolov3.cfg
_**Note 3:**_ No of filters in covolution works on formula [(no. of classes+5)*3]. So for our case its 18 for one class problem for our last layers of convolution.	
_**Note 4:**_ In Yolo we are not considering Training accuracy, but you can see training loss and plot it using log file or view while tarining was in progress. I stopped training when I saw loss ~0.15 you can go more further and use that weight for evaluation

### Steps for testing/inference: 
Will be done on local machine by runnig script "_"testing_script_on_trained_weights.ipynb"_"
Training is a one time process. So after this we are just going to use weights from training.
1. Download weights (latest weight or after 2000 iteration) from google drive and place it in the same folder as testing script and .cfg file. Likewise change this path in testing script _"testing_script_on_trained_weights.ipynb"_
2. Run testing script  by providing name of weight with its file path, name of image with its file path and name of config(.cfg) file with its file path respectively.
3. You can run target image or whole folder using regex expression.
4. Output print statement will give no of floors in image.
_**Note 1:**_ It can be possible that no of floor bounding box visible is not same as output print stament due to image resize and crop issue with that particular image. 
_**Note 2:**_ No of floors should be taken from script for better result rather than counting the detection box.
_**Note 3:**_ Detection is based on confiednce score that can be changed and played for more accuracy based on target image.

### Requirenment:
1. Google account to run Goggle colab
2. To run inference/testing- Try to use opencv version 4.x otherwise some CV DNN toolbox might not support
3. In case you want to use training in non linux machine there is a extra setup and software backlog like doc2unix and etc might be needed.
4. Linux VM or machine is prefeered with some tweaking in training notebook to train on local machine. Without GPU training time can be larger.  

### Quck start Guide:
To quickly start you can skip training and directly run your inference on local machine. You can download weights stored im my Google drive and just run testing script "testing_script_on_trained_weights". In below link you can find training and test images with weights stored-
https://drive.google.com/drive/folders/1aGmnB_nDbAfu-gIwyk4ZGcNwnjulHd9c?usp=sharing
Also you can directly run training script using my Google colab notebook hosted in cloud-
https://colab.research.google.com/drive/16-y43-Yg9XF8QCamSnjv_9bTqiAIj_Gf?usp=sharing

