# Cell_Detection
Cell Detection with [Scaled YOLO V4](https://github.com/WongKinYiu/ScaledYOLOv4)

**Original image size:** 2448 x 1920

**Partitioned image size:** 204 x 192 sized image -> 120 images

 1795  slice-image -d ./TEST -r 10 -c 12 10_01_23032021_172718.jpg
 
 1796  slice-image -d ./TEST -r 10 -c 12 10_02_23032021_172718.jpg
 
 ...
 
 1814  slice-image -d ./TEST -r 10 -c 12 10_20_23032021_172718.jpg

 1819  slice-image -d ./TEST -r 10 -c 12 4_01_23032021_171004.jpg
 
 1820  slice-image -d ./TEST -r 10 -c 12 4_02_23032021_171004.jpg
 
 ...
 
 1838  slice-image -d ./TEST -r 10 -c 12 4_20_23032021_171004.jpg


**Train:**

python train.py --img 416 --batch 64 --epochs 100 --data '../data.yaml' --cfg ./models/yolov4-csp.yaml --weights '' --name yolov4-csp-results --cache


python train.py --img 204 --batch 64 --epochs 200 --data '../data.yaml' --cfg ./models/yolov4-csp.yaml --weights '' --name yolov4-csp-results --cache


Image size 204 is resized to 224


**Test:**

python test.py --img-size 416 --conf-thres 0.001 --batch-size 8 --data ../data.yaml --weights ./runs/exp6_yolov4-csp-results/weights/best_yolov4-csp-results.pt

Scanning labels ../valid/labels.cache (353 found, 0 missing, 391 empty, 0 duplicate, for 744 images): 100%|█| 744/744 [00:00<0

               Class      Images     Targets           P           R      mAP@.5  mAP@.5:.95: 100%|█| 93/93 [00:05<00:00, 17.5
               
                 all         744         437       0.795       0.995       0.977       0.651
                 
Speed: 3.8/1.0/4.8 ms inference/NMS/total per 416x416 image at batch-size 8



python test.py --img-size 224 --conf-thres 0.001 --batch-size 8 --data ../data.yaml --weights ./runs/exp7_yolov4-csp-results/weights/best_yolov4-csp-results.pt

Scanning labels ../valid/labels.cache (353 found, 0 missing, 391 empty, 0 duplicate, for 744 images): 100%|█| 744/744 [00:00<0

               Class      Images     Targets           P           R      mAP@.5  mAP@.5:.95: 100%|█| 93/93 [00:04<00:00, 20.4
               
                 all         744         437       0.874       0.986       0.983       0.674
                 
Speed: 3.5/0.6/4.1 ms inference/NMS/total per 224x224 image at batch-size 8


python test.py --img-size 416 --conf-thres 0.001 --batch-size 8 --data ../data.yaml --weights ./runs/exp8_yolov4-csp-results/weights/best_yolov4-csp-results.pt

Scanning labels ../valid/labels.cache (353 found, 0 missing, 391 empty, 0 duplicate, for 744 images): 100%|█| 744/744 [00:00<0

               Class      Images     Targets           P           R      mAP@.5  mAP@.5:.95: 100%|█| 93/93 [00:04<00:00, 19.1
               
                 all         744         437       0.914       0.878       0.931       0.569
                 
Speed: 3.8/0.6/4.4 ms inference/NMS/total per 416x416 image at batch-size 8


**Detect:**

python detect.py --weights ./runs/exp6_yolov4-csp-results/weights/best_yolov4-csp-results.pt --img 2448 --conf 0.4 --source ../inf_test/ --device 2
