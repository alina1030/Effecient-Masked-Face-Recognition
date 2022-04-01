**Effecient-Masked-Face-Recognition**

**ABSTRACT**

 The COVID19 virus can be spread through contact and polluted surfaces. Many measures are needed to fight against the corona virus. One such measure is wearing a face mask. In the beginning stage, a face mask was not mandatory for everyone but as the situation worsened, scientist and doctors have recommended everyone to wear a face mask. So, to determine whether or not a person is wearing a face mask is an essential process to implement in the society. This can be used for various applications like at the malls, hospitals, offices, schools and other public places. Thus, the health and well-being of the society can be ensured. 
 
A neural network model is trained on a dataset. This dataset has two kinds of images namely with mask or without mask. The proposed model will consist of two parts. First part consists of a mask detector model to learn the difference between masked and unmasked faces. Second part will be the face detector model where it will input faces through a video stream and locate the face region. Once the face region is detected we apply the classifier model. The classifier model will predict whether there is “mask” or “no mask”. If the predicted label is “no mask”, then a warning message box is displayed and an email is sent to the concerned authority.

**METHODOLOGY**

**A. Mask Detector Model**

The proposed methodology consists of three parts. First 
part consists of a mask detector model. In this model, we
load a dataset which consists of masked and unmasked 
images. These images are first pre-processed. Pre-processing stage involves resizing of images into 224x224 
pixels and converting them to an array format. These are the 
new set of pre-processed images. They have corresponding 
set of labels as well. As the labels are stored in a textual 
format, the model cannot process the labels in such a format. 
So one-hot encoding must be done i.e. assign a numerical 
labels to these categories. The list of data along with the 
labels are converted to a numpy format. Neural networks 
can only work with an array format.


Now the data is ready to be segmented. Segmentation 
involves splitting data into train and test set. Some portion 
of the dataset can be taken as the training set and the other 
can be taken as the testing set. We also need to augment the 
images and this can be done by adding properties such as 
zooming, rotating, scaling, flipping etc. This process is 
important because it will help the model learn in a much 
better manner.

We make use of the MobileNet V2 model. This model 
consists of two parts namely basemodel and head model. 
We create a base model which makes of pre-trained set of 
weights knows as “imagenet”. Shape of the images are also 
passed into this model. The second layer is called the head 
model. The head model is a fully connected model placed 
on top pf the base model. The base model output is passed 
on to this model. Different layers are present here. Some of 
these are the dense layer which consists of 128 neurons, 
dropout layer which helps in preventing overfitting of the 
model, flattening layer which converts the pooled feature 
map to a single column that is passed to the fully connected 
layer.

These two layers are compiled and we pass in the 
augmented images as well to get more training data. The 
model gets trained to learn the difference between masked 
and unmasked images in the dataset.

**B. Face Detector Model**

The created mask detector model is loaded into the face 
detector model. Through an input video stream, we first 
input the images in the form of frames and grab the 
dimension of the frame and then construct a blob from it. 

We pass the blob through the network and obtain the face 
detections. Then, loop over the detections to extract the 
probability of the detection. If we detect a face, we compute 
the coordinates of the bounding box that need to be placed 
over the region of interest (ROI) and ensure that the 
bounding box coordinates do not fall out of the range of the 
frame. Once acquiring the face ROI, convert it from BGR to 
RGB channel, pre-process and resize it to 224x224. Once 
this is done, we have the face image and coordinates of the 
bounding boxes with us. 

Now the mask detector model is applied to this face ROI. 
The detector will determine whether a mask is present or 
not. If the mask is present, the corresponding label ie. 
“mask” along with the probability value will be displayed 
and if the mask is not present a warning message will be 
displayed alerting the person to wear a mask otherwise his 
access is denied. Simultaneously, an email notification is 
sent to the concerned authorities alerting that a person has 
violated the covid protocols.
