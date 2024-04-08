

## Introduction
 This repo contains object_detection.py, which can perform the following task -
 - Object detection from a live video frame, in any video file, or in an image
 - Counting the number of objects in a frame
 - Measuring the distance of an object using depth information
 - Inference on Multiple Camera feed at a time
 
For object detection, YOLO-V3 has been used, which is able to detect 80 different objects. Some of those are-
- person
- car
- bus
- stop sign
- bench
- dog
- bear
- backpack, and so on.

### User Instruction

## Update

**There is a new update with [yolov4 new release](https://github.com/Tianxiaomo/pytorch-YOLOv4). All you have to do a simple step which is after downloading the project, run the following command and follow the rest of the process as it is.**

  ```
    cd YOLOv4
  ```

You can also use Yolact++ as a object detector using [this](https://github.com/paul-pias/Social-Distance-Monitoring) repo.


To execute object_dection.py, you require Python version > 3.5 (depends if you are using gpu or not) and have to install the following libraries.

### Instalation
``` python
    $ pip install -r requirements.txt
         or
    $ pip install opencv-python
    $ pip install numpy
    $ pip install pandas
    $ pip install matplotlib
    $ pip install Pillow
    $ pip install imutils
```
<hr>

#### For the installation of torch using "pip" 
``` python
    $ pip3 install torch===1.2.0 torchvision===0.4.0 -f https://download.pytorch.org/whl/torch_stable.html
```
or please follow the instructions from [Pytorch](https://pytorch.org/)
#### For installing the "win32com.client" which is Text-to-Speech module for windows you have follow this
First open the cmd as an administrator, then run
``` python
   $ python -m pip install pywin32
   #After installing, open your Python shell and run
      import win32com.client
      speaker = win32com.client.Dispatch("SAPI.SpVoice")
      speaker.Speak("Good Morning")
```

You need to clone the repository using git bash (if git bash is already installed), or you can download the zip file.
``` python
    $ git clone https://github.com/paul-pias/Object-Detection-and-Distance-Measurement.git
```

After unzipping the project, there are two ways to run this. If you want to see your output in your browser, execute the "app.py" script or run "object_detection.py" to execute it locally.


If you want to run object detection and distance measurement on a video file, just write the name of the video file to variable <b>id</b> in either "app.py" or "object_detection.py" or if you want to run it on your webcam just put 0 in <b>id</b>.

However, if you want to run the inference on a feed of <b>IP Camera </b>, use the following convention while assigning it to the variable <b>"id"</b>
``` python
    "rtsp://assigned_name_of_the_camera:assigned_password@camer_ip/"
```

You can check the performance on different weights of YOLO, which are available in [YOLO](https://pjreddie.com/darknet/yolo/?style=centerme)

For multiple camera support, you need to add a few codes as follows in app.py-

``` python
   def simulate(camera):
       while True:
           frame = camera.main()
           if frame != "":
               yield (b'--frame\r\n'
                   b'Content-Type: image/jpeg\r\n\r\n' + frame + b'\r\n\r\n')

   @app.route('/video_simulate')
   def video_simulate():
       id = 0
       return Response(gen(ObjectDetection(id)), mimetype='multipart/x-mixed-replace; boundary=frame')
```

Depending on how many feeds you need, add the two methods in "app.py" with different names and add a section in index.html.

``` html
<div class="column is-narrow">
        <div class="box" style="width: 500px;">
            <p class="title is-5">Camera - 01</p>
            <hr>
            <img id="bg" width=640px height=360px src="{{ url_for('video_simulate') }}">
            <hr>

        </div>
    </div>
    <hr>
```
#### Note: 
You have to use git-lfs to download the yolov3.weight file. However you can also download it from here [YOLOv3 @ Google-Drive](https://drive.google.com/drive/folders/1nN49gRqt5HvuMptfc0wRVcuLwiNmMD6u?usp=sharing) || [YOLOv4 @ Google-Drive](https://drive.google.com/file/d/1cewMfusmPjYWbrnuJRuKhPMwRe_b9PaT/view)
<hr>


