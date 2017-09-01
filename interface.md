## 目录
* [新闻发布系统](https://github.com/VoiceNews/doc/blob/master/interface.md#1-新闻发布系统)
   * [内部系统间接口](https://github.com/VoiceNews/doc/blob/master/interface.md#11-内部系统间接口)
      * [机器人新闻发布接口](https://github.com/VoiceNews/doc/blob/master/interface.md#111-机器人新闻发布接口)

## 1. 新闻发布系统
### 1.1 内部系统间接口
|METHOD|PATH|MSG TYPE|
|:----:|:-----:|:----|
|POST|/internel|MSG_TYPE_INTERNEL_NEW_NEWS|
#### 1.1.1 机器人新闻发布接口
上报报文
```
    {
        type: "MSG_TYPE_INTERNEL_NEW_NEWS",
        data : [
          { //第一条新闻
            category: "sports", //类别: sports,finance,politics
            title: "", // 标题
            content: "", //正文（摘要的内容）
            source: "", //来源：toutiao,sina,sohu
            oriUrl: "", //原始链接
            newsTime: "2017-09-01", //新闻写作时间；另外在数据库中创建该新闻时，需要加一个创建时间字段
            audioFile: "audio/20170901/sports/sport_0000001", //语音文件的文件名. 0000001建议为数据库的id字段
            voiceType: ["male", "female", "lingzhiling"], //后台合成几个，放几个，至少合成male与female
            audoFileSuffix: ".mp3" // 实际使用中文件名为 [audioFile]_[voiceType].[audoFileSuffix]
          },
          { //第二条新闻，字段同上
          }
        ]
    }
```    
回复报文
```
    {
        type: "MSG_TYPE_INTERNEL_NEW_NEWS",
        ret：0,        //0：成功，非0：失败
        errStr: "N/A"  //出错时，携带该字段
    }
```
