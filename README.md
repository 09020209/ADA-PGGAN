# ADA-PGGAN
Amounts of digital rock samples are crucial for studying pore properties. However, it is currently challenging due to equipment limitations or cost considerations. To address this issue, we propose sorts of reconstruction solutions under Data-Scarce Scenarios based on latent inversion predict from proposed generative model. Firstly, A novel featured distribution learning model was proposed  though O-ResNet50 network training for prepared inversion. During inversion, the    latent vectors predict from mentioned learning model is prepared to interpolate into latent space of given images. To stably produce high-quality images, Adaptive Data Augmentation Progressive Growing Generative Adversarial Network (ADA-PGGAN) is proposed, which includes a mechanism to supervise discriminator's overfitting and automatically adjust levels of data augmentation. Subsequently, interpolated latent vectors are input into the generator to progressively increase image resolution and reconstruct large-scale 3D digital rocks.Finally, evaluations using various metrics were conducted in both 2D and 3D on our results. The Sliced Wasserstein Distance (SWD) was used to assess our proposed data augmentation operation. The majority of SWD values remained below 0.01, with further decreases as resolution increased. Furthermore, generated images accurately exhibited core characteristics.We also evaluated our results in 3D with corresponding metrics, structural properties to indicate consistency with given samples

The datasets.py script allows you to prepare your datasets and build their corresponding configuration files： 
python datasets.py celebaHQ $PATH_TO_CELEBAHQ -o $OUTPUT_DATASET - f

ADA-PGGAN generates training for the model, running train.py in generate: 
python train.py PGAN -c config_celebaHQ.json --restart -n celebaHQ --np_vis


This project requires:
pytorch
torchvision
numpy
scipy
h5py (fashionGen)
For our data sets and pre-trained models, download them here:https: //drive.google.com/drive/folders/1ZvqJMX_jq-wynKw7iV_whJBcAo2bXRuu?usp=drive_link

1. ADA-PGGAN
We first trained a generation model of ADA-PGGAN, the data set is 500 binary slices of 1024×1024 size, saved to the folder 1024_slice_500, training command:
python train.py PGAN -c config_celebaHQ.json --restart -n celebaHQ --np_vis
The pre-trained ADA-PGGAN model is saved as network-snapshot-000600.pkl and can be called directly.

2.RVION
(1) Use ADA-PGGAN model to generate 50K data set and save its corresponding input noise as a label, and store it in folder gen_train50k as a training set of Resnet50.
(2) The training command line of Resnet50 model :python train.py, and the pre-trained model is saved as image_to_latent_ada.pt.
(3) Inversion of the specified image using encode_image.py, command line:
python encode_image.py
aligned_image.jpg
dlatents.npy
--use_latent_finder true # Activates model.
--image_to_latent_path ./image_to_latent_ada.pt # Specifies path to model.

3.Interpolation
Interpolate the potential vector obtained by RVION:python interpolation.py
