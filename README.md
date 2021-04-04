# Semantic-segmentation

Semantic segmentation is a task of labeling eaach pixel in an image to a class label. This can be interpreted as image classification at pixel level.

## Fully convolutional networks for semantic segmentation

The work in the following project aims to utilize the novel method proposed by Jonathan Long et al in the [CVPR 2015 FCN](https://arxiv.org/abs/1411.4038). The model can be used to do segmentation of all 7 classes, but due to GPU limitations it is used only for road pixels. The training is done on PASCAL dataset.

### FCNs

The FCN network trained end-to-end, pixel-to-pixel for the task of image segmentation is utilizes encoder-decoder architecture. The paper's authors propose adapting well known image classification network (eg Alexnet) for the encoder module and transpose comvolution layers for the decoder part to upsample the coarse feature maps into a full-resolutiona segmentation map. 


<p align="center">
  <img src="https://user-images.githubusercontent.com/51709130/113503822-fb340980-953c-11eb-964f-fd7bff8ca150.png">
  <br><br>
  <a href="https://arxiv.org/abs/1411.4038">Encoder</a> 
</p>

 The full network, as shown below, is trained according tp a pixel-wise cross entropy loss

<p align="center">
  <img width="460" src="https://user-images.githubusercontent.com/51709130/113503462-aee7ca00-953a-11eb-9bde-7c171e3c4219.png">
  <br><br>
  <a href="https://arxiv.org/abs/1411.4038">FCN</a> 
</p>

The encoder of the FCN as above, downsamples the inout image by a factor of 32, which creates a problem for decoder in creating fine-grained segmentations. To work around the limitation, 'skip connections' were added at different depths of the encoder and stitched to respective upsampled predictions as shown bellow

<p align="center">
  <img width="460" src="https://user-images.githubusercontent.com/51709130/113504090-7a760d00-953e-11eb-9d85-738f1ad52a33.png">
  <br><br>
  <a href="https://arxiv.org/abs/1411.4038">Skip connections</a> 
</p>


### Current work
Instead of proposed Alexnet in the paper, VGG network was used for encoding as shown bellow
<p align="center">
  <img height="800" src="https://user-images.githubusercontent.com/51709130/113504776-e8bcce80-9542-11eb-8064-55a9539272dd.png">
  <br><br>
  <a href="https://github.com/ashsne/semantic-segmentation/blob/master/semantic-segmentation.ipynb">Modified network</a> 
</p>

The model was trained for 10 epochs and the results can be observed as below
<p align="center">
  <img width="460" src="https://user-images.githubusercontent.com/51709130/113504809-389b9580-9543-11eb-8a93-780cfc401c9f.png">
  <br><br>
  <a href="https://github.com/ashsne/semantic-segmentation/blob/master/semantic-segmentation.ipynb">Results</a> 
</p>

