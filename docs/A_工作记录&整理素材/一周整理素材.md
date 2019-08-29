#### 2019/8/14
---
 - vant:轻量移动端组件库(感觉很适合做电商类H5)
 - 骨架屏：移动端没有加载出数据时显示优化


#### echarts
- 矩阵树图数据格式
```js
function(ec) {
    var myChart = ec.init(document.getElementById("main"));
    var option = {
        title : {
            text: 'A公司员工吃水果统计表',
            subtext: '多吃水果有益身体健康'
        },
        tooltip : {
            trigger: 'item',
            formatter: "{b}: {c}"
        },
        toolbox: {
            show : true,
            feature : {
                mark : {show: true},
                dataView : {show: true, readOnly: false},
                restore : {show: true},
                saveAsImage : {show: true}
            }
        },
        calculable : false,
        series : [
            {
                name:'矩形图',
                type:'treemap',
                itemStyle: {
                    normal: {
                        label: {
                            show: true,
                            formatter: "{b}"
                        },
                        borderWidth: 1
                    },
                    emphasis: {
                        label: {
                            show: true
                        }
                    }
                },
                data:[
                    {
                        name: '苹果',
                        value: 6
                    },
                    {
                        name: '香蕉',
                        value: 4
                    },
                    {
                        name: '猕猴桃',
                        value: 4
                    },
                    {
                        name: '梨',
                        value: 2
                    },
                    {
                        name: '橙子',
                        value: 2
                    },
                    {
                        name: '桔子',
                        value: 1
                    },
                    {
                        name: '西瓜',
                        value: 1
                    }
                ]
            }
        ]
    };
    myChart.setOption(option);
}
```

- 饼图
```js
option = {
    tooltip: {
        trigger: 'item',
        formatter: "{a} <br/>{b}: {c} ({d}%)"
    },
    legend: {
        orient: 'vertical',
        x: 'left',
        data:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎']
    },
    series: [
        {
            name:'访问来源',
            type:'pie',
            radius: ['50%', '70%'],
            avoidLabelOverlap: false,
            label: {
                normal: {
                    show: false,
                    position: 'center'
                },
                emphasis: {
                    show: true,
                    textStyle: {
                        fontSize: '30',
                        fontWeight: 'bold'
                    }
                }
            },
            labelLine: {
                normal: {
                    show: false
                }
            },
            data:[
                {value:335, name:'直接访问'},
                {value:310, name:'邮件营销'},
                {value:234, name:'联盟广告'},
                {value:135, name:'视频广告'},
                {value:1548, name:'搜索引擎'}
            ]
        }
    ]
}
```

- 散点图
```js
option = {
    xAxis: {},
    yAxis: {},
    series: [{
        symbolSize: 20,
        data: [
            [20.0, 8.04], //20.0表示x轴值，8.04表示y轴值
            [8.0, 6.95],
            [13.0, 7.58],
            [9.0, 8.81],
            [11.0, 8.33],
            [14.0, 9.96],
            [6.0, 7.24],
            [4.0, 4.26],
            [12.0, 10.84],
            [7.0, 4.82],
            [5.0, 5.68]
        ],
        type: 'scatter'
    }]
}
```

- 词云
```js
wordCloudOption:{
    tooltip: {show:true},
    legend: {
        left:'20%',
        bottom:0,
        // itemWidth:15,
        // itemHeight:5,
        icon:'none',
        formatter: function (name) {
            return name;
        },
        textStyle: {
            color: '#000'          // 图例文字颜色
        }
    },
    series: [{
        maskImage:maskImage,
        gridSize: 2,
        name:'宜山路店',
        type: 'wordCloud',
        sizeRange: [12, 55],
        rotationRange: [-45, 0, 45, 90],
        textPadding: 0,
        // shape: 'pentagon',
        autoSize: {
            enable: true,
            minSize: 10
        },
        width: '90%',
        height: '85%',
        top: 10,
        bottom: 10,
        // left:10,
        // right: 10,
        textStyle: {
            normal: {
                color:function(){
                    var colors = ['#f39352', '#A18CCA', '#378BCE', "#A8D98D", "#6291c2"];
                    return colors[parseInt(Math.random() * 10)];
                },
            },
            // emphasis: {
            //     shadowBlur: 10,
            //     shadowColor: '#333'
            // }
        },
        data: [{name:'便宜',value:1231},{name:'好吃',value:121}],
    }]
}
```
- 柱状图
```js
barlineOption: {
    tooltip: {
        trigger: 'axis',
    },
    color:['#FE9000','#65ADDD','#FDC018','#9BA3B7'],
    grid:{
        left:'5%',
        right:'4%',
        bottom:'20%'
    },
    legend: {
        data:['德克士-北京','德克士-上海'],
        top:0,
        // bottom:0,
        // right:40,
        // padding:20,
    },
    dataZoom:[
        {
            type: 'slider',//数据滑块
            start:0,
            end:10,
            start:0,
            left:0,
            right:5,
            bottom:0,
            handleIcon: 'M10.7,11.9v-1.3H9.3v1.3c-4.9,0.3-8.8,4.4-8.8,9.4c0,5,3.9,9.1,8.8,9.4v1.3h1.3v-1.3c4.9-0.3,8.8-4.4,8.8-9.4C19.5,16.3,15.6,12.2,10.7,11.9z M13.3,24.4H6.7V23h6.6V24.4z M13.3,19.6H6.7v-1.4h6.6V19.6z',
            handleSize: '80%',
            height:25,
            handleStyle: {
                color: '#fff',
                shadowBlur: 3,
                shadowColor: 'rgba(0, 0, 0, 0.6)',
                shadowOffsetX: 2,
                shadowOffsetY: 2
            },
        },
        {
            type:'inside',//使鼠标在图表中时滚轮可用
            start:0,
            end:10,
        }
    ],
    xAxis: [
        {
            type: 'category',
            data: ['很大','干净','方便'],
            axisPointer: {
                type: 'shadow'
            },
            axisTick: {
                alignWithLabel: true
            },
        }
    ],
    yAxis: [
        {
            type: 'value',
            name: '评论(次数)',
            axisLine: {
                lineStyle: {
                    color: '#FE9000'
                }
            },
            axisLabel: {
                formatter: '{value}'
            },
            splitLine:{
                show: false,
                lineStyle:{
                    color:'#f1f1f1'
                }
            },
            splitArea:{
                show:true,
                areaStyle:{
                    color:['#FAFAFA','#fff']
                }
            }
        }
    ],
    series: [
        {
            name: '德克士-北京',
            type: 'bar',
            barMaxWidth:45,
            barGap:'10%',
            barCategoryGap:'30%',
            data: [43,44,45]
        },
        {
            name: '德克士-上海',
            type: 'bar',
            barMaxWidth:45,
            barGap:'10%',
            barCategoryGap:'30%',
            data: [84,106,99]
        }
    ]
}
```

- 拆线图
```js
lineOption:{
    color:['#e9b0f6','#65ADDD','#FDC018','#9BA3B7','#FE9000'],
    tooltip: {
        trigger: 'axis'
    },
    legend: {
        data:['淘宝','天猫','京东','小红书','甄会选']
    },
    grid:{
        left:'5%',
        right:'4%',
        bottom:'20%'
    },
    dataZoom:[
        {
            type: 'slider',//数据滑块
            start:0,
            end:10,
            start:0,
            left:0,
            right:5,
            bottom:0,
            handleIcon: 'M10.7,11.9v-1.3H9.3v1.3c-4.9,0.3-8.8,4.4-8.8,9.4c0,5,3.9,9.1,8.8,9.4v1.3h1.3v-1.3c4.9-0.3,8.8-4.4,8.8-9.4C19.5,16.3,15.6,12.2,10.7,11.9z M13.3,24.4H6.7V23h6.6V24.4z M13.3,19.6H6.7v-1.4h6.6V19.6z',
            handleSize: '80%',
            height:25,
            handleStyle: {
                color: '#fff',
                shadowBlur: 3,
                shadowColor: 'rgba(0, 0, 0, 0.6)',
                shadowOffsetX: 2,
                shadowOffsetY: 2
            }
        },
        {
            type:'inside'//使鼠标在图表中时滚轮可用
        }
    ],
    xAxis: {
        type: 'category',
        boundaryGap: false,
        axisTick: {
            alignWithLabel: true
        },
        axisLabel:{
            showMaxLabel:true
        },
        axisLine: {
            onZero: false,
            lineStyle: {
                color: '#333'
            }
        },
        data: ['8:00','9:00','10:00','11:00','12:00','13:00','14:00']
    },
    yAxis: [{
        type: 'value',
        name: '价格(元)',
        position: 'left',
        axisLine: {
            lineStyle: {
                color: '#FE9000'
            }
        },
        axisLabel: {
            formatter: '{value}'
        },
        splitLine:{
            show: false,
            lineStyle:{
                color:'#f1f1f1'
            }
        },
        splitArea:{
            show:true,
            areaStyle:{
                color:['#FAFAFA','#fff']
            }
        }
    }],
    series: [
        {
            name:'淘宝',
            type:'line',
            // stack: '总量',
            data:[89, 92, 85, 82, 79, 88, 98]
        },
        {
            name:'天猫',
            type:'line',
            // stack: '总量',
            data:[165, 145, 148, 155, 156, 160, 145]
        },
        {
            name:'京东',
            type:'line',
            // stack: '总量',
            data:[199, 178, 189, 187, 178, 188, 189]
        },
        {
            name:'小红书',
            type:'line',
            // stack: '总量',
            data:[288, 298, 285, 310, 322, 300, 296]
        },
        {
            name:'甄会选',
            type:'line',
            // stack: '总量',
            data:[216, 210,198, 188, 200, 185, 210]
        }
    ]
}
```

- 饼图
```js
pieOption:{
    color:['#FDC018','#FE9000','#65ADDD','#9BA3B7'],
    tooltip: {
        trigger: 'item',
        formatter: "{b}: {c} ({d}%)"
        // formatter: "{a} {b}: {c} ({d}%)"
    },
    grid: {  
        left: '8%',  
        right: '0',  
        bottom: '1%',  
        containLabel: true  
    } ,
    series: [
        {
            // name:'访问来源',
            type:'pie',
            radius: ['50%', '65%'],
            label: {
                normal: {
                    // position:'inside',
                    // color:'#000',
                    // formatter: '{b|{b}}\n{c}',
                    formatter:function(params){
                        if(params.name){
                            return params.name.split('-')[0] + '\n' + params.name.split('-')[1] +　'(' + params.value + ')';
                        }
                    },
                    lineHeight:18,
                    rich: {
                        a:{
                            lineHeight:38,
                        },
                        b: {
                            fontSize: 12,
                            lineHeight: 38
                        },
                        per: {
                            color: '#eee',
                            backgroundColor: '#334455',
                            padding: [2, 4],
                            borderRadius: 2
                        }
                    }
                }
            },
            labelLine:{
                length:0,
                smooth:true,
            },
            // center:['100%','100%'],
            data:[
                {value:335, name:'宜山路店'},
                {value:310, name:'W广场店'},
                {value:234, name:'七宝店'},
                {value:135, name:'龙阳店'}
            ]
        }
    ]
}
```

- 雷达图
```js
radarOption:{
    color:['#9BA3B7','#65ADDD','#FE9000','#FDC018'],
    legend: {
        x: 'center',
        y:'bottom',
        // left:0,
        // right:0,
        data:['龙阳店','W广场店','七宝店','宜山路店']
    },
    tooltip: {
        trigger: 'axis'
    },
    radar: [
        {
            indicator: [
                {text: '酸', max: 100},
                {text: '甜', max: 100},
                {text: '苦', max: 100},
                {text: '辣', max: 100},
                {text: '咸', max: 100},
                {text: '香', max: 100}
            ],
            radius:70,
            center: ['50%','40%'],
        }
    ],
    series: [
        {
            type: 'radar',
            // radarIndex: 1,
            tooltip: {
                trigger: 'item'
            },
            itemStyle: {normal: {areaStyle: {type: 'default'}}},
            data: [
                {
                    value: [85, 90, 90, 95, 95,40],
                    name: '龙阳店'
                },
                {
                    value: [95, 80, 95, 90, 93,55],
                    name: 'W广场店'
                },
                {
                    value: [35, 90, 30, 55, 95,40],
                    name: '七宝店'
                },
                {
                    value: [65, 50, 95, 70, 83,55],
                    name: '宜山路店'
                }
            ]
        }
    ]
}
```
 