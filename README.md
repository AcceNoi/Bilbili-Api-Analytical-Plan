# Bilbili Api解析计划
**这个项目用来解析B站API，欢迎各位pull request**

## 1. Bilibili动态-by Accen
 https://api.vc.bilibili.com/dynamic_svr/v1/dynamic_svr/space_history 

**GET**

请求参数

| 参数              | 说明              |
| ----------------- | ----------------- |
| visitor_uid       | 游客uid，可以为空 |
| host_uid          | 目标up uid        |
| offset_dynamic_id | offset（不含）    |

返回参数

**JSON**

重要说明：

data.cards[]：动态的数组

data.cards[].card：动态的具体内容（json格式的字符串）

data.cards[].desc.timestamp：*1000后为UNIX时间戳

data.cards[].desc.type：具体的一个动态的类型，已知的有：

| 取值 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| 1    | 转发动态。转发的原始动态在data.cards[].card转成JSON后的orgin（json格式的字符串）中 |
| 2    | 普通动态                                                     |
| 4    | 普通动态，但是格式与2有点区别，貌似也没有图片字段            |
| 8    | 视频动态。视频id（avid）的对应字段为aid                      |
| 16   |                                                              |
| 32   |                                                              |
| 64   | 专栏动态。专栏id（cvid）的对应字段为id                       |
| 128  |                                                              |
| 256  | 音频动态。音频id（auid）的对应字段为id                       |
| 512  | 番剧                                                         |

## 2. B站搜索-by Accen

https://api.bilibili.com/x/web-interface/search/type

**GET**

请求参数

| 参数        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| page        | 分页                                                         |
| keyword     | 搜索关键字                                                   |
| search_type | 搜索类型：<br />bili_user：用户<br />media_ft：影视<br />media_bangumi：番剧<br />video：视频<br />live：直播<br />article：专栏<br />topic：话题<br />photo：相簿<br />（可能还有activity，bangumi，card，live_all，live_master，live_room，live_user，movie，operation_card，pgc，special，tv，upuser，user） |
| order       | 排序                                                         |
| category_id |                                                              |
| order_sort  |                                                              |
| context     |                                                              |


综合搜索
https://api.bilibili.com/x/web-interface/search/all/v2
没有search_type字段，其他和上述基本一致