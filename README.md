[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]  

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/  
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg  


# ASSISTER: Assistive Navigation via Conditional Instruction Generation
This repository contains the dataset and code (available soon) that accompanies our ECCV 2022 paper [ASSISTER: Assistive Navigation via Conditional Instruction Generation](https://eshed1.github.io/papers/assister_eccv2022.pdf).  

<p>
    <img alt="Example 1" src="images/example.PNG" class="fit"/>
</p>  

## Simulation Dataset  
We provide the [[Training](https://drive.google.com/drive/folders/1mME0GCE_WDm8yP13zk2-LcuXUETwh5Ii?usp=sharing)] and 
[[Testing](https://drive.google.com/drive/folders/1jHpYJfEYXAG4LjabB425REFjVyTbUu6R?usp=sharing)] dataset.     

### Overview  
Our simulation dataset is collected using [CARLA](https://github.com/carla-simulator/carla). While [CARLA](https://github.com/carla-simulator/carla) is typically used for the development of autonomous driving policies, we modify the environment to collect instructional guidance and a sidewalk pedestrian perspective in various kinds of weather and towns. Overall, our simulation dataset contains 399,126 samples for training and 103,869 samples for testing. Among the testing samples, 36,615 samples are *new town new weather* (ntnw) setting, 36,378 are *new town same weather* (ntsw) setting, and 30,876 samples are *same town same weather* (stsw) setting.

### Data Format  
We provide [train.json](https://drive.google.com/file/d/1qRg6BiW3JVZZzHlydetZvvDglfeUnvX6/view?usp=sharing) which contains all the information needed for training. Note that the json file format is very similar to the coco format but not identical. The main difference is that we include the key: "goal" besides the "id" and "filename" in the list of images, and there exists multiple "id" map to one image "filename". This is because even with the same image, the instruction varies with different goals, and thus we cannot treat the images identically.   
   
```  
{    
  "info"         : [info],    
  "images"       : [image],    
  "annotations"  : [annotation],    
  "licenses"     : str,    
  "type"         : str,    
}     
    
info{    
  "year"         : int, 
  "version"      : str, 
  "description"  : str,    
}    
    
image{  
  "id"           : int,    
  "file_name"    : str,   
  "goal"         : [float, float],  
}    
    
annotation{  
  "id"           : int,  
  "image_id"     : int,  
  "caption"      : str,  
}  
```  
  
## Demo    
<p>
    <img width=900 class="center" alt="Demo 1" src="images/demo.gif"/ >  
</p>  

## Environment Setup
To run the code, you will need to install [py-bottom-up-attention](https://github.com/airsplay/py-bottom-up-attention/tree/master) and [Oscar](https://github.com/microsoft/Oscar).
### Installation
```
# Install py-bottom-up-attention
cd py-bottom-up-attention
pip install -r requirements.txt
pip install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'

# Install detectron2
python setup.py build develop

# install Oscar
cd Oscar/coco_caption
./get_stanford_models.sh
cd ..
python setup.py build develop
pip install -r requirements.txt
```
Note: We have made some modifications to the original repository. Please use our repository instead of cloning from the original one to ensure compatibility with our custom changes and configurations. 

## Training and Inference
The training process includes two stages: extracting features from images and training an image captioning model.
### Extract Features from Images
To extract features from images, please refer to the [**ASSISTER/py-bottom-up-attention/demo/extract_feature_sim.ipynb**](ASSISTER/py-bottom-up-attention/demo/extract_feature_sim.ipynb) notebook. This notebook is designed to work with our simulation dataset.
### Training an Conditional Instruction Generation Model
To train the image captioning model, you can use the following command:
```
python oscar/run_captioning.py --model_name_or_path pretrained_language_model_path --do_train --do_lower_case --evaluate_during_training --add_od_labels --learning_rate 0.00003 --per_gpu_train_batch_size 16 --num_train_epochs 500 --save_steps 2000 --output_dir your_output_directory --train_yaml train_config_file_path --data_dir dataset_path --val_yaml val_config_file_path --max_seq_length 90 --max_gen_length 40
```
You can download the pretrained language models from [Oscar Pre-trained Models](https://github.com/microsoft/Oscar/blob/master/DOWNLOAD.md)  
Make sure to replace the following placeholders with your specific information:  
- **your_model_path**: Replace this with the path to your pre-trained model.  
- **your_output_directory**: Set the directory where you want to save the model output and training results.  
- **train_config_file_path**: Provide the path to your train configuration file.  
- **dataset_path**: Specify the path to your dataset directory.  
- **val_config_file_path**: Enter the path to your validation configuration file.   
Adjust the other parameters (e.g., learning_rate, batch_size) as needed to suit your training requirements.  
### Inference
After successfully training and saving your model, you can perform inference and evaluate it on a testing dataset using the following command:
```
python oscar/run_captioning.py --do_test --test_yaml test_config_file_path --per_gpu_eval_batch_size 16 --num_beams 4 --max_gen_length 30 --eval_model_dir your_model_path
```


## Contact  
Please contact us if you have any remarks or questions at sgzk@bu.edu.  

## License  
Our work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].  

## ToDos  
- [X] Simulation dataset release
- [X] Training code release
- [ ] Real-world dataset release

