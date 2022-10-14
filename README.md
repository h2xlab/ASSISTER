[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]  

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/  
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg  


# ASSISTER: Assistive Navigation via Conditional Instruction Generation
This repository contains the dataset and code (avaliable soon) that accompanies our ECCV 2022 paper [ASSISTER: Assistive Navigation via Conditional Instruction Generation](https://eshed1.github.io/papers/assister_eccv2022.pdf).  

<p>
    <img alt="Example 1" src="images/example.PNG" class="fit"/>
</p>  

## Simulation Dataset  
We provide the [[Training](https://drive.google.com/drive/folders/1mME0GCE_WDm8yP13zk2-LcuXUETwh5Ii?usp=sharing)] and 
[[Testing](https://drive.google.com/drive/folders/1jHpYJfEYXAG4LjabB425REFjVyTbUu6R?usp=sharing)] dataset.     

### Overview  
Our simulation dataset contains 399,126 samples for training and 103,869 samples for testing. Among the testing samples, 36,615 samples are *new town new weather* (ntnw) setting, 36,378 are *new town same weather* (ntsw) setting, and 30,876 samples are *same town same weather* (stsw) setting.

### Data Format  
We provide train.json file contains all information need for training. Note that the json file is very similar to coco format but not identical.  
   
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
  
## Results  
<p>
    <img width=600 alt="Demo 1" src="images/demo.gif"/>
</p>  

## Contact us  
Please don't hesitate to contact us if you have any remarks or questions at sgzk@bu.edu.  

## License  
Our work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].  

## ToDos  
- [ ] Initial code release
- [ ] Real-world dataset release

