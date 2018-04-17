---
layout: post
title: MediaPlayer的使用
date: 2016-02-19
categories: blog
tags: [技术]
description: MediaPlayer的使用
header-img: "img/green.jpg"
---

## 初衷

好家长新版本中增加了课本点读的功能，以前没有接触过音频播放的技术，所以在使用mediaplayer的过程中还是碰到了很多的坑，特意总结一下。

## 流程

关于mediaplayer google官方提供了一张流程图

![](http://7xr4xe.com1.z0.glb.clouddn.com/mediaplayer-prcess.jpg)

	/**
	 * 初始化
	 * @Description:TODO
	 * @exception:
	 * @time:2016-2-22 下午4:48:05
	 */
	private void init() {
		mediaPlayer = new MediaPlayer();
		mediaPlayer.setAudioStreamType(AudioManager.STREAM_MUSIC);
		mediaPlayer.setOnBufferingUpdateListener(this);
		mediaPlayer.setOnPreparedListener(this);
		mediaPlayer.setOnCompletionListener(this);
	}	
	
	/**
	 * 播放mp3
	 * 
	 * @Description:TODO
	 * @param path
	 * @exception:
	 * @time:2016-1-20 下午3:48:34
	 */
	private void playMp3(String path, int start) {
		try {
			if (!isLoadMp3) { // 第一次加载
				mediaPlayer.setDataSource(mp3PathRoot + path);
				mediaPlayer.prepareAsync();
				isLoadMp3 = true;
			} else { // 加载过mp3的话就直接播放
				mediaPlayer.start();
			}
		} catch (IllegalArgumentException e) {
			e.printStackTrace();
		} catch (SecurityException e) {
			e.printStackTrace();
		} catch (IllegalStateException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	/**
	 * mp3播放准备完成的回调
	 * 
	 * @Description:TODO
	 * @return
	 * @exception:
	 * @time:2016-1-20 下午4:00:18
	 */
	public OnPreparedListener getOnPreparedListener() {
		return new OnPreparedListener() {
	
			@Override
			public void onPrepared(MediaPlayer mp) {
				// TODO
			}
		};
	}
	
	/**
	 * 快进完成的回调
	 * 
	 * @Description:TODO
	 * @return
	 * @exception:
	 * @time:2016-1-20 下午3:59:54
	 */
	public OnSeekCompleteListener getOnSeekCompleteListener() {
		return new OnSeekCompleteListener() {
	
			@Override
			public void onSeekComplete(MediaPlayer mp) {
	
			}
		};
	}
	
	/**
	 * 播放结束的回调
	 * 
	 * @Description:TODO
	 * @return
	 * @exception:
	 * @time:2016-1-20 下午3:59:15
	 */
	public OnCompletionListener getOnCompletionListener() {
		return new OnCompletionListener() {
	
			@Override
			public void onCompletion(MediaPlayer mp) {
	
			}
		};
	}

首先要加载音频资源，setDataSource(path)，path可以是file路径（绝对路径）或者url，然后准备加载prepareAsync()（有两个准备方法，建议使用异步的），然后在准备完成回调方法onPrepared中写自己的业务逻辑，因为prepare需要花时间，是一个异步操作，所以要在回调中执行start方法开始播放音频。

补充：

meidiaplayer播放视频时，发现所支持的视频格式和视频参数特别有限，先看一张官网截图

![](http://7xr4xe.com1.z0.glb.clouddn.com/mediaplayer_format.png)

经过测试发现，帧率24和25也可用，比特率必须要小于1M，否在在6.0以上的机子上会出现缓冲到80%左右停止的现象，在播放到缓冲尾部的时候出现error(1,-1004)的错误，所以尽量保证比特率在正确范围内。










