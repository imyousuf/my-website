---
title: 'Video Recording using Flash'
date: 2007-07-05T02:53:00.000-07:00
draft: false
tags : [video streaming, flash, Red5]
---

Recording Video using Flash is a trend on the high. YouTube Quick Capture is one that has caught our eyes on this. So I was trying to get something done in the same way. I am basically Java developer and have experience of developing Video Recorder using Java Media Framework. Though I am a Java fanatic I feel that at present Flash is the way to Video on Internet. Its adaptation in video technology is very wide spread and well acclaimed. This blog is about is about video recording.  
  
The first thing that is required for Flash video recording is a media server for streaming; because Flash unlike signed applet can store on local disk, it in fact streams the captured video to media server. There is Adobe Media Server or Flash Communication Server that we can use after procuring or there is [Red5](http://osflash.org/red5); thanks to the open source community. Now with Red5 comes a sample simple video recorder, using which you can simply stream video to the server. If we look at a customized [Simple Recorder](http://imyousuf.100webspace.net/blog-demo/video-recorder/SimpleRecorder.html) (it is only the recorder and there is no attached streaming server :) if anyone can help please let me know) we will find that for sole recording purpose there is a video container that shows the video. Initially it shows the currently being captured video and once the recording is stopped it shows the streamed video of the just recorded stream. This events are triggered by the buttons on SWF video. It uses the oflaDemo Red5 Application provided as demo with the server. All streamed videos are stored in {RED5\_HOME}/webapps/oflaDemo/streams/.  
  
Now lets look at the code used for this purpose. The first task is to open an stream when we intend to record something.  

> var nc:NetConnection = new NetConnection();  
>   
> // connect to the local media server  
> // rtmp://{host}:{port}/{Red5\_application\_context}  
> // default port is 1935  
> nc.connect("rtmp://localhost/oflaDemo");  
>   
> // create the netStream object and pass the netConnection object in the  
> // constructor  
> var ns:NetStream = new NetStream(nc);

The second thing that we can do is detect and select the capture devices.  

> // get references to the camera and mic  
> var cam:Camera = Camera.get();  
> var mic:Microphone = Microphone.get();

Now above we selected the default devices but we could Camera.names to get the names of the capture devices and select the one that we want; this is something that YouTube does :). Next we need to configure the video capture stream.  

> // setting dimensions and framerate  
> cam.setMode(320, 240, 30);  
> // set to minimum of 70% quality  
> cam.setQuality(0,70);  
> //Setting sampling rate to 8kHz  
> mic.setRate(8);

Next we need to add the device streams to the capture stream.  

> // This FLV is recorded to webapps/oflaDemo/streams/ directory  
> // attach cam and mic to the NetStream Object  
> ns.attachVideo(cam);  
> ns.attachAudio(mic);

After that we need to add the camera to the container and publish the video.  

> // attach the cam to the videoContainer on stage so we can see ourselves  
> videoContainer.attachVideo(cam);  
> // Publish the video and mention record  
> // lastVideoName is the name of the video and it will be saved as \]  
> // lastVideoName.flv  
> ns.publish(lastVideoName, "record");  

Now once the recording is just clear the video container and the captured stream to the container and specify the stream to play the just recorded video  

> // attach the netStream object to the video object  
> videoContainer.attachVideo(ns);  
> // play back the recorded stream  
> ns.play(lastVideoName);

Hopefully with these steps a video recording and stream playback should be possible.