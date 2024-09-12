# veo-flipboard

## 介绍
uniapp 的 前端组件 封装，画板有正向反向翻动、动画快慢、背景色、数字变动等功能

## 安装教程
本插件支持组件easycom，使用者可以直接按照easycom规范使用

## 使用说明
### 模板
      
```vue
<veo-flipboard style="font-size: 200%;" 
    :width="200" :height="300"
    :num="num1"
    :middleline="true"
    :transition="2000"
    :direction="false"
></veo-flipboard>
```
    
### 程序调用

```javascript
data() {
	return {
        background:'#aad10a',
        num1:0,
        num2:0,
    }
},
onLoad() {
    let num = [0,1,2,3,4,5,6,7,8,9];
    let i = 0;
    setInterval(()=>{
        this.num1 = num[i];
        i++;
        i = i>9 ? 0 : i;
        
    },4000)
},
```

    
## 仓库
> [dcloud 插件](https://ext.dcloud.net.cn/plugin?id=10311) https://ext.dcloud.net.cn/plugin?id=10311
> [gitee](https://gitee.com/veeoo/veo-uniwebsocket) https://gitee.com/veeoo/veo-uniwebsocket
