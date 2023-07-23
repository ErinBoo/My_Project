# Classifying If a Plant is Healthy or Not

 This project is about identifying if a plant is healthy or not. The dataset I used was for veggies and fruits but by putting your image in you can identify your own plants.  

<img width="323" alt="Screen Shot 2023-07-23 at 1 53 06 PM" src="https://github.com/ErinBoo/My_Project/assets/140011304/32a2525c-345d-4ac4-a02f-6ed40cc981bd">


## The Algorithm

Jetson Nano was used to create this project and so was the retrained resnet18 model. A variety of fruits and veggies make up the dataset I used for this project. The plants are labeled by the type of plant, and if it has a disease, the type of disease. When it runs, it utilizes the imagenet.py tool and the model to identify the plant in the input image and decide whether or not it has a disease. 

<img width="616" alt="Screen Shot 2023-07-23 at 2 37 59 PM" src="https://github.com/ErinBoo/My_Project/assets/140011304/94dc6fab-395e-421b-a930-c98852490d1e">


## Running this project

**Training**
1. Make sure you have resnet-18 already downloaded onto your jetson.
2. All of the files in the GitHub should be downloaded onto the jetson, including all Python scripts that will be used.
3. On Kaggle find the data set called PlantVillage and download it
4. Then go to VS Code and change directories into jetson-inference/python/training/classification/data
5. unzip the file, by running "wget (the link you got from downloading) -O PlantVillage.tar.gz"
6. Then after you've done that go to the jetson-inference folder and run: ./docker/run.sh
7. Go back to jetson-inference/python/training/classification
8. To train the data, run the following: python3 train.py --model-dir=models/PlantVillage data/PlantVillage
9. Allow the resnet-18 model to train for at least 10 epochs, but the more training that is done, the better.
10. Make sure the data set is in VS Code in Nvidia/jetson-inference/python/training/classification/data

**Exporting the Model**
1. Make sure you are in the docker container and in jetson-inference/python/training/classification
2. Then run: python3 onnx_export.py --model-dir=models/PlantVillage

**Processing Images**
1. Exit the docker container by pressing Ctrl + D.
2. Then make sure you're still in jetson-inference/python/training/classification
3. Use ls models/PlantVillage to make sure that the model is on the nano. You should see a file called resnet18.onnx.
4. Then Set the NET and DATASET variables using these codes:
   - NET=models/cat_dog
   - DATASET=data/cat_dog
5. Then run: imagenet.py --model=models/PlantVillage/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=models/PlantVillage/labels.txt data/PlantVillage/Test/(Name of a Folder in your Test Folder)/(Name of picture in that folder).JPG (Any name you want for the picture).jpg
6. After that you should be able to find a picture in your models folder named after what you chose

[View a video explanation here](video link)
