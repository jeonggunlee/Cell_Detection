# Cell_Detection
Cell Detection

**Train:**

python train.py --img 416 --batch 64 --epochs 100 --data '../data.yaml' --cfg ./models/yolov4-csp.yaml --weights '' --name yolov4-csp-results --cache


**Test:**

python test.py --img-size 416 --conf-thres 0.001 --batch-size 8 --data ../data.yaml --weights ./runs/exp6_yolov4-csp-results/weights/best_yolov4-csp-results.pt


**Detect:**

python detect.py --weights ./runs/exp6_yolov4-csp-results/weights/best_yolov4-csp-results.pt --img 2448 --conf 0.4 --source ../inf_test/ --device 2
