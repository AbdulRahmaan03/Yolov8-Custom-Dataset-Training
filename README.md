# Yolov8 Custom Dataset Training
- This repo can be used to train Yolov8 model for custom training on any class from the [Open Images Dataset v7](https://storage.googleapis.com/openimages/web/visualizer/index.html).
- Just change the class id in **create_image_list_file.py** and **create_dataset_yolo_format.py** files.
  - Right now it is set to [alpaca_id = '/m/0pcr'](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/d974d44746422ddc158835d42cf60f007f3fb4f4/prepare_data/create_image_list_file.py#L4).
  - You can change it to some other id based on the class from the [class description](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/main/prepare_data/class-descriptions-boxable.csv) file.


## Steps to create environment and install libraries
- Enter the following commands in anaconda prompt:
```
conda create -n yolo python=3.8 -y
```
```
conda activate yolo
```
```
git clone https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training.git
```
```
pip install -r requirements.txt
```
## Steps to download the dataset

1. Go to **prepare_data** directory and paste the following files after dowloading:
   ```
   cd Downloads\Yolov8-Custom-Dataset-Training\prepare_data
   ```
2. Download the [downloader.py](https://raw.githubusercontent.com/openimages/dataset/master/downloader.py) file.
3. Download the object detection dataset; [train](https://storage.googleapis.com/openimages/v6/oidv6-train-annotations-bbox.csv), [validation](https://storage.googleapis.com/openimages/v5/validation-annotations-bbox.csv) and [test](https://storage.googleapis.com/openimages/v5/test-annotations-bbox.csv).
4. Execute **create_image_list_file.py** to generate a list of image id's based on the class id.
   ```
    python create_image_list_file.py
    ```
5. Create a **images_all** folder in **prepare_data** directory.
   ```
    mkdir images_all
    ```
6. Execute **downloader.py** to download the images based on the list that was generated in the previous step.
    ```
    python downloader.py image_list_file --download_folder=images_all
    ```
7. Create **data** folder in **prepare_data** directory.
    ```
    mkdir data
    ```
8. Execute **create_dataset_yolo_format.py** to map the downloaded images with their respective annotations and then to convert this to YOLO training format.
    ```
    python create_dataset_yolo_format.py
    ```
## Steps to train
1. Create the [config.yaml](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/main/config.yaml) file in the main directory:
2. Step out of **prepare_data** directory.
    ```
    cd ..
    ```
3. Execute the following command:
    ```
    yolo detect train data=config.yaml model='yolov8n.yaml' epochs=100
    ```
## Steps to analyse results
1. A new folder called runs will be created in the main directory.
2. Go to runs -> detect -> train
3. Open [results.png](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/main/runs/detect/train2/results.csv) file and check if the loss graphs are descending.
4. View the model performance by opening [val_batch0_pred.jpg](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/main/runs/detect/train2/val_batch0_pred.jpg) file.

## Steps to evaluate model on mp4 video
1. Return to main directory.
2. Paste your video in [videos](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/tree/main/videos) folder.
3. Update video path in [predict_video](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/87235e0a977f4809c4a5b6e4de2f606e513baaba/predict_video.py#L9) file. 
4. Run **predict_video.py**
   ```
   python predict_video.py
   ```
5. You can then view the output video in [videos](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/tree/main/videos) folder.

> [YouTube Video Referred](https://www.youtube.com/watch?v=m9fH9OWn8YM)
