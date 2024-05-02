# Face processing with JavaScript

In the project, we have written a face recognition program with JavaScript

## Skills

Javascript

## Usage

These files must be located in localhost and cannot be uploaded by themselves!

You can test the program through the following address.

https://aiolearnfamily.com/student/opencv/index.html

```javascript
function openCvReady() {
    let cv = window.cv;
cv['onRuntimeInitialized'] = ()=>{
    let video = document.getElementById("cam_input");  
    navigator.mediaDevices.getUserMedia({ video: true, audio: false })
    .then(function(stream) {
        video.srcObject = stream;
        video.play();
    })
    .catch(function(err) {
        console.log("An error occurred! " + err);
    });
    let src = new cv.Mat(video.height, video.width, cv.CV_8UC4);
    let dst = new cv.Mat(video.height, video.width, cv.CV_8UC1);
    let gray = new cv.Mat();
    let cap = new cv.VideoCapture(cam_input);
    let faces = new cv.RectVector();
    let classifier = new cv.CascadeClassifier();
    let utils = new Utils('errorMessage');
    let faceCascadeFile = 'haarcascade_frontalface_default.xml';  
    utils.createFileFromUrl(faceCascadeFile, faceCascadeFile, () => {
    classifier.load(faceCascadeFile);  
});
    const FPS = 30;
    function processVideo() {
        let begin = Date.now();
        cap.read(src);
        src.copyTo(dst);
        cv.cvtColor(dst, gray, cv.COLOR_RGBA2GRAY, 0);
        try{
            classifier.detectMultiScale(gray, faces, 1.1, 3, 0);
            console.log(faces.size());
        }catch(err){
            // console.log(err);
        }
        for (let i = 0; i < faces.size(); ++i) {
            let face = faces.get(i);
            let point1 = new cv.Point(face.x, face.y);
            let point2 = new cv.Point(face.x + face.width, face.y + face.height);
            cv.rectangle(dst, point1, point2, [0, 255, 0, 255],3);
        }
        cv.imshow("canvas_output", dst);
        // schedule next one.
        let delay = 1000/FPS - (Date.now() - begin);
        setTimeout(processVideo, delay);
}
// schedule first one.
setTimeout(processVideo, 0);
};
}
```


This code provides a simple implementation of real-time face detection using OpenCV in a web environment. Let's break down the various components of the code:

### 1. Connecting to the Camera:
The code uses navigator.mediaDevices.getUserMedia() to connect to the device's camera and obtain the video stream. It then assigns this stream to a video element (video) on the web page and starts playing it.

### 2. Creating Image Matrices:
To process the image and detect faces, the code creates matrices using cv.Mat. src is the matrix that holds the video stream from the camera, dst is the destination matrix for processing, and gray is the matrix for storing grayscale images (required for face detection).

### 3. Cascade Classifier:
A cv.CascadeClassifier object is created, responsible for face detection. Before starting the detection, the XML file for the face detection cascade is retrieved and loaded. In this case, it's haarcascade_frontalface_default.xml.

### 4. Processing and Detecting Faces:
The code defines a function called processVideo() that handles video processing. This function continuously reads the video from the camera (cap.read(src)), converts it to grayscale, and then uses classifier.detectMultiScale() to detect faces.

### 5. Drawing Rectangles and Displaying Output:
After detecting faces, the code uses cv.rectangle() to draw rectangles around the detected faces. Then it uses cv.imshow() to display the processed image on a canvas element on the web page.

### 6. Setting Frame Rate (FPS):
The code is designed to run at a specific frame rate (in this case, 30 frames per second). This frame rate is achieved by calculating the time spent in each loop and using setTimeout to schedule the next loop accordingly.

### In Summary:
This structure allows for continuous, real-time processing of the video stream from the device's camera, detecting faces as they appear. This implementation is suitable for web applications that require face detection, such as security applications, surveillance, or fun filters.

## Result

This project was written by Majid Tajanjari and the Aiolearn team, and we need your support!❤️


# تشخیص چهره با جاوااسکریپت

در پروژه یک برنامه تشخیص چهره با جاوا اسکریپت نوشته ایم

## مهارت ها

Javascript

## نحوه استفاده

این فایل ها باید در لوکال هاست قرار داشته باشند و به تنهایی قابل آپلود نیستند!

از طریق آدرس زیر می توانید برنامه را تست کنید.

https://aiolearnfamily.com/student/opencv/index.html

```javascript
function openCvReady() {
    let cv = window.cv;
cv['onRuntimeInitialized'] = ()=>{
    let video = document.getElementById("cam_input");  
    navigator.mediaDevices.getUserMedia({ video: true, audio: false })
    .then(function(stream) {
        video.srcObject = stream;
        video.play();
    })
    .catch(function(err) {
        console.log("An error occurred! " + err);
    });
    let src = new cv.Mat(video.height, video.width, cv.CV_8UC4);
    let dst = new cv.Mat(video.height, video.width, cv.CV_8UC1);
    let gray = new cv.Mat();
    let cap = new cv.VideoCapture(cam_input);
    let faces = new cv.RectVector();
    let classifier = new cv.CascadeClassifier();
    let utils = new Utils('errorMessage');
    let faceCascadeFile = 'haarcascade_frontalface_default.xml';  
    utils.createFileFromUrl(faceCascadeFile, faceCascadeFile, () => {
    classifier.load(faceCascadeFile);  
});
    const FPS = 30;
    function processVideo() {
        let begin = Date.now();
        cap.read(src);
        src.copyTo(dst);
        cv.cvtColor(dst, gray, cv.COLOR_RGBA2GRAY, 0);
        try{
            classifier.detectMultiScale(gray, faces, 1.1, 3, 0);
            console.log(faces.size());
        }catch(err){
            // console.log(err);
        }
        for (let i = 0; i < faces.size(); ++i) {
            let face = faces.get(i);
            let point1 = new cv.Point(face.x, face.y);
            let point2 = new cv.Point(face.x + face.width, face.y + face.height);
            cv.rectangle(dst, point1, point2, [0, 255, 0, 255],3);
        }
        cv.imshow("canvas_output", dst);
        // schedule next one.
        let delay = 1000/FPS - (Date.now() - begin);
        setTimeout(processVideo, delay);
}
// schedule first one.
setTimeout(processVideo, 0);
};
}
```


این کد به عنوان یک پیاده‌سازی ساده از تشخیص چهره در زمان واقعی با استفاده از OpenCV در محیط وب عمل می‌کند. بیایید بخش‌های مختلف این کد را دقیق‌تر بررسی کنیم:

### 1. اتصال به دوربین:
کد با استفاده از navigator.mediaDevices.getUserMedia() به دوربین دستگاه متصل می‌شود و جریان ویدئویی را می‌گیرد. سپس این جریان را به عنصر ویدئو (video) در صفحه وب اختصاص می‌دهد و آن را پخش می‌کند.

### 2. ایجاد ماتریس‌های تصویر:
برای پردازش تصویر و تشخیص چهره، کد ماتریس‌هایی را با استفاده از cv.Mat ایجاد می‌کند. src ماتریسی است که ویدئو از دوربین در آن خوانده می‌شود، dst ماتریس هدف برای انجام پردازش‌ها، و gray ماتریسی برای ذخیره‌سازی تصویر به صورت سیاه‌وسفید (ضروری برای تشخیص چهره).

### 3. طبقه‌بندی آبشاری (Cascade Classifier):
یک شیء از نوع cv.CascadeClassifier ایجاد می‌شود که مسئول تشخیص چهره‌هاست. قبل از شروع تشخیص، فایل XML مربوط به آبشاری تشخیص چهره از یک URL دریافت و بارگذاری می‌شود. در این مورد، از haarcascade_frontalface_default.xml استفاده شده است.

### 4. پردازش و تشخیص چهره‌ها:
کد یک تابع به نام processVideo() را ایجاد می‌کند که مسئول پردازش ویدئو است. این تابع در یک حلقه به طور مداوم تصویر را از دوربین می‌خواند (cap.read(src))، آن را به سیاه‌وسفید تبدیل می‌کند، و سپس از classifier.detectMultiScale() برای تشخیص چهره‌ها استفاده می‌کند.

### 5. ترسیم مستطیل و نمایش خروجی:
پس از تشخیص چهره‌ها، کد از cv.rectangle() برای رسم مستطیل‌هایی دور چهره‌ها استفاده می‌کند. سپس، از cv.imshow() برای نمایش تصویر پردازش‌شده روی یک عنصر canvas در صفحه وب استفاده می‌شود.

### 6. تنظیم نرخ فریم (FPS):
کد طوری طراحی شده که با یک نرخ فریم خاص (در اینجا 30 فریم در ثانیه) اجرا شود. این نرخ با محاسبه زمان صرف‌شده در هر حلقه و استفاده از setTimeout برای برنامه‌ریزی حلقه بعدی تنظیم می‌شود.

### در نهایت:
این ساختار به ما امکان می‌دهد تا به طور پیوسته و در زمان واقعی، جریان ویدئویی از دوربین دستگاه را پردازش کرده و چهره‌ها را تشخیص دهیم. این پیاده‌سازی برای برنامه‌های وب که نیاز به تشخیص چهره دارند، مانند برنامه‌های امنیتی، نظارتی یا فیلترهای سرگرمی، مناسب است.


## نتیجه

این پروژه توسط مجید تجن جاری و تیم Aiolearn نوشته شده است و ما به حمایت شما نیازمندیم!❤️