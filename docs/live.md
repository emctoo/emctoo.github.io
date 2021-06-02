客户端 [使用flv.js做直播](https://github.com/gwuhaolin/blog/issues/3#)

服务端简单的方案 [livego](https://github.com/gwuhaolin/livego)

- 启动服务端

```shell
./livego
```

- get chanel key from livego http service, for pushing stream: `http://localhost:8090/control/get?room=movie`

- ffmpeg push stream

```shell
# download demo video
wget https://s3plus.meituan.net/v1/mss_7e425c4d9dcb4bb4918bbfa2779e6de1/mpack/default/demo.flv

# push streaming, here `rfBd...9PYk` is the channel key， appname: live
ffmpeg -re -i demo.flv -c copy -f flv rtmp://localhost:1935/live/rfBd56ti2SMtYvSgD5xAV0YU99zampta7Z7S575KLkIZ9PYk
```

following three playback available, appName = live

​    - `rtmp://localhost:1935/{appname}/movie`

​    - `http://127.0.0.1:7001/{appname}/movie.flv`

​    - `http://127.0.0.1:7002/{appname}/movie.m3u8`

- create `flv.js` demo, serving with `python -m http.server 2000`, visit at `http://localhost:2000` in browser

```html
<!DOCTYPE html>
<html>

<head>
    <meta content="text/html; charset=utf-8" http-equiv="Content-Type">
    <title>live demo</title>
    <style>
        .mainContainer {
            display: block;
            width: 1024px;
            margin-left: auto;
            margin-right: auto;
        }
        .urlInput {
            display: block;
            width: 100%;
            margin-left: auto;
            margin-right: auto;
            margin-top: 8px;
            margin-bottom: 8px;
        }
        .centeredVideo {
            display: block;
            width: 100%;
            height: 576px;
            margin-left: auto;
            margin-right: auto;
            margin-bottom: auto;
        }
        .controls {
            display: block;
            width: 100%;
            text-align: left;
            margin-left: auto;
            margin-right: auto;
        }
    </style>
</head>
<body>
    <div class="controls">
        <button onclick="flv_start()">开始</button>
        <button onclick="flv_pause()">暂停</button>
        <button onclick="flv_destroy()">停止</button>
        <input style="width:100px" type="text" name="seekpoint" />
        <button onclick="flv_seekto()">跳转</button>
    </div>

	<script src="https://cdn.bootcdn.net/ajax/libs/flv.js/1.5.0/flv.min.js"></script>
    <script>
        const url = 'http://127.0.0.1:7001/live/movie.flv';
        let player = document.getElementById('videoElement');
        if (flvjs.isSupported()) {
            const flvPlayer = flvjs.createPlayer({type: 'flv', isLive: true, url});
            flvPlayer.attachMediaElement(videoElement);
            flvPlayer.load();
            flv_start();
        }
        function flv_start() { player.play(); }
        function flv_pause() { player.pause(); }
        function flv_destroy() {
            player.pause();
            player.unload();
            player.detachMediaElement();
            player.destroy();
            player = null;
        }
        function flv_seekto() { player.currentTime = parseFloat(document.getElementsByName('seekpoint')[0].value); }
    </script>
</body>
</html>
```

