<h2>Tiled-ImageMask-Dataset-ORCA (Updated: 2024/04/28)</h2>
<li>2024/04/28: Added <a href="https://drive.google.com/file/d/1dke6ZBcC5tbFBne0yyz2IdQiwfK4n5uH/view?usp=sharing">
Tiled-ORCA-ImageMask-Dataset-V2.zip (Random-Shuffled Version)</a></li>
<br>
This is a simple Tiledly-Splitted ImageMask Dataset for Oral Cancer Image Segmentation.<br>
The dataset used here has been taken from the following web-site<br>
<b>ORCA: ORal Cancer Annotated dataset</b><br>
<pre>https://sites.google.com/unibas.it/orca/home</pre><br>
We have generated test, train, and valid datasets of 512x512 pixel-size from the original ORCA,
because the pixel-size of all images and masks of the dataset is 4500x4500, and too large to 
use for training of an ordinary segmentation model.<br> 
<br>
<hr>
<table>
<tr>
<td>
<b>Oral cancer image sample </b><br>
<img src="./samples/images/TCGA-CN-4723-01Z-00-DX1.13483e7b-9322-4d39-8cd6-91e898bf2ee9_0.png" width="512" height="auto">
</td>
<td>
<b>Oral cancer mask sample </b><br>
<img  src="./samples/masks/TCGA-CN-4723-01Z-00-DX1.13483e7b-9322-4d39-8cd6-91e898bf2ee9_0_mask.png" width="512" height="auto">

</td>
</tr>
</table>
<br>

<b>
You can download our 512x512 tiledly-splitted <b>Tiled-ORCA-ImageMask-Dataset</b> from the google drive

<li>
<a href="https://drive.google.com/file/d/1ILujbAFlycxGDieCR-TAi-Iu0afwKnNi/view?usp=sharing">
Tiled-ORCA-ImageMask-Dataset-V1.zip</a>

<li>
<a href="https://drive.google.com/file/d/1ILujbAFlycxGDieCR-TAi-Iu0afwKnNi/view?usp=sharing">
Tiled-ORCA-ImageMask-Dataset-V2.zip (Random-Shuffled Version)
</a>
</li>
</b>
<br>

<h3>1. Dataset Citation</h3>
<pre>
If you use the ORCA data, please cite:
F.  Martino,  D.D.  Bloisi,  A.  Pennisi,  M. Fawakherji,  G. Ilardi,  D. Russo,  D. Nardi,  S. Staibano, F. Merolla
"Deep Learning-based Pixel-wise Lesion Segmentation on Oral Squamous Cell Carcinoma Images"
Applied Sciences: 2020, 10(22), 8285; https://doi.org/10.3390/app10228285  [PDF]
</pre>
<br>

<h3>2. ImageMask Dataset Generation</h3>

If you would like to generate your own ImageMask-Dataset, please download the two original master datataset of  
<a href="https://drive.google.com/drive/folders/1XfplgYK5JWzzYWXQhrPUQujXNKUDK-WR">validation_100</a> 
and <a href="https://drive.google.com/drive/folders/1A_xiKTwBNO9XS_NzdDvWJNAx_z1nRnpS">test_100</a> in the following download page.<br> 
<a href="https://sites.google.com/unibas.it/orca/download">Download</a>,
and place the downloaded files under valid and test repectively.<br> 

Please run the following command for Python script <a href="./ImageMaskDatasetGenerator.py">ImageMaskDatasetGenerator.py</a>.
<br>
<pre>
> python ImageMaskDatasetGenerator.py
</pre>
This script splits *png and *_mask.png files in <b>valid</b> folder into images and masks folders under <b>./ORCA_master</b> as shown below.
<br>
<pre> 
./ORCA_master
├─images
│  ├─*.jpg
│  ├─*.jpg
│  └─,,,
└─masks
    ├─*.jpg
    ├─*.jpg
    └─...
</pre>


To create these new dataset <b>ORCA_master</b> with images and masks sub folders, all images and masks of the original dataset 
are resized to be 5120x5120 pixel-size from the original 4500x4500 pixel-size, and saved as jpg files.<br>
The pixel-size 5120,  which is larger than the original size 4500,  is selected to become an integral multiple of a tile-pixel-size 512
which is the size we would like to create.<br>

<h3>3. Split ORCA master</h3>

Please run the following command for Python <a href="./split_master.py">split_master.py</a> 
<br>
<pre>
>python split_master.py
</pre>
, by which test, train and valid subdatasets are created under <b>./ORCA-ImageMask-Dataset-X</b>.<br>
<pre>
./ORCA-ImageMask-Dataset-X
├─test
│  ├─images
│  └─masks
├─train
│  ├─images
│  └─masks
└─valid
    ├─images
    └─masks
</pre>
<hr>


Train images sample<br>
<img src="./asset/train_images.png" width=1024 heigh="auto"><br><br>
Train mask sample<br>
<img src="./asset/train_masks.png" width=1024 heigh="auto"><br><br>

<h3>4. Split ORCA-ImageMask-Dataset to tiles </h3>
Please run the following command for Python <a href="./ImageMaskTilesSplitter.py">ImageMaskTilesSplitter.py</a> 
<br>
<pre>
>python ImageMaskTilesSplitter.py
</pre>
, by which tiledly splitted  <b>./Tiled-ORCA-ImageMask-Dataset-V1</b> is created.<br>
<pre>
./Tiled-ORCA-ImageMask-Dataset-V1
├─test
│  ├─images
│  └─masks
├─train
│  ├─images
│  └─masks
└─valid
    ├─images
    └─masks
</pre>
<hr>
As shown below, each image and mask is splitted to 100-tiles of 512x512 pixel-size respectively.<br>
<br>
<b>Tiled train/image sample</b><br>
<img src="./asset/tiled_train_images.png" width="1024" height="auto"><br>
<b>Tiled train/mask sample</b><br>

<img src="./asset/tiled_train_mask.png"   width="1024" height="auto"><br>

Dataset Statictics <br>

<img src="./Tiled-ORCA-ImageMask-Dataset-V1_Statistics.png" width="512" height="auto"><br>


<h3>4. Random Shuffling </h3>
By exchanging the order of the master-splitting operation by <a href="./split_master.py">split_master.py</a> 
and the splitting-tiles operation by <a href="./ImageMaskTilesSplitter.py">ImageMaskTilesSplitter.py</a>, 
we created <a href="https://drive.google.com/file/d/1dke6ZBcC5tbFBne0yyz2IdQiwfK4n5uH/view?usp=sharing">
Tiled-ORCA-ImageMask-Dataset-V2.zip (Random-Shuffled Version).</a>
<hr>
Randomized train images sample<br>
<img src="./asset/randomized_train_images.png"  width="1024" height="auto"><br>
Randomized train masks sample<br>
<img src="./asset/randomized_train_masks.png"  width="1024" height="auto"><br>


