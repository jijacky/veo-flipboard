<template>
    <view class="card-container" 
    :class="{'card-container-middle-linear':middleline}"
    :style="{...cardContainerStyle,background:background}">
        <div class="card1 card" 
            :style="{...flip1,background:background,...lineHeight}">{{num1}}</div>
        <div class="card2 card" 
            :style="{...flip2,background:background}">{{num1}}</div>
        <div class="card3 card" 
            :style="{...flip3,background:background,...lineHeight}">{{num2}}</div>
        <div class="card4 card" 
            :style="{...flip4,background:background}">{{num2}}</div>
    </view>
</template>

<script>
    export default {
        name: "veo-flipboard",
        props: {
            // 卡片数字
            num: {
                type: [Number, String],
                default: 0
            },
            // 背景色
            background: {
                type: [String],
                default: "#d7d7d7"
            },
            // 尺寸(宽度)
            width: {
                type: [Number, String],
                default: 100
            },
            // 尺寸(高度)
            height: {
                type: [Number, String],
                default: 100
            },
            // 中间横线
            middleline:{
                type: [Boolean,String],
                default: true
            },
            // 动画时间
            transition:{
                type: [Number, String],
                default: 500
            },
            // 翻动方向
            direction:{
                type: [Boolean,String],
                default: true
            }
        },
        computed: {
            cardContainerStyle:function(){
                return {
                    "width": this.width + 'px',
                    "height": this.height + 'px'
                };
            },
            lineHeight:function(){
                return {
                    "line-height":this.height + 'px',
                }
            }
        },
        watch: {
            num(newVal, oldVal){
                if(this.direction){
                    this.forward(newVal, oldVal);
                }else{
                    this.backward(newVal, oldVal);
                }
            }
        },
        data() {
            return {
                numflag: true,
                num1: null,
                num2: null,
                flip1:{},
                flip2:{},
                flip3:{},
                flip4:{},
            }
        },
        methods: {
            // backward or forward
            forward(val,old) {
                if(this.numflag){
                    // 第 1 组动作
                    // 变动数字 1、2数字
                    this.num1 = val;
                    
                    // 分解1 2、3显式翻动
                    this.flip1 = {
                        "z-index": "10"
                    };
                    this.flip2 = {
                        "z-index": "10",
                        "transform": "rotateX(0deg)",
                        "transition": this.transition + "ms"
                    };
                    this.flip3 = {
                        "z-index": "9",
                        "transform": "rotateX(-180deg)",
                        "transition": this.transition + "ms"
                    };
                    this.flip4 = {
                        "z-index": "9"
                    };
                    
                    // 分解2 3、4隐式翻动
                    setTimeout(()=>{
                        this.flip1 = {
                            "z-index": "10",
                        };
                        this.flip2 = {
                            "z-index": "10",
                            "transform": "rotateX(0deg)"
                        };
                        this.flip3 = {
                            "z-index": "9",
                            "transform": "rotateX(0deg)",
                            "transition": "0ms"
                        };
                        this.flip4 = {
                            "z-index": "9",
                            "transform": "rotateX(180deg)",
                            "transition": "0ms"
                        };
                    },this.transition+1);
            
                }else{
                    // 第 2 组动作
                    // 变动数字 3、4数字
                    this.num2 = val;
                    
                    // 分解1 4、1显式翻动
                    this.flip1 = {
                        "z-index": "9",
                        "transform": "rotateX(-180deg)",
                        "transition": this.transition + "ms"
                    };
                    this.flip2 = {
                        "z-index": "9",
                        "transform": "rotateX(0deg)"
                    };
                    this.flip3 = {
                        "z-index": "9",
                        "transform": "rotateX(0deg)"
                    };
                    this.flip4 = {
                        "z-index": "10",
                        "transform": "rotateX(0deg)",
                        "transition": this.transition + "ms"
                    };
                    
                    // 分解2 1、2隐式翻动
                    setTimeout(()=>{
                        this.flip1 = {
                            "z-index": "9",
                            "transition": "0ms"
                        };
                        this.flip2 = {
                            "z-index": "9",
                            "transition": "0ms"
                        };
                        this.flip3 = {
                            "z-index": "10",
                            "transform": "rotateX(0deg)"
                        };
                        this.flip4 = {
                            "z-index": "10",
                            "transform": "rotateX(0deg)"
                        };
                    },this.transition+1);
                    
                }
                
                this.numflag = !this.numflag;
            },
            backward(val,old) {
                if(this.num1 === null){
                    this.flip1 = {
                        "z-index": "9",
                        "transform": "rotateX(-180deg)",
                        "transition": "0ms"
                    };
                    this.flip2 = {
                        "z-index": "9",
                        "transform": "rotateX(0deg)",
                        "transition": "0ms"
                    };
                    this.flip3 = {
                        "z-index": "10",
                        // "transform": "rotateX(0deg)"
                    };
                    this.flip4 = {
                        "z-index": "10",
                        // "transform": "rotateX(0deg)"
                    };
                }
                if(this.numflag){
                    // 第 1 组动作
                    // 变动数字 1、2数字
                    this.num1 = val;
                    
                    // 分解1 1、4显式翻动
                    this.flip1 = {
                        "z-index": "10",
                        "transition": this.transition + "ms"
                    };
                    this.flip2 = {
                        "z-index": "9",
                        "transform": "rotateX(0deg)"
                    };
                    this.flip3 = {
                        "z-index": "9"
                    };
                    this.flip4 = {
                        "z-index": "9",
                        "transform": "rotateX(180deg)",
                        "transition": this.transition + "ms"
                    };
                    
                    // 分解2 3、4隐式翻动
                    setTimeout(()=>{
                        this.flip1 = {
                            "z-index": "10",
                        };
                        this.flip2 = {
                            "z-index": "10",
                            "transform": "rotateX(0deg)"
                        };
                        this.flip3 = {
                            "z-index": "9",
                            "transform": "rotateX(-180deg)",
                            "transition": "0ms"
                        };
                        this.flip4 = {
                            "z-index": "9",
                            "transition": "0ms"
                        };
                    },this.transition+1);
                            
                }else{
                    // 第 2 组动作
                    // 变动数字 3、4数字
                    this.num2 = val;
                    
                    // 分解1 2、3显式翻动
                    this.flip1 = {
                        "z-index": "9",
                    };
                    this.flip2 = {
                        "z-index": "9",
                        "transform": "rotateX(180deg)",
                        "transition": this.transition + "ms"
                    };
                    this.flip3 = {
                        "z-index": "9",
                        "transform": "rotateX(0deg)",
                        "transition": this.transition + "ms"
                    };
                    this.flip4 = {
                        "z-index": "9",
                    };
                    
                    // 分解2 1、2隐式翻动
                    setTimeout(()=>{
                        this.flip1 = {
                            "z-index": "9",
                            "transform": "rotateX(-180deg)",
                            "transition": "0ms"
                        };
                        this.flip2 = {
                            "z-index": "9",
                            "transform": "rotateX(0deg)",
                            "transition": "0ms"
                        };
                        this.flip3 = {
                            "z-index": "10",
                        };
                        this.flip4 = {
                            "z-index": "10",
                        };
                    },this.transition+1);
                    
                }
                
                this.numflag = !this.numflag;
            }
        }
    }
</script>
<style>
    page {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .card-container{
        background: #d7d7d7;
        width: 100px;
        height: 100px;
        position: relative;
        perspective: 500px;
    }
   .card-container-middle-linear::before{
        content: '';
        position: absolute;
        left: 0;
        top: 50%;
        height: 2px;
        background: linear-gradient(to bottom,#000,#000 1px,#fff 1px);
        width: 100%;
        margin-top: -1px;
        z-index: 99;
    }
    .card{
        position: absolute;
        width: 100%;
        height: 50%;
        left: 0;
        top: 0;
        overflow: hidden;
    }
    .card1{
        background: #d7d7d7;
        line-height: 100px;
        z-index: 9;
        
        transform-origin: center bottom;
        backface-visibility: hidden;
        /* transition: 3s; */
    }
    .card2{
        top: 50%;
        background: #d7d7d7;
        line-height: 0;
        z-index: 9;

        transform-origin: center top;
        backface-visibility: hidden;
        /* transition: 3s; */
        
        transform: rotateX(180deg);
    }
    .card3{
        background: #d7d7d7;
        line-height: 100px;
        z-index: 10;
        
        transform-origin: center bottom;
        backface-visibility: hidden;
        /* transition: 3s; */
    }
    .card4{
        top: 50%;
        background: #d7d7d7;
        line-height: 0;
        z-index: 10;
        
        transform-origin: center top;
        backface-visibility: hidden;
        /* transition: 3s; */
    }
</style>

