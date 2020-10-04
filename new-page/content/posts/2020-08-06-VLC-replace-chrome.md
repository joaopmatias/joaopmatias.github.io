---
layout: post
date: 2020-08-06
title:  "Lightweight alternatives to stream video on the browser"
---


Like many others, I often enjoy having youtube or twitch videos playing on the brackground while doing other tasks on the computer, and like most people I would have them conveniently playing on a separate tab of Chrome. Despite the convenience, there are some downside to using Chrome for that purpose like the excessive memory used by the browser, the whole area of the webpage occupied by things other than the video and the lack of an option to keep the video, say, on the corner of the computer screen. These drawbacks drove me to search some alternatives and I'd like to share my set up. 

## Disclaimer

The options shown were tested in MacOS and it is possible that they may not work in a different OS.


Let us start by the mediaplayer.

## VLC window

This is an extremely popular mediaplayer and it is no surprise that it is capable of playing video directly from Youtube or Twitch (the latter has a caveat, more on that later). For a better experience, I prefer to have a window just for the video and without any control buttons, which can be achieved by unchecking *Video decorations* in *Preferences > Video*. Beware that version 3.0.9 showed problems resizing the window when this option was unchecked. 

![VLC Preferences](https://joaopmatias.github.io/content/images/blog/video_decorations.png)

I also like adding the option *Video > Float on Top* and the controls *View > Show Previous & Next Buttons* and *View > Show Shuffle & Repeat Buttons*.


## Playing Youtube videos

Since VLC is looking better now, you can try playing a Youtube video. Simply, copy the video link, paste it in *File > Open Network...* and enjoy!


## Update VLC Lua playlist script

Some older versions of VLC may have some issues playing some videos. One possible solution is updating a specific file. You can try deleting the file `/Applications/VLC.app/Contents/MacOS/share/lua/playlist/youtube.luac` and replacing it with a [newer version](https://github.com/videolan/vlc/blob/master/share/lua/playlist/youtube.lua).


## Video playlists

One easy way to make a playlist of Youtube videos is by creating a plaintext file with the `.m3u` extension with the following format.

```
#EXTM3U
#EXTINF:1,1 - This is a fun video
https://www.youtube.com/watch?v=dQw4w9WgXcQ
#EXTINF:1,1 - This is a fun video 2
https://www.youtube.com/watch?v=kfVsfOSbJY0
```


## streamlink

The software [streamlink](https://streamlink.github.io/install.html) allows streaming Twitch directly in VLC by running a command of the form
```
streamlink https://www.twitch.tv/gamesdonequick 720p
```


I hope you enjoyed! See you in the next post.

