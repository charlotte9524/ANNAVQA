# Deep Neural Networks for Full-Reference and No-reference Audio-Visual Quality Assessment
[![License](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](License)

## Description
ANNAVQA code for the following papers:

- Y. Cao, X. Min, W. Sun and G. Zhai, "Deep Neural Networks For Full-Reference And No-Reference Audio-Visual Quality Assessment," 
  2021 IEEE International Conference on Image Processing (ICIP), 2021, pp. 1429-1433, doi: 10.1109/ICIP42928.2021.9506408.
  
## Test Demo
The test video should be provided in raw `YUV 4:2:0` format. The test audio should be provided in `wav` format.
### Saliency Detection
You should first run sal_position.m in Matlab to get `test_position.mat`.
```
sal_position ./dis_test.yuv 1080 1920
```
You need to specify the `distorted video`, `video height` and `video width`.

### Quality Prediction
#### Full-Reference Model Quality Prediction
The FR model weights provided in `./models/FR_model` are the saved weights when running on LIVE-SJTU. During training, we randomly split each database
into three sets: a training set (80% of the A/V sequences), a validation set (20% of the A/V sequences) and a testing set (20% of the A/V sequences) without overlapping each
other. We train models only on the training set, find the top models `./models/NR_model` on the validation set (PowerDig class and RedKayak class) and test the top model on the testing set (FootMusic class and Sparks class).
```
python FR_LS_test.py --ref_video_path='./ref_test.yuv' --dis_video_path='./dis_test.yuv' --dis_audio_path='./dis_test.wav' --ref_audio_path='./ref_test.wav' --frame_rate=24
```
You need to specify the `referenced video path`, `referenced audio path`, `distorted video path`, `distorted audio path` and `frame rate`.
Because the video resolution of LIVE-SJTU is `1080p`, our default settings of height and width are 1080 and 1920.
You can change by `--video_width=` and `--video_height=`.

#### No-Reference Model Quality Prediction
The NR model weights provided in `./models/NR_model` are the saved weights when running on LIVE-SJTU.  During training, we randomly split each database
into three sets: a training set (80% of the A/V sequences), a validation set (20% of the A/V sequences) and a testing set (20% of the A/V sequences) without overlapping each
other. We train models only on the training set, find the top models `./models/NR_model` on the validation set (PowerDig class and RedKayak class) and test the top model on the testing set (FootMusic class and Sparks class).
 
```
python NR_LS_test.py --dis_video_path='./dis_test.yuv' --dis_audio_path='./dis_test.wav' --frame_rate=24
```
You need to specify the `distorted video path`, `distorted audio path` and `frame rate`.
Because the video resolution of LIVE-SJTU is `1080p`, our default settings of height and width are 1080 and 1920,
which you can change by `--video_width=` and `--video_height=`.

### Requirement
- PyTorch 1.5.0
- Matlab R2020b

Note: we will upload the training code of ANNAVQA later. When you use `./models/FR_model`  and 
`./models/NR_model` we trained, the model extracts features of the first 192 frames.
### Contact
caoyuqin800@163.com

