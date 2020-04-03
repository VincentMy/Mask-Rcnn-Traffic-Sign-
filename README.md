# Mask-Rcnn-Traffic-Sign-
# Datasets
The dataset of traffic sign can load from <br>
[Chinese Traffic Sign Database](http://www.nlpr.ia.ac.cn/pal/trafficdata/recognition.html)<br>
[Tsinghua-Tencent 100K Tutorial](https://cg.cs.tsinghua.edu.cn/traffic-sign/)<br>
[DiDi](https://outreach.didichuxing.com/d2city/challenge)<br>
[ApolloScape Dataset](http://apolloscape.auto/index.html)<br>
[LISA](http://cvrr.ucsd.edu/LISA/datasets.html)<br>
# Labelme
Due to these datasets are not that prefect ,I labeled hundreds of images to fit my model with labelme.<br>
1、Install labelme.The soures code and the install tutorial can find from [labelme](https://github.com/wkentaro/labelme) <br>
2、Label your image and get a json file
3、use the command of "labelme_json_to_dataset <file-name>.json", after that you can get four files which is *.png, info.yaml , label.png, label_viz.png.<br>
4、To deal with batch file of json, you can use the following command:<br>
```shell
#!/bin/bash
let i=1                   
path=./        	                    # The path of json，the json file and the shell in the same directory ./ 
cd ${path}
for file in *.json                  # loop json file
do
    labelme_json_to_dataset ${file} # transform json file to image
    let i=i+1
done
```
5、Load the file img.png、info.yaml、label.png use the following code:<br>
```python
import os
import shutil
filename = "mask"                                   # The file that json transformed
fileList = os.listdir(filename)
fileList.remove(".DS_Store")

for i in range(len(fileList)):
    img_source = "mask/" + fileList[i] + "/img.png"
    mask_source = "mask/" + fileList[i] + "/label.png"
    yaml_source = "mask/" + fileList[i] + "/info.yaml"

    img_target = "pic/img_{}.png".format(i)
    mask_target = "orig_mask/label_{}.png".format(i)
    yaml_target = "yaml/info_{}.yaml".format(i)

    shutil.copy(img_source, img_target)
    shutil.copy(mask_source, mask_target)
    shutil.copy(yaml_source, yaml_target)
```
# Train with mask-rcnn
The detail of the code can read from the file named traffic_sin.py.
