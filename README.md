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
    * For example: `http://192.168.0.30:8080/live/test.m3u8`
* Click "Play"
* Now VLC should start playing whatever you are transmitting from OBS Studio