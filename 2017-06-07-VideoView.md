---
title: 使用VideoView遇到的问题
date: 2017-06-07 14:51:05
tags:
---

- #### 基本使用


  VideoView本身是继承了SurfaceView，其内部维护了一个Mediaplayer实例，所以api和Mediaplayer的api非常相似；另外可以为VideoView加上简单的控制器，使用MediaController。

  ```
  mVideoView.setVideoPath("http://video.jiecao.fm/11/23/xin/%E5%81%87%E4%BA%BA.mp4");
  mVideoView.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
              @Override
              public void onPrepared(MediaPlayer mp) {
                  mVideoView.start();
              }
          });

  MediaController mediaController = new MediaController(this);
  mediaController.setMediaPlayer(mVideoView);
  mVideoView.setMediaController(mediaController);
  ```

- #### 遇到的问题

  进入有VideoView的activity会黑屏；不管为VideoView设置多大的宽高，最终显示效果类似ImageView的FIT_CENTER效果；由于在onStop时SurfaceView会调用surfaceDestroyed()方法，onResume是会调用surfaceCreated()重新创建，进而导致视频会从头播放；全屏显示；

- #### 解决方法

  黑屏根本原因没有找到，但是发现只有VideoView的父布局黑屏，解决方法可以先给VideoView设置背景，等mediaPlayer prepare完成再把背景设置透明；

  宽高的问题，重写onMearse方法；

  onResume之后重头播放的问题，onPause保存播放进度，onResume中调用seekTo方法；

  surfaceView在onMearse方法中进行了特殊处理，视频本身只会撑满surfaceView宽高，不管surfaceView多大视频就撑满，为了不变形会对视频宽高和自身宽高进行等比计算出最终的宽高。

- #### 更好的解决方案

  使用TextureView+mediaPlayer，具体参考[JieCaoVideoPlayer](https://github.com/lipangit/JieCaoVideoPlayer)

  ​