Original paper: https://arxiv.org/abs/1703.10593

## Environment

* TensorFlow & Python3

## Data preparing

* First, download a dataset, e.g. vangogh2photo
```bash
$ bash download_dataset.sh vangogh2photo
```

* Write the dataset to tfrecords
```bash
$ python build_data.py --X_input_dir data/vangogh2photo/trainA \
						--Y_input_dir data/vangogh2photo/trainB \
						--X_output_file data/vangogh2photo/vangogh.tfrecords \
						--Y_output_file data/vangogh2photo/photo.tfrecords
```

## Training

```bash
$ python train.py --X data/vangogh2photo/vangogh.tfrecords \
				   --Y data/vangogh2photo/photo.tfrecords \
				   --skip False
```
If the skip is set to be True, then it will use our improved CNN architecture which is explained in our report
To change other default settings, you can check 'train.py'


## Check TensorBoard to see training progress and generated images.
```
$ tensorboard --logdir checkpoints/${datetime}
```

## Export model
You can export from a checkpoint to a standalone GraphDef file as follow:

```bash
$ python export_graph.py --checkpoint_dir checkpoints/${datetime} \
                          --XtoY_model vangogh2photo.pb \
                          --YtoX_model photo2vangogh.pb \
                          --image_size 256
```

## Inference
After exporting model, you can use it for inference. For example:
```bash
python inference.py --model model/vangogh2photo.pb \
                     --input input_sample.jpg \
                     --output output_sample.jpg \
                     --image_size 256
```
More sample inference code are given in 'trans.txt' 

## Pretrained models
My pretrained models are in the 'model' document
