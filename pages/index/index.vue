<template>
	<view class="content">
		<!-- 使用示例 -->
		<view class="code-examples">
			<veo-flipboard style="font-size: 200%;" 
            :width="200" :height="300"
            :num="num1"
            :middleline="true"
            :transition="2000"
            :direction="false"
            ></veo-flipboard>
            <div></div>
            <veo-flipboard style="" 
            :width="200" :height="300" 
            :middleline="true"
            :background='background'
            :transition="2000"
            :num="num1"
            ></veo-flipboard>
		</view>
	</view>
</template>

<script>
	export default {
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
		methods: {
		}
	}
</script>

<style>
    page {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
	.code-examples {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        height: 100vh;
        background: #353535;
        padding-top: 100px;
        font-size: 4em;
        color: #333;
        font-family: Arial, Helvetica, sans-serif;
        text-align: center;
    }
</style>
