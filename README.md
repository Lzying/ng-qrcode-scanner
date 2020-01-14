##### 总体思路
* 总体思路是通过navigator.mediaDevices.getUserMedia 获取摄像头流，通过video播放视频流，通过截图video视频得到图片，再通过对图片的识别得出二维码识别二维码js库，ios中只兼容safari，其他手机兼容chrome，只在https协议中支持
* angular可以采用ViewChild来获取元素  <video id="video"  #video autoplay x5-playsinline="" playsinline="" webkit-playsinline=""></video>
*  @ViewChild('video') video: HTMLVideoElement;
* 注意有些浏览器不兼容需要解决，
 
        <video id="video" autoplay x5-playsinline="" playsinline="" webkit-playsinline=""></video>
 
        let video=document.getElementById('video');
        let constraintss = { video: { facingMode: { exact: 'environment' } }, audio: false };
        navigator.mediaDevices.getUserMedia(constraintss).then((stream) => {
            // video.src = URL.createObjectURL(stream);   // 将获取到的视频流对象转换为地址，不兼容Safari
            let track = stream.getTracks()[0]; // 此方法兼容Safari
            video.srcObject = stream;   // 将获取到的视频流对象转换为地址

            // this.video.onplaying = () => {
            //    // 已經播放
            // };
            this.video.onloadedmetadata = (e) => {
                // video.play();   // 播放，video标签上有自动播放设置不需要触发播放
            };

        }).catch((err) => {
            /* 处理error */
        });
