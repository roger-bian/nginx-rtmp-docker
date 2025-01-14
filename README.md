## How to use

### build docker image

```
docker build -t nginx-rtmp-hls:1.0.0 .
```

### run docker image
```
docker run -d -p 1935:1935 -p 8080:8080 --name nginx-rtmp-hls nginx-rtmp-hls:1.0.0
```

### access interactive shell

```
docker exec -it nginx-rtmp-hls /bin/bash
```

### stream to nginx using ffmpeg

```
ffmpeg -i rtsp://Factory-Admin:Camadmin1@{$CAM_IP}/Src/MediaInput/stream_1 -c:v copy -c:a aac -ar 44100 -ac 1 -f flv rtmp://localhost:{$INPUT_PORT}/live/{$SET_CAM_KEY}
```

## port + hls_path mapping

| Port (Listen)  | hls_path    |
| -------------- | ----------- |
| 1935           | /www/hls1/  |
| 1936           | /www/hls2/  |
| 1937           | /www/hls3/  |
| 1938           | /www/hls4/  |
| 1939           | /www/hls5/  |
| 1940           | /www/hls6/  |
| 1941           | /www/hls7/  |
| 1942           | /www/hls8/  |


## How to test with OBS Studio and VLC

* Run a container with the command above


* Open [OBS Studio](https://obsproject.com/)
* Click the "Settings" button
* Go to the "Stream" section
* In "Stream Type" select "Custom Streaming Server"
* In the "URL" enter the `rtmp://<ip_of_host>/live` replacing `<ip_of_host>` with the IP of the host in which the container is running. 
    * For example: `rtmp://192.168.0.30/live`
* In the "Stream key" use a "key" that will be used later in the client URL to display that specific stream. 
    * For example: `test`
* Click the "OK" button
* In the section "Sources" click the "Add" button (`+`) and select a source (for example "Screen Capture") and configure it as you need
* Click the "Start Streaming" button
* Open a [VLC](http://www.videolan.org/vlc/index.html) player (it also works in Raspberry Pi using `omxplayer`)
* Click in the "Media" menu
* Click in "Open Network Stream"
* Enter the URL from above as `http://<ip_of_host>:8080/hls/<key>.m3u8` replacing `<ip_of_host>` with the IP of the host in which the container is running and `<key>` with the key you created in OBS Studio. 
    * For example: `http://192.168.0.30:8080/hls/test.m3u8`
* Click "Play"
* Now VLC should start playing whatever you are transmitting from OBS Studio