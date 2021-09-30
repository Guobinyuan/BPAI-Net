## Bidirectional Posture-Appearance Interaction Network for Driver Behavior Recognition



This repo holds the codes and models for the BPAI-Net framework presented on ???.

**Bidirectional Posture-Appearance Interaction Network for Driver Behavior Recognition**

author list

[[Paper]](http://openaccess.thecvf.com/content_ICCV_2019/papers/Zeng_Graph_Convolutional_Networks_for_Temporal_Action_Localization_ICCV_2019_paper.pdf)



# Get started


## Prerequisites

Install the runtime environment by running 

```bash
conda env create -f environment.yml
```



### Get the code

Clone this repo with git

```bash
git clone  https://github.com/SCUT-AILab/BPAI-Net
```

 

### Download Datasets

We support experimenting with two publicly available datasets for driver behavior recognition: Drive&Act and PCL-BDB. Here are some steps to download these two datasets.

Drive&Act: you can download it from the [Drive&Act website][drive&act].

PCL-BDB: We will release PCL-BDB dataset soon.



## Results

The recall scores of BPAI-Net with different backbone on Drive&Act.

| Model  |   Backbone   |  Recall |
| :----: | :----------: |  :----: |
|  BPAI-Net  | MobileNet V2 |   64.03  |
|  BPAI-Net  |   ResNet50   |  65.34  |
|  BPAI-Net  | Inception V1 |  67.83  |

The recall scores of BPAI-Net with different backbone on PCL-BDB.

| Model  |   Backbone   |  Recall |
| :----: | :----------: |  :----: |
|  BPAI-Net  | MobileNet V2 | 85.92  |
|  BPAI-Net  |   ResNet50   | 85.84  |

The BPAI-Net checkpoints with different backbone can be get from [here][checkpoints].



## Training BPAI-Net

Use the following commands to train BPAI-Net

```bash

train BPAI-Net with ResNet50 backbone on Drive&Act

python main_drive.py --arch fusion --arch_cnn resnet50 --num_segments 8  --xyc --first layer2  --dropout 0.8   --shift --mode train --root_model exp/test --root_log exp/test  --tune_from=pretrained/TSM_kinetics_RGB_resnet50_shift8_blockres_avg_segment8_e50.pth --gcn_pretrained=pretrained/st_gcn.kinetics.pt

train BPAI-Net with ResNet50 backbone on PCL-BDB

python main_drive.py --dataset pcl --arch fusion --arch_cnn resnet50 --num_class 40 --num_segments 8 --first layer2 --xyc --batch-size 8 --dropout 0.8 --shift --mode train --root_model exp/test --root_log exp/test --root dataset/pcl-bdb/ --skeleton_json dataset/pcl-bdb/video_pose --tune_from=pretrained/TSM_kinetics_RGB_resnet50_shift8_blockres_avg_segment8_e50.pth --gcn_pretrained=pretrained/st_gcn.kinetics.pt --pcl_anno 'annotation(2)(1).json'
```



## Testing Trained Models

 Use the following commands to test BPAI-Net

```bash

#test BPAI-Net with ResNet50 backbone on Drive&Act
python test_drive.py --arch fusion --arch_cnn resnet50 --num_segments 8 --xyc --first layer2 --shift --test_crops=1 --batch-size=8 --mode test --model_path tsm_new/exp/test/checkpoint.best.pth --root_log exp/test/

#test BPAI-Net with ResNet50 backbone on PCL-BDB
 python test_drive.py --dataset pcl --arch fusion --arch_cnn resnet50 --num_segments 8 --num_class 40 --first layer2 --xyc --test_crops=1 --batch-size=8 --mode test --model_path exp/test/checkpoint.best.pth --root_log exp/test --pcl_anno 'annotation(2)(1).json' --root dataset/pcl-bdb/ --skeleton_json dataset/pcl-bdb/video_pose
```

 More train and test commands refer to [script.sh][script].



## Citation

Please cite the following paper if you feel BPAI-Net useful to your research

```
reference
```

 

## Contact

For any question, please file an issue or contact

```
Gengqin Ni: gengqinni@gmail.com
Runhao Zeng: runhaozeng.cs@gmail.com
```

 

[**drive&act**]    https://www.driveandact.com/ 

[**pcl-bdb**]    https://pclbdb.netlify.app/ 

[**checkpoints**]    https://drive.google.com/drive/folders/1Oqpa0o5Dfkd8Qku3w25Ys69020aJk9CH?usp=sharing 

[**script**]  https://drive.google.com/drive/folders/1Oqpa0o5Dfkd8Qku3w25Ys69020aJk9CH?usp=sharing 