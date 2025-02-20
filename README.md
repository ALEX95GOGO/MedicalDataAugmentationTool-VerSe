# Coarse to Fine Vertebrae Localization and Segmentation with SpatialConfiguration-Net and U-Net

## Usage
This code has been used for the Verse2019 and Verse2020 challenges, as well as the paper [Coarse to Fine Vertebrae Localization and Segmentation with SpatialConfiguration-Net and U-Net](https://doi.org/10.5220/0008975201240133). Look into the subfolders `verse2019` and `verse2020` for running the code and further instructions.  

## Required Packages
The required python packages include `tensorflow-gpu==2.2.0`, `SimpleITK==1.2.4`, `itk==5.1.1`, `scikit-image==0.17.2`, `tqdm==4.51.0`, `networkx==2.5`, `Pyro4==4.80`.

## Dataset preprocessing
Download the files from the [challenge website](https://verse2020.grand-challenge.org/) and copy them to the folder `verse2020_dataset/images`. The framework expects that the `.nii.gz` files are directly in the folder `verse2020_dataset/images`, e.g., `verse2020_dataset/images/GL003.nii.gz`. In order for the framework to be able to load the data, every image needs to be reoriented to RAI. The following script in the folder `other` performs the reorientation to RAI and Gaussian smoothing for all images:

`cd verse2020/other`

`python preprocess.py --image_folder ../verse2020_dataset/images --output_folder ../verse2020_dataset/images_reoriented --sigma 0.75`

## Landmark detection training
In the folder `training` there are the scripts for training the vertebrae localization networks. Currently they are set up to train the three cross-validation folds as well as train on the whole training set. If you want to see the augmented network input images, set `self.save_debug_images = True`. This will save the images into the folders `debug_train` and `debug_val`. However, as every augmented images will be saved to the hard disk, this could lead to longer training times on slow computers.
`module load cuda/11.6'

`set_env.sh'

`python training/main_vertebrae_localization.py`

## Landmark detection inference
`python inference/main_vertebrae_localization.py --image_folder /projects/MAD3D/Zhuoli/MICCAI/VerSe2020/MedicalDataAugmentationTool-VerSe/verse2020/verse2020_dataset/images_test --setup_folder /projects/MAD3D/Zhuoli/MICCAI/VerSe2020/MedicalDataAugmentationTool-VerSe/verse2020/verse2020_dataset/setup --model_files /projects/MAD3D/Zhuoli/MICCAI/VerSe2020/MedicalDataAugmentationTool-VerSe/verse2020/output/vertebrae_localization/spatial_configuration_net/fin_cv/0/FINAL/weights/ckpt-5000 --output_folder test_output'
## Citation
If you use this code for your research, please cite our [paper](https://doi.org/10.5220/0008975201240133) and the overview paper of the [Verse2019 challenge](https://arxiv.org/abs/2001.09193):

```
@inproceedings{Payer2020,
  title     = {Coarse to Fine Vertebrae Localization and Segmentation with SpatialConfiguration-Net and U-Net},
  author    = {Payer, Christian and {\v{S}}tern, Darko and Bischof, Horst and Urschler, Martin},
  booktitle = {Proceedings of the 15th International Joint Conference on Computer Vision, Imaging and Computer Graphics Theory and Applications - Volume 5: VISAPP},
  doi       = {10.5220/0008975201240133},
  pages     = {124--133},
  volume    = {5},
  year      = {2020}
}
```

```
@misc{Sekuboyina2020verse,
 title         = {VerSe: A Vertebrae Labelling and Segmentation Benchmark},
 author        = {Anjany Sekuboyina and Amirhossein Bayat and Malek E. Husseini and Maximilian Löffler and Markus Rempfler and Jan Kukačka and Giles Tetteh and Alexander Valentinitsch and Christian Payer and Martin Urschler and Maodong Chen and Dalong Cheng and Nikolas Lessmann and Yujin Hu and Tianfu Wang and Dong Yang and Daguang Xu and Felix Ambellan and Stefan Zachowk and Tao Jiang and Xinjun Ma and Christoph Angerman and Xin Wang and Qingyue Wei and Kevin Brown and Matthias Wolf and Alexandre Kirszenberg and Élodie Puybareauq and Björn H. Menze and Jan S. Kirschke},
 year          = {2020},
 eprint        = {2001.09193},
 archivePrefix = {arXiv},
 primaryClass  = {cs.CV}
}
```
