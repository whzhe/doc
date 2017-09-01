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
            audoFileSuffix: ".mp3", // 实际使用中文件名为 [audioFile]_[voiceType].[audoFileSuffix]
            imageFile: ["img/20170901/sports/sport_0000001_0.jpg", "img/20170901/sports/sport_0000001_1.jpg"] //新闻配图文件地址
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
### 1.2 用户接口
|METHOD|PATH|MSG TYPE|
|:----:|:-----:|:----|
|POST|/news|MSG_TYPE_NEWS_GET_NEWS|
#### 1.2.1 用户获取新闻
上报报文
```
    {
        type: "MSG_TYPE_NEWS_GET_NEWS",
        category："sports",
        startIdx: 100,
        num: 30
    }
```    

回复报文
```
    {
        type: "MSG_TYPE_NEWS_GET_NEWS",
        ret: 0, // 非0 时，携带errStr字段，不携带data
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
            audoFileSuffix: ".mp3", // 实际使用中文件名为 [audioFile]_[voiceType].[audoFileSuffix]
            imageFile: ["img/20170901/sports/sport_0000001_0.jpg", "img/20170901/sports/sport_0000001_1.jpg"] //新闻配图文件地址
          },
          { //第二条新闻，字段同上
          }
        ]
    }
```
### 1.3 编辑接口
|METHOD|PATH|MSG TYPE|
|:----:|:-----:|:----|
|POST|/edit|MSG_TYPE_EDIT_GET_NEWS_1<br>MSG_TYPE_EDIT_GET_NEWS_2|
#### 1.3.1 获取待编辑处理的新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_GET_NEWS_1",
        category："sports",
        startIdx: 100,
        num: 30
    }
```    

回复报文
```
    {
        type: "MSG_TYPE_EDIT_GET_NEWS_1",
        ret: 0, // 非0 时，携带errStr字段，不携带data
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
            audoFileSuffix: ".mp3", // 实际使用中文件名为 [audioFile]_[voiceType].[audoFileSuffix]
            imageFile: ["img/20170901/sports/sport_0000001_0.jpg", "img/20170901/sports/sport_0000001_1.jpg"] //新闻配图文件地址
          },
          { //第二条新闻，字段同上
          }
        ]
    }
```
#### 1.3.2 获取待总编处理的新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_GET_NEWS_2",
        category："sports",
        startIdx: 100,
        num: 30
    }
```    

回复报文
```
    {
        type: "MSG_TYPE_EDIT_GET_NEWS_2",
        ret: 0, // 非0 时，携带errStr字段，不携带data
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
            audoFileSuffix: ".mp3", // 实际使用中文件名为 [audioFile]_[voiceType].[audoFileSuffix]
            imageFile: ["img/20170901/sports/sport_0000001_0.jpg", "img/20170901/sports/sport_0000001_1.jpg"] //新闻配图文件地址
          },
          { //第二条新闻，字段同上
          }
        ]
    }
```
