# aws-kinesis
aws-kinesis video stream for raspberry pi 3 b+

1) https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/producersdk-cpp-rpi.html#producersdk-cpp-rpi-software  
2) https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/examples-gstreamer-plugin.html  

```
....
Now you can set the environment variables before running the sample applications
by running source set_kvs_sdk_env.sh
Also, you may want to add the following environment variables to set it permanently
in /root/.bashrc or /root/.bash_profile or /root/.zshrc
**********************************************************
Success in building kinesis-video-gstreamer-plugin !!!
```

```
$ export AWS_ACCESS_KEY_ID=""
$ export AWS_SECRET_ACCESS_KEY=""
$ export AWS_DEFAULT_REGION=""
$ export STREAM_NAME=""
```

```
./set_kvs_sdk_env.sh
```

```
gst-launch-1.0 v4l2src do-timestamp=TRUE device=/dev/video0 ! videoconvert ! video/x-raw,format=I420,width=640,height=480,framerate=30/1 ! omxh264enc control-rate=1 target-bitrate=5120000 inline-header=FALSE ! h264parse ! video/x-h264,stream-format=avc,alignment=au,width=640,height=480,framerate=30/1,profile=baseline ! kvssink stream-name="${STREAM_NAME}" access-key="${AWS_ACCESS_KEY_ID}" secret-key="${AWS_SECRET_ACCESS_KEY}" aws-region="${AWS_DEFAULT_REGION}"
```

