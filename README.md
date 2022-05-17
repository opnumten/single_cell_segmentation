citation link
https://www.sciencedirect.com/science/article/pii/S0010482519301143

The classification FCN is modified based on the code from  https://github.com/imlab-uiip/keras-segnet
The faster R-CNN is modified based on the code from  https://github.com/yhenon/keras-frcnn

weights file can be found in https://drive.google.com/drive/folders/1RBuebNQGxEQ-JSrOON3-R7Y8XOB9pftk?usp=sharing

================================================================================
# single_cell_segmentation

This single cell segmentation method is a multistep, sequential method.
Manually segmenting cells is a physically taxing and time consuming process.
By combining multiple methods, we attempted to create a fast and accurate pipeline for automatically segmenting cells.


The first step in this method is the Euclidean distance transform. In deep_distance_estimator.ipynb, raw data for training should be located at path_train_input and training labels should be located at path_train_gt. During training, comment out prediction. Once weight file has been created, you can then comment out training and load weight file with any raw data you wish to perform Euclidean distance transform on.


The next step is to train the cell detector. To train the model use train_frcnn.ipynb. Using the Euclidean distance transform data as opposed to raw data has yielded much more accurate results. Euclidean distance transofrm data should be located at "Images" and training labels should be located at "Annotations" (see wwk_parser.py). In order to then use the trained model, use frcnn_apply.ipynb and load weights and input Euclidean distance transform data for prediction. The output of this prediction will be saved at "/bndbox.txt".


Finally, using watershed_boundingbox.ipynb we input the Euclidean distance transform data as the subject of segmentation and the detector, bounding box data as the seeds. Distance transform images should be located at ori_img_path and bounding box data should be located at "bndbox.txt". The result is segmentation on distance transform data using traditional watershed method with frcnn detection data as the seeds.
