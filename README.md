# Cell_Detection
Cell Detection

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


**Detect:**

python detect.py --weights ./runs/exp6_yolov4-csp-results/weights/best_yolov4-csp-results.pt --img 2448 --conf 0.4 --source ../inf_test/ --device 2
