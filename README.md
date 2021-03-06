Stream2Chromecast
=================

A Chromecast media streamer for Linux.

Stream2Chromecast casts media files to a Chromecast device from Linux.

It will also transcode any unsupported files in real time and play them on the Chromecast.

It is written in Python 2.7 and uses the PyChromecast library to control the device: https://github.com/balloob/pychromecast (Thanks Paulus!)




Installation
------------
We need the python packages requests and protobuf installed.

So, for example, on Ubuntu run:-

    sudo apt-get install python-protobuf python-requests
   
   
   
To play media file types that are unsupported by Chromecast, we need either ffmpeg or avconv installed to do the transcoding.

On Ubuntu we can either install avconv:-

    sudo apt-get install libav-tools
   
...or install ffmpeg

    sudo add-apt-repository ppa:mc3man/trusty-media
    apt-get install ffmpeg
   



Functionality
-------------
To stream supported media files to a Chromecast.

        stream2chromecast.py my_media.mp4


To transcode and stream unsupported media files to a Chromecast.
    (This requires either ffmpeg or avconv to be installed. See Dependencies.)

        stream2chromecast.py -transcode my_mpeg_file.mpg


Control playback

 - pause playback (currently only works when not transcoding)
   
        stream2chromecast.py -pause
       
 - continue (unpause) playback (currently only works when not transcoding)
   
        stream2chromecast.py -continue
       
 - stop playback
   
        stream2chromecast.py -stop  


Configuration

 - set the preferred transcoder (if both ffmpeg and avconv are installed)
    
        stream2chromecast.py -set_transcoder <transcoder command>
        
 The transcoder command value mst be one of ffmpeg or avconv
    

 - set the transcoding quality preset and bitrate

        stream2chromecast.py -set_transcode_quality <preset> <bitrate>       
    
 The preset value must be one of:-
   ultrafast, superfast, veryfast, faster, fast, medium, slow, slower, veryslow, placebo.
   
 The bitrate must be an integer (optionally ending with k) e.g. 2000k
      
            
 - reset the transcoding quality and bitrate to defaults:-
        stream2chromecast.py -reset_transcode_quality              
          
   
Notes
-----
The real-time transcoding is done by ffmpeg (or avconv) using the ultrafast preset by default. Consequently, by default, the video quality is not as good as it would be if slower presets were used. However, it does allow even modestly powered machines to serve video without buffering. The transcoding preset and bitrate can be adjusted using the "set_transcode_quality" function to improve the quality on more highly powered processors.

avconv is a fork of ffmpeg. It appears that the Ubuntu packagers included avconv in the repositories rather than ffmpeg. However there is a PPA repository available which contains the latest builds of ffmpeg. See the installation notes.


To Do
-----
    Add stream2chromecast to the "open with" context menu. 
    Handle multiple Chromecast devices.
    Automatic identification of media types that need transcoding.
    Set up a proper install procedure.


License
-------
stream2chromecast.py is GPLv3 licensed.

It depends on the PyChromecast library which is MIT licensed - see https://github.com/balloob/pychromecast


Thanks
------
This project uses the PyChromecast library by Paulus Schoutsen to do the difficult bits.
