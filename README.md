# Yolov8 Custom Dataset Training
- This repo can be used to train Yolov8 model for custom training on any class from the [Open Images Dataset v7](https://storage.googleapis.com/openimages/web/visualizer/index.html).
- Just change the class id in **create_image_list_file.py** file.
  - Right now it is set to [alpaca_id = '/m/0pcr'](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/d974d44746422ddc158835d42cf60f007f3fb4f4/prepare_data/create_image_list_file.py#L4).
  - You can change it to some other id based on the class from the [class description](https://github.com/AbdulRahmaan03/Yolov8-Custom-Dataset-Training/blob/main/prepare_data/class-descriptions-boxable.csv) file.
> [YouTube Video](https://www.youtube.com/watch?v=m9fH9OWn8YM)
## Steps to download the dataset

1. Go to **prepare_data** directory and paste the following after dowloading:
2. Download the [downloader.py](https://raw.githubusercontent.com/openimages/dataset/master/downloader.py) file.
3. Download the object detection dataset; [train](https://storage.googleapis.com/openimages/v6/oidv6-train-annotations-bbox.csv), [validation](https://storage.googleapis.com/openimages/v5/validation-annotations-bbox.csv) and [test](https://storage.googleapis.com/openimages/v5/test-annotations-bbox.csv).
4. Execute **create_image_list_file.py** to generate a list of image id's based on the class id.
5. Create a **data_all** folder in **prepare_data** directory.
6. Execute **downloader.py** to download the images based on the list that was generated in the previous step.

       python downloader.py $IMAGE_LIST_FILE --download_folder=<path_to_data_all_folder>
7. Execute **create_dataset_yolo_format.py** to map the downloaded images with their respective annotations and then to convert this to YOLO training format.

