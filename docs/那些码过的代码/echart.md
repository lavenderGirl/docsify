##### chartsCom.js
```js
// chartsCom.js
let colors = Cfg.colorData[Cfg.colors];

let c_axisLine = 'rgba(76,180,231,0.33)';
let c_bg_bar = 'rgba(76,180,231,0.15)';

//所有图表的公共属性
let com_charts = {
    color: colors,
    grid: {
        top: '25%',
        bottom: '10%'
    },

    textStyle: {
        fontFamily: 'PingFang SC, sans-serif',
        fontSize: 10 * scale
    },
    legend: {
        itemWidth: 20 * scale,
        itemHeight: 10 * scale,
        inactiveColor: '#666',
        lineHeight: 10 * scale,
        textStyle: {
            color: colors[0],
            fontSize: 16 * scale,
        }
    },
    tooltip: {
        textStyle: {
            fontSize: 16 * scale,
            color: colors[0]
        },
    },
};

//直角坐标系坐标轴
let com_axis = {
    axisLabel: { //标签名称
        color: colors[0],
        margin: 8 * scale,
        fontSize: 16 * scale,
    },
    nameTextStyle: { //坐标轴名称
        color: colors[0],
        fontSize: 18 * scale
    },
    nameGap: 16 * scale, //坐标轴名称距离
    axisTick: { //小刻度线
        show: false
    },
    axisLine: { //坐标轴
        show: true,
        lineStyle: {
            color: c_axisLine
        }
    },
    splitLine: { //分割线
        show: false,
        lineStyle:{
            color:['#aaa', '#888'],
            type:'dashed'
        }
    },
    boundaryGap: false
};

//折线图公共属性
let opt_line = $.extend(true, {}, com_charts, {
    xAxis: $.extend(true, {}, com_axis, {
        type: 'category',
    }),
    yAxis: $.extend(true, {}, com_axis, {
        type: 'value',
    }),
    //这里写此类图表其他属性
    tooltip: {
        trigger: 'axis',
    },
});
let seri_line = {
    type: 'line',
    smooth: true,
    lineStyle: {
        width: 1.5 * scale,
        shadowColor: 'rgba(255,255,255,0.4)', //线条外发光
        shadowBlur: 1.5 * scale,
    },
};
let seri_area = $.extend(true, {}, seri_line, {
    areaStyle: {
        color: {
            x: 0,
            y: 0,
            x2: 0,
            y2: 1,
            colorStops: [{
                offset: 0, color: colors[0] // 0% 处的颜色
            }, {
                offset: 1, color: 'transparent' // 100% 处的颜色
            }]
        }
    }
});

// let opt_area = $.extend(true, {}, com_charts,opt_line)
//横条图公共属性
let opt_bar_h = $.extend(true, {}, com_charts, {
    xAxis: $.extend(true, {}, com_axis, {
        type: 'value'
    }),
    yAxis: $.extend(true, {}, com_axis, {
        boundaryGap: true,
        type: 'category'
    }),
});
let seri_bar_h = {
    type: 'bar',
    // symbol: 'circle',
    // showSymbol: false,
    // smooth: true,
    // lineStyle: {
    //     normal: {
    //         width: 1.5 * scale,
    //         shadowColor: 'rgba(255,255,255,0.4)', //线条外发光
    //         shadowBlur: 1.5 * scale,
    //     }
    // },
};
//竖条图公共属性
let opt_bar_v = $.extend(true, {}, com_charts, {
    xAxis: $.extend(true, {}, com_axis, {
        boundaryGap: true,
        type: 'category'
    }),
    yAxis: $.extend(true, {}, com_axis, {
        type: 'value'
    }),
    tooltip: {
        trigger: 'axis',
    }
    //这里写此类图表其他属性
});
let seri_bar_v = {
    type: 'bar',
    barWidth: '60%'

};
//圆环图 series里的属性设置
let circle_series_label = {
    normal: {
        show: true,
        fontSize: 12 * scale
    },
    emphasis: {
        show: true,
        textStyle: {
            fontSize: 15 * scale,
            fontWeight: 'normal'
        }
    }
};


//竖柱条组合图公共属性
let com_lineBar_vertical = $.extend(true, {}, com_charts, {
    xAxis: $.extend(true, {}, com_axis, {
        boundaryGap: true,
        type: 'category'
    }),
    yAxis: [
        {
            min: 0,
            max: 250,
            interval: 50,

        },
        {
            min: 0,
            max: 25,
            interval: 5,
            axisLine: {       //y轴
                show: false
            },
            axisTick: {       //y轴刻度线
                show: false
            },
            splitLine: {     //网格线
                show: false
            }
        }
    ].map(function (item, index) {
        return $.extend(true, {type: 'value'}, com_axis, item);
    }),
    legend: {
        show: true,
        x: 'right',
        y: 'top',
    },
    tooltip: {
        trigger: 'axis',
        backgroundColor: 'rgba(0,51,124,0.8)',
        axisPointer: {
            type: 'shadow',
            shadowStyle: {
                color: "rgba(6,88,255,0.1)",
            }
        },
        textStyle: {
            fontSize: 16 * scale,
            color: '#fff'
        },
    },
    //这里写此类图表其他属性*/
});
let com_lineBarSeries = {
    type: 'bar',
    barGap: 0,
    barWidth: '30%',
    itemStyle: {
        normal: {
            color: new echarts.graphic.LinearGradient(
                0, 0, 0, 1,
                [
                    {offset: 1, color: '#227cff'},
                    //{offset: 0.5, color: '#188df0'},
                    {offset: 0, color: '#2377fe'}
                ]
            )
        }
    },
};

let com_circleSeries = {
    type: 'pie',
    radius: ['45%', '65%'],
}
//散点图公共属性
let opt_scatter = $.extend(true, {}, com_charts, {
    xAxis: $.extend(true, {}, com_axis, {
        type: 'category'
    }),
    yAxis: $.extend(true, {}, com_axis, {
        type: 'category'
    }),

    //这里写此类图表其他属性

});

//雷达图公共属性
let opt_radar = $.extend(true, {}, {
    legend: {
        itemWidth: 7 * scale,
        itemHeight: 7 * scale,
        textStyle: {
            fontSize: 12 * scale,
        },
        top: '2%',
        left: 'right',
        orient: 'vertical'
    },
    tooltip: {
        axisPointer: {
            label: {
                backgroundColor: '#6a7985'
            }
        },
        textStyle: {
            align: 'left',
            fontFamily: 'PingFang SC, sans-serif',
            // fontSize: 15 * scale
        }
    },
    radar: {
        center: ['50%', '58%'],
        // shape: 'circle',
        name: {
            textStyle: {
                color: '#0cf',
                fontSize: 12 * scale
                // backgroundColor: '#999',
                // borderRadius: 3,
                // padding: [3, 5]
            }
        },

        splitArea: {
            areaStyle: {
                color: 'rgba(0,0,0,0)'
            }
        },
        axisLine: {
            lineStyle: {
                color: '#0cf'
            }
        },
        splitLine: {
            lineStyle: {
                color: '#0cf'
            }
        }
    },
});
//饼图公共属性
let opt_pie = $.extend(true, {}, com_charts, {});

let seri_pie = $.extend(true, {}, com_charts, {
    type: 'pie',
    radius: '60%',
    center: ['50%', '55%'],
    label: {
        fontSize: 16 * scale
    },

});
let seri_circle = $.extend(true, {}, com_charts, seri_pie, {
    radius: ['20%', '60%'],

});

function scatterSymbolSize(data) {
    return Math.sqrt(data[2]) * scale / 2;
}

function lineAreaStyle(index) {
    return {
        color: {
            x: 0,
            y: 0,
            x2: 0,
            y2: 1,
            colorStops: [{
                offset: 0, color: colors[index] // 0% 处的颜色
            }, {
                offset: 1, color: '#00adef11' // 100% 处的颜色
            }]
        }
    }

}

// 地图
let geoCoordMap = {
    '上海': [121.4648, 31.2891],
    '东莞': [113.8953, 22.901],
    '东营': [118.7073, 37.5513],
    '中山': [113.4229, 22.478],
    '临汾': [111.4783, 36.1615],
    '临沂': [118.3118, 35.2936],
    '丹东': [124.541, 40.4242],
    '丽水': [119.5642, 28.1854],
    '乌鲁木齐': [87.9236, 43.5883],
    '佛山': [112.8955, 23.1097],
    '保定': [115.0488, 39.0948],
    '兰州': [103.5901, 36.3043],
    '包头': [110.3467, 41.4899],
    '北京': [116.4551, 40.2539],
    '北海': [109.314, 21.6211],
    '南京': [118.8062, 31.9208],
    '南宁': [108.479, 23.1152],
    '南昌': [116.0046, 28.6633],
    '南通': [121.1023, 32.1625],
    '厦门': [118.1689, 24.6478],
    '台州': [121.1353, 28.6688],
    '合肥': [117.29, 32.0581],
    '呼和浩特': [111.4124, 40.4901],
    '咸阳': [108.4131, 34.8706],
    '哈尔滨': [127.9688, 45.368],
    '唐山': [118.4766, 39.6826],
    '嘉兴': [120.9155, 30.6354],
    '大同': [113.7854, 39.8035],
    '大连': [122.2229, 39.4409],
    '天津': [117.4219, 39.4189],
    '太原': [112.3352, 37.9413],
    '威海': [121.9482, 37.1393],
    '宁波': [121.5967, 29.6466],
    '宝鸡': [107.1826, 34.3433],
    '宿迁': [118.5535, 33.7775],
    '常州': [119.4543, 31.5582],
    '广州': [113.5107, 23.2196],
    '廊坊': [116.521, 39.0509],
    '延安': [109.1052, 36.4252],
    '张家口': [115.1477, 40.8527],
    '徐州': [117.5208, 34.3268],
    '德州': [116.6858, 37.2107],
    '惠州': [114.6204, 23.1647],
    '成都': [103.9526, 30.7617],
    '扬州': [119.4653, 32.8162],
    '承德': [117.5757, 41.4075],
    '拉萨': [91.1865, 30.1465],
    '无锡': [120.3442, 31.5527],
    '日照': [119.2786, 35.5023],
    '昆明': [102.9199, 25.4663],
    '杭州': [119.5313, 29.8773],
    '枣庄': [117.323, 34.8926],
    '柳州': [109.3799, 24.9774],
    '株洲': [113.5327, 27.0319],
    '武汉': [114.3896, 30.6628],
    '汕头': [117.1692, 23.3405],
    '江门': [112.6318, 22.1484],
    '沈阳': [123.1238, 42.1216],
    '沧州': [116.8286, 38.2104],
    '河源': [114.917, 23.9722],
    '泉州': [118.3228, 25.1147],
    '泰安': [117.0264, 36.0516],
    '泰州': [120.0586, 32.5525],
    '济南': [117.1582, 36.8701],
    '济宁': [116.8286, 35.3375],
    '海口': [110.3893, 19.8516],
    '淄博': [118.0371, 36.6064],
    '淮安': [118.927, 33.4039],
    '深圳': [114.5435, 22.5439],
    '清远': [112.9175, 24.3292],
    '温州': [120.498, 27.8119],
    '渭南': [109.7864, 35.0299],
    '湖州': [119.8608, 30.7782],
    '湘潭': [112.5439, 27.7075],
    '滨州': [117.8174, 37.4963],
    '潍坊': [119.0918, 36.524],
    '烟台': [120.7397, 37.5128],
    '玉溪': [101.9312, 23.8898],
    '珠海': [113.7305, 22.1155],
    '盐城': [120.2234, 33.5577],
    '盘锦': [121.9482, 41.0449],
    '石家庄': [114.4995, 38.1006],
    '福州': [119.4543, 25.9222],
    '秦皇岛': [119.2126, 40.0232],
    '绍兴': [120.564, 29.7565],
    '聊城': [115.9167, 36.4032],
    '肇庆': [112.1265, 23.5822],
    '舟山': [122.2559, 30.2234],
    '苏州': [120.6519, 31.3989],
    '莱芜': [117.6526, 36.2714],
    '菏泽': [115.6201, 35.2057],
    '营口': [122.4316, 40.4297],
    '葫芦岛': [120.1575, 40.578],
    '衡水': [115.8838, 37.7161],
    '衢州': [118.6853, 28.8666],
    '西宁': [101.4038, 36.8207],
    '西安': [109.1162, 34.2004],
    '贵阳': [106.6992, 26.7682],
    '连云港': [119.1248, 34.552],
    '邢台': [114.8071, 37.2821],
    '邯郸': [114.4775, 36.535],
    '郑州': [113.4668, 34.6234],
    '鄂尔多斯': [108.9734, 39.2487],
    '重庆': [107.7539, 30.1904],
    '金华': [120.0037, 29.1028],
    '铜川': [109.0393, 35.1947],
    '银川': [106.3586, 38.1775],
    '镇江': [119.4763, 31.9702],
    '长春': [125.8154, 44.2584],
    '长沙': [113.0823, 28.2568],
    '长治': [112.8625, 36.4746],
    '阳泉': [113.4778, 38.0951],
    '青岛': [120.38, 36.07],
    '韶关': [113.7964, 24.7028],
    '敦煌': [94.71, 40.13],
    '库尔勒': [86.17369, 41.72643],
    '奎屯': [84.90167, 44.42689],
    '昌吉': [87.30822, 44.01117],
    '克拉玛依': [84.8697, 45.5905],

    '武威': [102.63, 37.93],
    '瓜州': [95.7832282721, 40.5319295174],
    '双塔水库': [95.8618987044, 40.5488634768],
    '哈密': [93.5219246754, 42.8243728820],
    '鄯善': [90.2207332610, 42.8731928218],
    '吐鲁番': [89.1960521828, 42.9572578648],
    '焉耆': [86.5807573704, 42.0652104472],
    '阿克苏': [80.2665024939, 41.1745589469],

    '托克马克': [75.2833, 42.8333],
    '撒马尔罕': [66.965159, 39.651099],
    '古佐尔': [66.258211, 38.612865],
    '巴米扬': [67.832346, 34.821217],
    '喀布尔': [69.189511, 34.562135],
    '白沙瓦': [71.555907, 34.011312],
    '斯利那加': [74.795235, 34.128023],
    '卢迪亚纳': [75.855612, 30.906297],
    '卡瑙杰': [79.919299, 27.065225],
    '那烂陀寺': [85.457013, 25.121574],

    '陕州': [111.103453, 34.720437],
    '洛阳': [112.454331, 34.618038],
    '开封': [114.307571, 34.797395],
    '冲绳岛那霸市': [127.680613, 26.226334],
    '奄美市': [129.493458, 28.376662],
    '屋久岛': [130.394543, 30.371910],
    '佐多岬': [130.659499, 30.997713],
    '南萨摩市鹿儿岛县': [130.318799, 31.418862],
    '长崎': [129.875784, 32.751862],
    '太宰府': [130.521372, 33.515718],
    '难波': [135.500393, 34.667345],
    '奈良东大寺': [135.839815, 34.689066],

    '塞维利亚': [-5.984412, 37.389825],
    '桑卢卡尔－德巴拉梅达': [ -6.352948,36.773200],
    '加纳利群岛': [ -15.501880,28.004794],
    '大西洋辅助点1': [ -20.135627,14.616552],
    '大西洋辅助点2': [ -22.429777,4.321913 ],
    '大西洋辅助点3': [ -31.435243,-6.038134],
    '大西洋辅助点4': [  -36.541832,-12.595625],
    '大西洋辅助点5': [ -38.254773,-20.750359],
    '里约热内卢': [ -43.169265,-22.908516],
    '大西洋辅助点6': [ -47.892756,-27.399968],
    '大西洋辅助点7': [ -50.978379,-32.087062],
    '拉普拉塔河': [ -56.746412,-35.179830],
    '圣胡利安湾': [ -67.714665,-49.312443],
    '维尔赫纳斯角': [ -68.524543,-52.475863],
    '麦哲伦海峡': [-70.725699, -53.540607],
    '希望角': [-70.725699,-53.540607 ],
    '太平洋辅助点1': [ -78.328160,-42.895632],
    '太平洋辅助点2': [ -80.470603, -32.746314],
    '太平洋辅助点3': [  -85.027722, -31.273247],
    '太平洋辅助点4': [   -91.244359, -28.402350],
    '太平洋辅助点5': [   -98.665583, -24.404688],
    '太平洋辅助点6': [   -113.188808,  -23.483444],
    '太平洋辅助点7': [  -125.387639, -21.746314],
    '太平洋辅助点8': [  -133.928313, -17.850126],
    '太平洋辅助点9': [  -145.928313, -15.850126],
    // '太平洋辅助点2': [ -80.470603, -32.746314],
    '普卡普卡岛': [ -138.819320 ,-14.829683],
    '弗林特岛': [ -151.8,-11.1],
    '太平洋辅助点10': [  -160.928313, -9.850126],
    '太平洋辅助点11': [  -168.928313, -8.850126],
    '太平洋辅助点12': [  -178.928313, -5.850126],
    '太平洋辅助点13': [  -188.928313, -2.850126],
    '太平洋辅助点14': [  -198.928313, 5.850126],
    '太平洋辅助点15': [  -205.928313, 7.850126],
    '马里亚纳群岛': [ 145.209632,14.164687 ],
    '太平洋辅助点16': [  137.928313, 12.850126],
    '太平洋辅助点17': [  129.928313, 11.850126],
    '萨玛1': [ 125.638948,11.243016],
    '萨玛2': [ 125.852730,10.903617],
    '霍蒙洪岛': [ 125.686260,10.826970],
    '菲律宾群岛辅助点': [ 125.347643,9.809548],
    '利马萨瓦': [ 125.064417,9.961198],
    '宿雾岛': [123.803228, 10.235243],
    '麦克坦': [ 123.980188,10.332247],
    '巴拉望': [ 118.634276,9.435080],
    '蒂多雷': [ 127.390863,0.697616],
    '安汶岛': [128.096533,-3.527012 ],
    '帝汶': [124.179756, -9.236652],
    '印度洋辅助点1': [  109.726788, -15.147889],
    '印度洋辅助点2': [  99.726788, -18.047889],
    '印度洋辅助点3': [  85.726788, -23.147889],
    '印度洋辅助点4': [  76.726788, -29.147889],
    '印度洋辅助点5': [  66.726788, -35.147889],
    '印度洋辅助点6': [  56.726788, -39.147889],
    '印度洋辅助点7': [  43.726788, -39.147889],
    '印度洋辅助点7': [  39.726788, -39.947889],
    '印度洋辅助点8': [  29.726788, -40.147889],
    '好望角': [ 18.473927,-34.356817],
    '大西洋返回辅助点1': [ 9.384907,-27.079606],
    '大西洋返回辅助点2': [ 2.778027,-19.928112],
    '大西洋返回辅助点3': [ -2.945186,-12.617718],
    '大西洋返回辅助点4': [ -12.135627,-6.616552],
    '大西洋返回辅助点5': [ -20.135627,0.616552],
    '大西洋返回辅助点6': [ -23.135627,8.616552],
    '大西洋返回辅助点7': [ -24.135627,15.616552],
    '大西洋返回辅助点8': [ -20.135627,26.616552],
    '大西洋返回辅助点9': [ -14.135627,32.616552],
    '塞维利亚': [-5.984412, 37.389825],

};

```

#### common.js
```js
/**
 * Created by Administrator on 2019/4/19.
 */
const settings = JSON.parse(localStorage.getItem('settings')) || {};
const Cfg = {
    designW: settings.designW || 1920, //设计图宽度
    designH: settings.designH || 1080, //设计图高度
    zoomMode: settings.zoomMode || (innerWidth < 768 ? 'cover' : 'contain'),
    notebookOptim: [undefined, true].includes(settings.notebookOptim),
    getWeatherPeriod: settings.getWeatherPeriod || 5, //天气预报更新周期（分）
    chartRefreshPeriod: settings.chartRefreshPeriod || 10, // 图表刷新周期（秒）
    colors: settings.colors || 'default',
    colorData: {//配色方案，部分色彩参考 http://rmco.jp/coloringroom/haisyoku_rei/haisyoku_haru.html
        default: ['lightskyblue', 'orange', 'greenyellow', 'limegreen',
            'mediumturquoise', 'mediumpurple'],
        spring: ['#BEDC6E', '#FA8C8C', '#FAAAC8', '#FAC8C8',
            '#FFFFE6', '#6E6464'],
        summer: ['#FFAE00', '#FF5200', '#007AFF', '#00BF05',
            '#DCFFFF', '#505064'],
        autumn: ['#c1ad2f',/*'#A5912D',*/ '#782323', '#783723', '#A05027',
            '#FAE6DC', '#283C14'],
        winter: ['#F5F5FA', '#96822D', '#6E5A19', '#BECDEB',
            '#E1E1F0', '#281E1E'],
    }
};
let hasGetWeather = false;
let scale = 1;
let notebookOptim = true;
let colonShow = true;
let [pageH, pageW] = [$(window).height(), $(window).width()];
const weather2Code = {
    "晴": 100,
    "多云": 101,
    "少云": 102,
    "晴间多云": 103,
    "阴": 104,
    "有风": 200,
    "平静": 201,
    "微风": 202,
    "和风": 203,
    "清风": 204,
    "强风/劲风": 205,
    "疾风": 206,
    "大风": 207,
    "烈风": 208,
    "风暴": 209,
    "狂爆风": 210,
    "飓风": 211,
    "龙卷风": 212,
    "热带风暴": 213,
    "阵雨": 300,
    "强阵雨": 301,
    "雷阵雨": 302,
    "强雷阵雨": 303,
    "雷阵雨伴有冰雹": 304,
    "小雨": 305,
    "中雨": 306,
    "大雨": 307,
    "极端降雨": 308,
    "毛毛雨/细雨": 309,
    "暴雨": 310,
    "大暴雨": 311,
    "特大暴雨": 312,
    "冻雨": 313,
    "小到中雨": 314,
    "中到大雨": 315,
    "大到暴雨": 316,
    "暴雨到大暴雨": 317,
    "大暴雨到特大暴雨": 318,
    "雨": 399,
    "小雪": 400,
    "中雪": 401,
    "大雪": 402,
    "暴雪": 403,
    "雨夹雪": 404,
    "雨雪天气": 405,
    "阵雨夹雪": 406,
    "阵雪": 407,
    "小到中雪": 408,
    "中到大雪": 409,
    "大到暴雪": 410,
    "雪": 499,
    "薄雾": 500,
    "雾": 501,
    "霾": 502,
    "扬沙": 503,
    "浮尘": 504,
    "沙尘暴": 507,
    "强沙尘暴": 508,
    "浓雾": 509,
    "强浓雾": 510,
    "中度霾": 511,
    "重度霾": 512,
    "严重霾": 513,
    "大雾": 514,
    "特强浓雾": 515,
    "热": 900,
    "冷": 901,
    "未知": 999,
};
const Public = {
    hasVal(val) {
        if (val === null) {
            return '-';
        }
        return val;
    },
    // 页面顶部时间
    setHeaderTime() {
        setTimeout(function () {
            let t = new Date();
            let [year, mon, date, hour, min, sec, milliSec] = [
                t.getFullYear(),
                t.getMonth() + 1,
                t.getDate(),
                t.getHours(),
                t.getMinutes(),
                t.getSeconds(),
                t.getMilliseconds()
            ];
            let timeHtml = `
                <span class="date"> ${year}-${mon}-${date}</span>
                <span class="digital-num">
                    ${hour} 
                    <span class="colon" style="">${colonShow ? ' :' : '&nbsp;'}</span>
                    ${(min + "").padStart(2, '0')}
                </span>`;
            colonShow = !colonShow;
            $("#headerTime").html(timeHtml);
            if (!hasGetWeather) {
                Public.getWeather(t);
                hasGetWeather = true;
            } else {
                if (min % Cfg.getWeatherPeriod === 0 && sec === 0 && milliSec < 500) {
                    Public.getWeather(t);
                }
            }
            Public.setHeaderTime();
        }, 500)
    },
    // 获取天气情况
    getWeather(currTime) {
        // 获取地理位置
        $.get({
            //这里的url不能写到data对象的外面
            url: 'https://api.asilu.com/weather_v2/',
            dataType: 'jsonp',  // 请求方式为jsonp
            success: function (data) {
                const city = data.forecasts[0].city;
                let temperatureTxt = '';
                let daily_forecast = data.forecasts[0].casts[0];
                let [code, txt] = ['', ''];
                if ((currTime.getHours() >= 6) && (currTime.getHours() < 18)) {
                    txt = daily_forecast.dayweather;
                    temperatureTxt = daily_forecast.nighttemp + "℃~" + daily_forecast.daytemp + "℃";
                } else {
                    txt = daily_forecast.nightweather;
                    temperatureTxt = daily_forecast.daytemp + "℃~" + daily_forecast.nighttemp + "℃";
                }
                $("#weather").html(txt + '&emsp;' + city);
                $("#temperature").text(temperatureTxt);
                $("#weatherIcon").css('background-image', `url("https://cdn.heweather.com/cond_icon/${weather2Code[txt]}.png")`);
            }
        })

    },
    //页面缩放
    pageResize() {
        [pageH, pageW] = [$(window).height(), $(window).width()];
        let isWider = pageW / pageH > Cfg.designW / Cfg.designH;
        let [scaleW, scaleH] = [pageW / Cfg.designW, pageH / Cfg.designH];
        let $container = $("#container");
        switch (Cfg.zoomMode) {
            case "contain":
                if (isWider) {
                    $container.css({width: pageH * Cfg.designW / Cfg.designH, height: '100%'});
                } else {
                    $container.css({height: pageW * Cfg.designH / Cfg.designW, width: '100%'});
                }
                scale = isWider ? scaleH : scaleW;
                break;
            case 'cover':
                $("html,body").css('overflow', 'initial');
                if (isWider) {
                    $container.css({height: pageW * Cfg.designH / Cfg.designW, width: '100%'});
                } else {
                    $container.css({width: pageH * Cfg.designW / Cfg.designH, height: '100%'});
                }
                scale = isWider ? scaleW : scaleH;
                break;
            case 'stretch':
                scale = isWider ? scaleH : scaleW;
                $container.css({width: '100%'}, {height: '100%'});
                break;
        }
        $("html").css("font-size", scale * 16 + "px").css("opacity", 1);
        notebookOptim = !(Cfg.notebookOptim === false || scale > .75);
        // console.log("~~~~~~~~~窗口高度：" + pageH + ",\n宽度:" + pageW + " \nbody字号：" + scale)
    },
    //图表缩放
    chartsResize(charts, param) {
        $(window).resize(() => {
            Object.keys(charts).forEach(id => {
                if (param && param.notResize.includes(id)) {
                    return
                }
                charts[id].resize();
            })
        });
    },
    /**
     *
     * @param charts
     * @param t 默认刷新时间（秒）
     * @param noRefresh 无需刷新的图表
     * @param someRefresh 指定要刷新的图表，有重复指定的图表时优先权高于noRefresh
     */
    chartsReDraw(charts, t = Cfg.chartRefreshPeriod, noRefresh, someRefresh) {
        let counter = setInterval(() => {
            Object.keys(charts).forEach(item => {
                if (noRefresh && noRefresh.includes(item) && !(someRefresh && someRefresh.includes(item))) return;
                let chart = charts[item];
                let opt = chart.getOption();
                chart.clear();
                chart.setOption(opt);
            })
        }, (t || Cfg.chartRefreshPeriod) * 1000)

    },
    // 自定义方法
    initTools() {
        $.fn.extend({
            /**
             * 将文本转为数字并保留相应小数位数
             * @param n 小数位数
             * @param power 数据缩放到10的多少次方
             * @param str 后面可以跟上个字符串，比如‘%’
             */
            str2NumFixed: function (n, power, str = '') {
                $.each($(this), function () {
                    $(this).text(Public.hasVal(parseFloat($(this).text() + 'e' + power).toFixed(n) + str));
                })
            }
        })
    }
};

//jsonP
function onBack(data) {
}

Public.pageResize();
let init = () => {
    Public.initTools(); // 自定义方法
};

$(window).resize(() => {
    Public.pageResize();
});

$(function () {
    // 加载源不能写成body>header>*,原因不明
    $('#container>header').load('common.html header>*', function () {
        if($('body').attr('id')==='pb_studyPlan'){
            $('header>h1').text('学习进度执行图表')
        }
        Public.setHeaderTime(); // 页面顶部时间
    });
    // 加载设置面板
    $('body>aside').load('common.html aside >*', function () {
        $("#getWeatherPeriod").val(settings.getWeatherPeriod || 5);
        $("#chartRefreshPeriod").val(settings.chartRefreshPeriod || 10);
        $("#notebookOptim").attr('checked', [undefined, true].includes(settings.notebookOptim));
        $("#designW").val(settings.designW || 1920);
        $("#designH").val(settings.designH || 1080);
        $("#" + Cfg.zoomMode).prop('checked', true);
        let $colors = $("body>aside .colors");
        Object.keys(Cfg.colorData).forEach(item => {
            $colors.append(`
            <label for="colors_${item}">
                <input type="radio" id="colors_${item}" name="colors" ${Cfg.colors === item ? 'checked' : ''}><span>${item}</span>
            </label>
        `)
        });
    });

    // 保存设置
    $("body ").on('click', '#saveSetting', function () {
        let settings = {
            getWeatherPeriod: $("#getWeatherPeriod").val(),
            chartRefreshPeriod: $("#chartRefreshPeriod").val(),
            notebookOptim: $("#notebookOptim").is(":checked"),
            designW: $("#designW").val(),
            designH: $("#designH").val(),
            colors: $("body>aside input[type=radio][name=colors]:checked").next().text(),
            zoomMode: $("body>aside input[type=radio][name=zoomMode]:checked").next().text(),
        };
        localStorage.setItem('settings', JSON.stringify(settings));
        window.location.reload();
    });

    const sessionData = JSON.parse(sessionStorage.getItem('sessionData'));
    // body的id以“pb_”开头的将作为屏保，无需alert
    if (!(sessionData && sessionData.settingTip) && !$('body').attr('id').startsWith('pb_')) {
        alert('请把鼠标移动到屏幕左侧边靠下的位置，可以滑出设置面板。' +
            '\n如果浏览器已经解除最小字号限制，请在设置面板中取消“低分辨率优化”的勾选。');
        sessionStorage.setItem('sessionData', JSON.stringify({settingTip: true}))
    }

});

```

#### index.js
```js
let Index = {
    init() {
        this.charts = {};
        this.loadData();
        Public.chartsResize(this.charts);
        Public.chartsReDraw(this.charts, null, [
            'ec01_line_tiobe', 'ec06_pie_findSong'
        ], [
            'ec03_barV_timeDistribute', 'ec05_lineBar_timeDistribute', 'ec06_pie_findSong'
        ])
    },
    loadData() {
        this.ec01_line_tiobe();//
        this.ec02_area_accessSource();//
        this.ec03_barV_timeDistribute();//
        this.ec04_pie_computerBroken();//
        this.ec05_lineBar_timeDistribute();//
        this.ec06_pie_findSong();//
    },
    ec01_line_tiobe() {
        let chart = echarts.init($("#ec01_line_tiobe")[0]); //初始化图表，注意命名的规范合理
        this.charts.ec01_line_tiobe = chart; //放入charts对象方便后面的刷新缩放以及其他操作
        chart.setOption(opt_line); // 设置这个类型（折线图）图表的共性
        chart.setOption({
            xAxis: { // 本图表option的个性
                nameLocation: 'start',
                inverse: true,
                data: ['2019', '2014', '2009', '2004', '1999', '1994', '1989']
            },
            yAxis: { // 本图表option的个性
                name: '排名',
                nameLocation: 'start',
                min: 1,
                inverse: true
            },
            dataZoom: { // 本图表option的个性
                type: 'inside',
                orient: 'vertical'
            },
            series: [
                {"name": "Java", data: [1, 2, 1, 1, 12, '-', 0]},
                {"name": "C", data: [2, 1, 2, 2, 1, 1, 1]},
                {"name": "C++", data: [3, 4, 3, 3, 2, 2, 3]},
                {"name": "Python", data: [4, 7, 5, 9, 27, 21, 0]},
                {"name": "Visual Basic .NET", data: [5, 10, '-', '-', '-', '-', 0]},
                {"name": "C#", data: [6, 5, 6, 7, 23, '-', 0]},
                {"name": "JavaScript", data: [7, 8, 8, 8, 17, '-', 0]},
                {"name": "PHP", data: [8, 6, 4, 5, '-', '-', 0]},
                {"name": "SQL", data: [9, '-', '-', 6, '-', '-', 0]},
                {"name": "Objective-C", data: [10, 3, 36, 44, '-', '-', 0]},
                // {"name": "COBOL", data: [25, 20, 16, 11, 3, 9, 12]},
                // {"name": "Lisp", data: [29, 13, 19, 14, 14, 5, 2]},
                // {"name": "Pascal", data: [207, 14, 14, 96, 6, 3, 17]}
            ].map(item => {
                return $.extend(true, {}, seri_line,// 折线图图表series的共性
                    { // 本图表series的个性
                        symbol:'circle',
                        smooth: false,
                        showSymbol: false,
                    }, item)
            })
        })
    },
    ec02_area_accessSource() {
        let chart = echarts.init($("#ec02_area_accessSource")[0]);
        this.charts.ec02_area_accessSource = chart;
        chart.setOption(opt_line);
        chart.setOption({
            xAxis: {
                data: ['周日', '周一', '周二', '周三', '周四', '周五', '周六']
            },
            yAxis: {
                name: '数量/次',
            },
            series: [{
                name: '邮件营销',
                data: [120, 132, 101, 134, 90, 230, 210]
            }, {
                name: '联盟广告',
                data: [220, 182, 191, 234, 290, 330, 310]
            }, {
                name: '视频广告',
                data: [550, 432, 501, 454, 390, 530, 410]
            }, {
                name: '直接访问',
                data: [420, 432, 401, 434, 490, 530, 320]
            }, {
                name: '搜索引擎',
                data: [820, 932, 901, 934, 1290, 1330, 1320]
            }].map(item => {
                return $.extend(true, {}, seri_area, {
                    symbol: 'circle',
                }, item)
            })
        });
    },
    ec03_barV_timeDistribute() {
        let chart = echarts.init($("#ec03_barV_timeDistribute")[0]);
        this.charts.ec03_barV_timeDistribute = chart;
        chart.setOption(opt_bar_v);
        chart.setOption({
            xAxis: {
                data: ['周日', '周一', '周二', '周三', '周四', '周五', '周六']
            },
            yAxis: {
                name: '时间/小时',
            },
            series: [
                {"name": "吃饭", data: [3, 2, 2, 2, 2, 2, 3]},
                {"name": "睡觉", data: [8, 7, 7, 7, 7, 7, 7.5]},
                {"name": "工作", data: [0, 8, 8, 8, 8, 7.5, 8]},
                {"name": "学习", data: [3, 1, 1, 1.5, 1, 1, 2]},
                {"name": "其他", data: [10, 6, 6, 5.5, 6, 6.5, 3.5]},
            ].map(item => {
                return $.extend(true, {}, seri_bar_v, item, {stack: '总时间'})
            })
        })
    },
    ec04_pie_computerBroken() {
        let chart = echarts.init($("#ec04_pie_computerBroken")[0]);
        this.charts.ec04_pie_computerBroken = chart;
        chart.setOption(opt_pie);
        chart.setOption({
            roseType: 'radius',
            series: [
                {
                    name: "电脑坏了",
                    data: [{
                        value: 72,
                        name: '重启'
                    },{
                        value: 3,
                        name: '找人帮忙'
                    }, {
                        value: 10,
                        name: '放弃使用'
                    }, {
                        value: 15,
                        name: '想法修复'
                    } ]
                },
            ].map(item => {
                return $.extend(true, {}, seri_circle, item)
            })
        })
    },
    ec05_lineBar_timeDistribute() {
        let chart = echarts.init($("#ec05_lineBar_timeDistribute")[0]);
        this.charts.ec05_lineBar_timeDistribute = chart;
        chart.setOption(opt_line);
        chart.setOption({
            legend: {
                data: ["吃饭", "学习", "工作", "其他", '睡觉',]
            },
            tooltip: {
                formatter: function (param) {
                    return param.map(item => {
                        if (item.seriesName === '补位') {
                            return ''
                        } else {
                            return `${item.seriesName}: ${item.value}<br>`
                        }
                    }).join("").replace(',', '')

                }
            },
            xAxis: {
                boundaryGap: true,
                data: ['周日', '周一', '周二', '周三', '周四', '周五', '周六']
            },
            yAxis: {
                name: '时间/小时',
            },
            series: [
                {
                    name: '睡觉',
                    data: [8, 7, 7, 7, 6, 6.5, 7.5]
                }, {
                    name: '补位',
                    silent: true,
                    itemStyle: {
                        color: c_bg_bar,
                    },
                    barGap: '-100%',
                    data: new Array(7).fill(12)
                }
            ].map(item => {
                return $.extend(true, {}, seri_bar_v, item)
            }).concat([
                {"name": "吃饭", data: [3, 2, 2, 2, 2, 2, 3]},
                {"name": "学习", data: [3, 1, 1, 1.5, 1, 1, 2]},
                {"name": "工作", data: [0, 8, 8, 8, 8, 7.5, 8]},
                {"name": "其他", data: [10, 6, 6, 5.5, 7, 7, 3.5]},
            ].map(item => {
                return $.extend(true, {}, seri_line, {
                    symbol: 'emptyCircle'
                }, item)
            }))
        })
    },
    ec06_pie_findSong() {
        let chart = echarts.init($("#ec06_pie_findSong")[0]);
        this.charts.ec06_pie_findSong = chart;
        chart.setOption(opt_pie);
        chart.setOption({
            roseType: 'radius',
            visualMap: {
                show: false,
                min: 0,
                max: 100,
                inRange: {
                    colorLightness: [0.3, 1.2]
                }
            },

            series: [
                {
                    name: "视频网站找歌的结果",
                    itemStyle: {
                        normal: {
                            color: colors[0],
                            shadowBlur: 100 * scale,
                            shadowColor: 'rgba(0, 0, 0, 0.5)'
                        }
                    },
                    data: [{
                        value: 40,
                        name: '手机拍的现场版'
                    }, {
                        value: 30,
                        name: '翻唱'
                    }, {
                        value: 18,
                        name: '尤克里里的演奏'
                    }, {
                        value: 10,
                        name: '该视频已被删除'
                    }, {
                        value: 2,
                        name: '找到了'
                    }].sort(function (a, b) {
                        return a.value - b.value;
                    }),
                },
            ].map(item => {
                return $.extend(true, {}, seri_pie, item)
            })
        })
    }
};
Index.init();
```