### 多媒体

> [音频](#音频)、

#### 音频

##### 使用MediaPlayer播放音频

MediaPlayer是一个支持音频及视频文件播放。

资源文件可以放在`res/raw/`目录下。`raw`下不可以有目录结构，`raw`中的资源文件会获得资源id，可以通过R直接访问。

```java
MediaPlayer mPlayer = MediaPlayer.create(Context,ResouceID);//创建Mediaplayer实例
mPlayer.start();//播放
mPlayer.release();//释放资源
mPlayer = null;
```

`setOnCompletionListener()`可以设置监听，在播放完毕后做对应处理。