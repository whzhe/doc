## 目录
* [新闻发布系统](https://github.com/VoiceNews/doc/blob/master/interface.md#1-新闻发布系统)
   * [内部系统间接口](https://github.com/VoiceNews/doc/blob/master/interface.md#11-内部系统间接口)
      * [机器人新闻发布接口](https://github.com/VoiceNews/doc/blob/master/interface.md#111-机器人新闻发布接口)
   * [用户接口](https://github.com/VoiceNews/doc/blob/master/interface.md#12-用户接口)
      * [用户获取新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#121-用户获取新闻)
   * [编辑接口](https://github.com/VoiceNews/doc/blob/master/interface.md#13-编辑接口)
      * [获取待编辑处理的新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#131-获取待编辑处理的新闻)
      * [获取待总编处理的新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#132-获取待总编处理的新闻)
      * [编辑新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#133-编辑新闻)
      * [总编编辑新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#134-编辑新闻)
      * [发布新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#135-发布新闻)
      * [撤回发布新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#136-撤回发布新闻)
      * [删除新闻](https://github.com/VoiceNews/doc/blob/master/interface.md#137-删除新闻)

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
            states:"",//表示此条新闻的状态，0表示需要编辑处理，1表示需要总编处理，2表示用户可看
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
            id: 1, // 数据库identity字段
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
            states:"",//表示此条新闻的状态，0表示需要编辑处理，1表示需要总编处理，2表示用户可看
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
            id: 1, // 数据库identity字段
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
            states:"",//表示此条新闻的状态，0表示需要编辑处理，1表示需要总编处理，2表示用户可看
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
            id: 1, // 数据库identity字段
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
            states:"",//表示此条新闻的状态，0表示需要编辑处理，1表示需要总编处理，2表示用户可看
          },
          { //第二条新闻，字段同上
          }
        ]
    }
```
#### 1.3.3 编辑新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_EDIT_NEWS_1",
        data: {
          id: 1,
          title: "", // 标题
          content: "", //正文（摘要的内容）
          editorScore: 90, //编辑推荐度 0~100
        }
    }
```    
回复报文
```
    {
        type: "MSG_TYPE_EDIT_EDIT_NEWS",
        ret: 0, // 非0 时，携带errStr字段，不携带data
    }
````
#### 1.3.4 总编编辑新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_EDIT_NEWS_2",
        data: {
          id: 1,
          title: "", // 标题
          content: "", //正文（摘要的内容）
          editorScore: 90, //编辑推荐度 0~100
        }
    }
```    
回复报文
```
    {
        type: "MSG_TYPE_EDIT_EDIT_NEWS",
        ret: 0, // 非0 时，携带errStr字段，不携带data
    }
````
#### 1.3.5 发布新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_PUBLISH_NEWS",
        data: {
          idArray: [1, 2, 3] // 发布新闻的id数组
        }
    }
```    
回复报文
```
    {
        type: "MSG_TYPE_EDIT_PUBLISH_NEWS",
        ret: 0, // 非0 时，携带errStr字段，不携带data
    }
````
#### 1.3.6 撤回发布新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_RECALL_NEWS",
        data: {
          idArray: [1, 2, 3] // 发布新闻的id数组
        }
    }
```    
回复报文
```
    {
        type: "MSG_TYPE_EDIT_PUBLISH_NEWS",
        ret: 0, // 非0 时，携带errStr字段，不携带data
    }
````
#### 1.3.7 删除新闻
上报报文
```
    {
        type: "MSG_TYPE_EDIT_DEL_NEWS",
        data: {
          idArray: [1, 2, 3] // 新闻的id数组
        }
    }
```    
回复报文
```
    {
        type: "MSG_TYPE_EDIT_DEL_NEWS",
        ret: 0, // 非0 时，携带errStr字段，不携带data
    }
````
