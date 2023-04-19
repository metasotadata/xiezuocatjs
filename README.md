# xiezuocatjs
对智能纠错、智能改写、AI写作、单点登录签名算法进行封装<br />
关于具体接口的调用方法与参数说明，请访问[写作猫API文档中心](https://apidocs.xiezuocat.com/guide/)
## 一、npm引入
```js
npm install xiezuocatjs

import Xiezuocat from 'xiezuocatjs/src/xiezuocat.js'
```

## 二、调用示例
### 1、智能纠错
#### 调用示例
```js
var checkData = JSON.stringify({
  "texts": [
    "河北省赵县的洨河上，有一座世界文明的石拱桥，叫安济桥，又叫赵州桥。",
    "它是隋朝的石匠李春涉及和参加建造的，到现在已经有一千三百多年了。"
  ]
});
var xiezuocat = new Xiezuocat({your-secretKey});
xiezuocat.check(checkData).then(res => {
  console.log(JSON.stringify(res.data));
}).catch(err => {
  console.error(err);
})
```
#### 返回结果
```json
{"errCode":0,"errMsg":"","data":null,"alerts":[[{"alertType":4,"alertMessage":"建议用“闻名”替换“文明”。","sourceText":"文明","replaceText":"闻名","start":15,"end":16,"errorType":1,"advancedTip":false}],[{"alertType":4,"alertMessage":"建议用“设计”替换“涉及”。“涉及”指关联到，牵涉到。“设计”指根据一定要求﹐对某项工作预先制定图样﹑方案。","sourceText":"涉及","replaceText":"设计","start":9,"end":10,"errorType":1,"advancedTip":false}]],"checkLimitInfo":{"checkWordCountLeftToday":"996730","totalCheckWordCountLeft":"996730","expireDate":"2024-02-02 00:00:00"}}
```
### 2、智能改写
##### 调用示例
```js
var rewriteData = JSON.stringify({
  "items": [
    "河北省赵县的洨河上，有一座世界文明的石拱桥，叫安济桥，又叫赵州桥。它是隋朝的石匠李春涉及和参加建造的，到现在已经有一千三百多年了。"
  ],
  "level": "middle"
});
var xiezuocat = new Xiezuocat({your-secretKey});
xiezuocat.rewrite(rewriteData).then(res => {
  console.log(JSON.stringify(res.data));
}).catch(err => {
  console.error(err);
})
```
##### 返回结果
```json
{"errcode":0,"errmsg":null,"items":["河北省赵县境内，有一座名为“安济桥”的“赵州桥”，是一座举世闻名的“世界文化遗产”。这座桥由李春参与修建，距今已有1300年之久。"],"stat":"996730"}
```

### 3、AI写作
#### 创建生成任务
##### 调用示例
```js
var generateParams = JSON.stringify({
  "type": "Step",
  "title": "仿生人会梦见电子羊吗",
  "length": "default"
});
var xiezuocat = new Xiezuocat({your-secretKey});
xiezuocat.generate(generateParams).then(res => {
  console.log(JSON.stringify(res.data));
}).catch(err => {
  console.error(err);
})
```
##### 返回结果
```json
{"errCode":0,"errMsg":"success","data":{"docId":"b0906b7e-c7ec-42fd-81c6-98ee48175860"}}
```

#### 获取生成结果
##### 调用示例
```js
var xiezuocat = new Xiezuocat({your-secretKey});
var docId = "b0906b7e-c7ec-42fd-81c6-98ee48175860"; // 此处docId为第一步生成的结果
xiezuocat.getGenerateResult(docId).then(res => {
  console.log(JSON.stringify(res.data));
}).catch(err => {
  console.error(err);
})
```
##### 返回结果
```json
{"errCode":0,"errMsg":"success","data":{"status":"FINISHED","result":"仿生人会梦见电子羊吗\n仿生人会梦见电子羊吗？这是一个科幻电影里的桥段，相信看过科幻的朋友对这个桥段都不陌生。仿生人机器），可以说是当今世界上最先进、最完美的生物技术，而最近又有一部影片《电子羊》，让仿生人“火”了一把，这是一部由好莱坞著名导演克里斯托弗·诺兰执导的科幻电影。《电子羊》讲述了仿生人“电子羊”在未来世界上寻找配偶时，遭遇到“人类情感缺失”，最终只能以一个假名存在。\n1.电子羊的出现，意味着人类情感缺失\n电子羊的出现，意味着人类情感缺失，正如影片中的“你不懂我，我也不懂你”这个句子一样。当仿生人机器人的出现，意味着未来世界中所有情感缺失的人群都将会得到拯救，在未来世界中所有人都会成为“有情感、懂人类、有感情”的仿生人，当仿生人机器人走进千家万户时，“人类情情感缺失”的悲剧就将不再是悲剧。《电子羊》电影给我们一个信息：人类情感缺失是一种普遍存在的现象，而仿生人机器人在未来世界是无法弥补这种现象的。\n2.仿生人能否实现自我认同\n目前，仿生人技术主要有两大方向：\n一是仿生人的自我认同；\n二是机器情感交互系统。仿生人机器之所以被称为“仿生”，是因为它们的行为具有某种程度的“类人化”，即“自我”特征。而这也就意味着，它们不像人类一样具有人类情感。\n3.未来仿生人的前景如何？\n人类的情感缺失是人类社会的共同难题，仿生人也不例外。当仿生人无法满足人类情感需求时，仿生人的命运就可想而知了。其实在电影中我们看到了机器人“电子羊”和她的配偶在一起生活，虽然现实中确实存在这样一种可能，但我们也不能完全否定这种可能性。仿生人与人类之间有共同情感需求，但是这是建立在仿生人具有情感行为基础上的，当人们无法做到像电影中“电子羊”一样，与人建立情感互动时，那么他就会逐渐失去人性。所以说这其实是一种理想化。\n4.为什么没有一个“完整的生命”\n目前，我们在研究生命是如何诞生的，也有科学家试图将其定义为“完整的生命”，但我们至今还没有找到真正意义上的完整生命。为什么会出现这种情况呢？因为没有生物是不完整的，在生物体内，一个生物体内拥有一套复杂的细胞系统（包括有各种细胞类型），如果没有这些基因来进行控制，那么就会出现无法进行自我复制和增殖等现象。但是我们却发现了一些奇怪的现象：在胚胎发育过程中，不同细胞中有不同种类的基因（可以通过 DNA杂交形成单倍体）、甚至是同一类型的基因可以在胚胎早期就通过复制形成双倍体细胞、甚至胚胎干细胞。\n5.未来世界，仿生人还是机器吗？\n随着科技的进步，仿生人技术也在不断地发展和进步，现在世界上已经有了很多的仿生人，而这些仿生人也在不断的改变自己的形态。比如现在人类可以制造出一个机器人，而它并不会像原来的机器人那样思考和行动，而是通过模仿、学习或者说模拟人类的大脑和情绪。所以它与真正的真人还是有很大差别。\n","wordCount":"1141","restCount":"98405"}}
```
### 4、单点登录签名算法
##### 调用示例
```js
var xiezuocat = new Xiezuocat({your-secretKey});
const signature = xiezuocat.getSSOSignature({your-appId}, {your-uid});
console.log(signature);
```
##### 返回结果
```json
eyJhcHBJZCI6Inh4eCIsInVpZCI6ImxsIiwidGltZXN0YW1wIjoxNjgwNTA2MjI2MzgxLCJzaWduIjoiY2M1YzBiZjA0ZDUxZjQ3NmVkOGRiYjVkOWVmNDI5ZTNmZmEyNTUyZjEyMzc4MDgwODI5NGY4ODY0M2I4MjQ3OSJ9
```
##### 拿到签名之后访问下述URL即可登录写作猫
```js
// p为签名算法生成的结果
https://xiezuocat.com/api/open/login?p=eyJhcHBJZCI6Inh4eCIsInVpZCI6ImxsIiwidGltZXN0YW1wIjoxNjgwNTA2MjI2MzgxLCJzaWduIjoiY2M1YzBiZjA0ZDUxZjQ3NmVkOGRiYjVkOWVmNDI5ZTNmZmEyNTUyZjEyMzc4MDgwODI5NGY4ODY0M2I4MjQ3OSJ9
```
