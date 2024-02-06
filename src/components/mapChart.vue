<template>
    <div>
        <div id="app">
            <el-button size="mini" type="primary" @click="backMap()" class="btn">返回全国</el-button>
            <div id="container">
                <div id="left">
                    <span>COLOR PANEL</span>
                    <div class="sp-container sp-light sp-palette-only fillpicker-container"
                        style="position: absolute; min-height: 550.562px; top: 237.922px; left: 402.891px;">
                        <div class="sp-palette-container">
                            <div class="sp-cf sp-palette-row sp-palette-row-0">
                                <span title="#f7fcfd" data-color="rgb(247, 252, 253)" class="sp-thumb-el sp-thumb-light">
                                    <span class="sp-thumb-inner" style="background-color:rgb(247, 252, 253);" @click="changeColor(247, 252, 253)"></span>
                                </span>
                                <span title="#e5f5f9" data-color="rgb(229, 245, 249)" class="sp-thumb-el sp-thumb-light">
                                    <span class="sp-thumb-inner" style="background-color:rgb(229, 245, 249);" @click="changeColor(229, 245, 249)"></span>
                                </span>
                                <span title="#ccece6" data-color="rgb(204, 236, 230)" class="sp-thumb-el sp-thumb-light">
                                    <span class="sp-thumb-inner" style="background-color:rgb(204, 236, 230);" @click="changeColor(204, 236, 230)"></span>
                                </span>
                                <span title="#99d8c9" data-color="rgb(153, 216, 201)" class="sp-thumb-el sp-thumb-light">
                                    <span class="sp-thumb-inner" style="background-color:rgb(153, 216, 201);" @click="changeColor(153, 216, 201)"></span>
                                </span>
                                <span title="#66c2a4" data-color="rgb(102, 194, 164)" class="sp-thumb-el sp-thumb-light">
                                    <span class="sp-thumb-inner" style="background-color:rgb(102, 194, 164);" @click="changeColor(102, 194, 164)"></span>
                                </span>
                                <span title="#41ae76" data-color="rgb(65, 174, 118)" class="sp-thumb-el sp-thumb-dark">
                                    <span class="sp-thumb-inner" style="background-color:rgb(65, 174, 118);" @click="changeColor(65, 174, 118)"></span>
                                </span>
                                <span title="#238b45" data-color="rgb(35, 139, 69)" class="sp-thumb-el sp-thumb-dark">
                                    <span class="sp-thumb-inner" style="background-color:rgb(35, 139, 69);" @click="changeColor(35, 139, 69)"></span>
                                </span>
                                <span title="#006d2c" data-color="rgb(0, 109, 44)" class="sp-thumb-el sp-thumb-dark">
                                    <span class="sp-thumb-inner" style="background-color:rgb(0, 109, 44);" @click="changeColor(0, 109, 44)"></span>
                                </span>
                                <span title="#00441b" data-color="rgb(0, 68, 27)" class="sp-thumb-el sp-thumb-dark">
                                    <span class="sp-thumb-inner" style="background-color:rgb(0, 68, 27);" @click="changeColor(0, 68, 27)"></span>
                                </span>
                            </div>
                        </div>
                    </div>
                    <div id="selectedColor"></div>
                </div>
                <div id="right"></div>
            </div>
        </div>
    </div>
</template>

<script>

// let echarts = require("echarts/lib/echarts")
import * as echarts from 'echarts/lib/echarts.js'
import $ from "jquery"
// import echarts from "echarts"
require("echarts/lib/chart/map")
require("echarts-map/js/china")

export default {
    name: "mapChart",
    data() {
        return {}
    },
    mounted() {

        // let colors = [
        //     ['rgb(247, 252, 253)', 'rgb(229, 245, 249)', 'rgb(204, 236, 230)', 'rgb(153, 216, 201)', 'rgb(102, 194, 164)', 'rgb(65, 174, 118)', 'rgb(35, 139, 69)', 'rgb(0, 109, 44)', 'rgb(0, 68, 27)']
        // ]
        // let a = $('.sp-palette-container')
        // // console.log(a)
        // for (let i = 0; i < colors.length; i++) {
        //     let t = $("<div>", { class: "sp-cf sp-palette-row sp-palette-row-" + i })
        //     a.append(t)
        //     for (let j = 0; j < colors[i].length; j++) {
        //         let b = $("<span title=\"#f7fcfd\" data-color=\"rgb(0, 68, 27)\" class=\"sp-thumb-el sp-thumb-light\"><span class=\"sp-thumb-inner\" style=\"background-color:rgb(0, 68, 27);\"></span></span>")
        //         t.append(b)
        //     }
        // }
        this.mapChart()

        // const colors = ['#FF5733', '#33FF57', '#5733FF', '#33A4FF', '#FF33D1']; // Add your desired colors

        // // Create color panel
        // const colorPanel = document.getElementById('left');
        // colors.forEach(color => {
        //   const colorBox = document.createElement('div');
        //   colorBox.classList.add('color-box');
        //   colorBox.style.backgroundColor = color;
        //   colorBox.addEventListener('click', () => selectColor(color));
        //   colorPanel.appendChild(colorBox);
        //   console.log(colorBox)
        // });

        // // Function to select a color
        // function selectColor(color) {
        //   const selectedColor = document.getElementById('selectedColor');
        //   selectedColor.textContent = `Selected Color: ${color}`;
        // }

    },
    methods: {
        changeColor(r, g, b){
            this.color = "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)
        },
        backMap() {
            this.$options.methods.mapChart()
        },
        mapChart() {
            let myChart = echarts.init(document.getElementById("right"))

            window.addEventListener("resize", () => {
                myChart.resize()
            })

            initEcharts("china")
            function initEcharts(map) {
                let option = {
                    geo: {
                        map: map,
                        roam: false,
                        scaleLimit: {
                            min: 1.2,
                            max: 3,
                        },
                        zoom: 1.2,
                        //图形上的文本标签，可用于说明图形的一些数据信息
                        label: {
                            normal: {
                                show: true,
                                fontSize: "16",
                                color: "rgba(0,0,0,0.7)",
                            },
                        },
                        //地图区域的多边形 图形样式，有 normal 和 emphasis 两个状态
                        itemStyle: {
                            //normal 是图形在默认状态下的样式；
                            normal: {
                                // borderColor: "rgba(0, 0, 0, 0.2)",
                                borderColor: "#000000",
                                areaColor: "#D1DBDD",
                                borderWidth: 1
                            },
                            //emphasis 是图形在高亮状态下的样式，比如在鼠标悬浮或者图例联动高亮时。
                            // emphasis: {
                            //   areaColor: "#F3B329",
                            //   shadowOffsetX: 0,
                            //   shadowOffsetY: 0,
                            //   shadowBlur: 20,
                            //   borderWidth: 0,
                            //   shadowColor: "rgba(0, 0, 0, 0.5)",
                            // },
                            // emphasis: {
                            //   areaColor: "#EEEEEE"
                            // }
                        },
                        emphasis: {
                            disabled: true
                        }
                    },
                    series: [
                        {
                            name: "信息量",
                            type: "map",
                            //这里是'china',及因为js中注册的名字，如果是上海市，则该出需pName 指的是'shanghai'
                            selectedMode: 'none',
                            animation: false,
                            mapType: map,
                            label: {
                                show: false
                            },
                            geoIndex: 0,
                            regions: []
                        },
                    ],
                }
                myChart.setOption(option)
            }

            function mergeGeo(dat1, dat2) {
                let dat = { "UTF8Encoding": false }
                dat.features = dat1.features.concat(dat2["features"])
                dat.type = "FeatureCollection"
                return dat
            }

            //定义全国省份的数组
            var provinces = {
                // 23个省
                台湾: "taiwan",
                河北: "hebei",
                山西: "shanxi",
                辽宁: "liaoning",
                吉林: "jilin",
                黑龙江: "heilongjiang",
                江苏: "jiangsu",
                浙江: "zhejiang",
                安徽: "anhui",
                福建: "fujian",
                江西: "jiangxi",
                山东: "shandong",
                河南: "henan",
                湖北: "hubei",
                湖南: "hunan",
                广东: "guangdong",
                海南: "hainan",
                四川: "sichuan",
                贵州: "guizhou",
                云南: "yunnan",
                陕西: "shanxi1",
                甘肃: "gansu",
                青海: "qinghai",
                // 5个自治区
                新疆: "xinjiang",
                广西: "guangxi",
                内蒙古: "neimenggu",
                宁夏: "ningxia",
                西藏: "xizang",
                // 4个直辖市
                北京: "beijing",
                天津: "tianjin",
                上海: "shanghai",
                重庆: "chongqing",
                // 2个特别行政区
                香港: "xianggang",
                澳门: "aomen",
            }

            // 市
            var cityMap = {
                北京市: "110100",
                天津市: "120100",
                上海市: "310100",
                重庆市: "500100",
                崇明县: "310200",
                湖北省直辖县市: "429000",
                铜仁市: "522200",
                毕节市: "522400",
                石家庄市: "130100",
                唐山市: "130200",
                秦皇岛市: "130300",
                邯郸市: "130400",
                邢台市: "130500",
                保定市: "130600",
                张家口市: "130700",
                承德市: "130800",
                沧州市: "130900",
                廊坊市: "131000",
                衡水市: "131100",
                太原市: "140100",
                大同市: "140200",
                阳泉市: "140300",
                长治市: "140400",
                晋城市: "140500",
                朔州市: "140600",
                晋中市: "140700",
                运城市: "140800",
                忻州市: "140900",
                临汾市: "141000",
                吕梁市: "141100",
                呼和浩特市: "150100",
                包头市: "150200",
                乌海市: "150300",
                赤峰市: "150400",
                通辽市: "150500",
                鄂尔多斯市: "150600",
                呼伦贝尔市: "150700",
                巴彦淖尔市: "150800",
                乌兰察布市: "150900",
                兴安盟: "152200",
                锡林郭勒盟: "152500",
                阿拉善盟: "152900",
                沈阳市: "210100",
                大连市: "210200",
                鞍山市: "210300",
                抚顺市: "210400",
                本溪市: "210500",
                丹东市: "210600",
                锦州市: "210700",
                营口市: "210800",
                阜新市: "210900",
                辽阳市: "211000",
                盘锦市: "211100",
                铁岭市: "211200",
                朝阳市: "211300",
                葫芦岛市: "211400",
                长春市: "220100",
                吉林市: "220200",
                四平市: "220300",
                辽源市: "220400",
                通化市: "220500",
                白山市: "220600",
                松原市: "220700",
                白城市: "220800",
                延边朝鲜族自治州: "222400",
                哈尔滨市: "230100",
                齐齐哈尔市: "230200",
                鸡西市: "230300",
                鹤岗市: "230400",
                双鸭山市: "230500",
                大庆市: "230600",
                伊春市: "230700",
                佳木斯市: "230800",
                七台河市: "230900",
                牡丹江市: "231000",
                黑河市: "231100",
                绥化市: "231200",
                大兴安岭地区: "232700",
                南京市: "320100",
                无锡市: "320200",
                徐州市: "320300",
                常州市: "320400",
                苏州市: "320500",
                南通市: "320600",
                连云港市: "320700",
                淮安市: "320800",
                盐城市: "320900",
                扬州市: "321000",
                镇江市: "321100",
                泰州市: "321200",
                宿迁市: "321300",
                杭州市: "330100",
                宁波市: "330200",
                温州市: "330300",
                嘉兴市: "330400",
                湖州市: "330500",
                绍兴市: "330600",
                金华市: "330700",
                衢州市: "330800",
                舟山市: "330900",
                台州市: "331000",
                丽水市: "331100",
                合肥市: "340100",
                芜湖市: "340200",
                蚌埠市: "340300",
                淮南市: "340400",
                马鞍山市: "340500",
                淮北市: "340600",
                铜陵市: "340700",
                安庆市: "340800",
                黄山市: "341000",
                滁州市: "341100",
                阜阳市: "341200",
                宿州市: "341300",
                六安市: "341500",
                亳州市: "341600",
                池州市: "341700",
                宣城市: "341800",
                福州市: "350100",
                厦门市: "350200",
                莆田市: "350300",
                三明市: "350400",
                泉州市: "350500",
                漳州市: "350600",
                南平市: "350700",
                龙岩市: "350800",
                宁德市: "350900",
                南昌市: "360100",
                景德镇市: "360200",
                萍乡市: "360300",
                九江市: "360400",
                新余市: "360500",
                鹰潭市: "360600",
                赣州市: "360700",
                吉安市: "360800",
                宜春市: "360900",
                抚州市: "361000",
                上饶市: "361100",
                济南市: "370100",
                青岛市: "370200",
                淄博市: "370300",
                枣庄市: "370400",
                东营市: "370500",
                烟台市: "370600",
                潍坊市: "370700",
                济宁市: "370800",
                泰安市: "370900",
                威海市: "371000",
                日照市: "371100",
                莱芜市: "371200",
                临沂市: "371300",
                德州市: "371400",
                聊城市: "371500",
                滨州市: "371600",
                菏泽市: "371700",
                郑州市: "410100",
                开封市: "410200",
                洛阳市: "410300",
                平顶山市: "410400",
                安阳市: "410500",
                鹤壁市: "410600",
                新乡市: "410700",
                焦作市: "410800",
                濮阳市: "410900",
                许昌市: "411000",
                漯河市: "411100",
                三门峡市: "411200",
                南阳市: "411300",
                商丘市: "411400",
                信阳市: "411500",
                周口市: "411600",
                驻马店市: "411700",
                省直辖县级行政区划: "469000",
                武汉市: "420100",
                黄石市: "420200",
                十堰市: "420300",
                宜昌市: "420500",
                襄阳市: "420600",
                鄂州市: "420700",
                荆门市: "420800",
                孝感市: "420900",
                荆州市: "421000",
                黄冈市: "421100",
                咸宁市: "421200",
                随州市: "421300",
                恩施土家族苗族自治州: "422800",
                长沙市: "430100",
                株洲市: "430200",
                湘潭市: "430300",
                衡阳市: "430400",
                邵阳市: "430500",
                岳阳市: "430600",
                常德市: "430700",
                张家界市: "430800",
                益阳市: "430900",
                郴州市: "431000",
                永州市: "431100",
                怀化市: "431200",
                娄底市: "431300",
                湘西土家族苗族自治州: "433100",
                广州市: "440100",
                韶关市: "440200",
                深圳市: "440300",
                珠海市: "440400",
                汕头市: "440500",
                佛山市: "440600",
                江门市: "440700",
                湛江市: "440800",
                茂名市: "440900",
                肇庆市: "441200",
                惠州市: "441300",
                梅州市: "441400",
                汕尾市: "441500",
                河源市: "441600",
                阳江市: "441700",
                清远市: "441800",
                东莞市: "441900",
                中山市: "442000",
                潮州市: "445100",
                揭阳市: "445200",
                云浮市: "445300",
                南宁市: "450100",
                柳州市: "450200",
                桂林市: "450300",
                梧州市: "450400",
                北海市: "450500",
                防城港市: "450600",
                钦州市: "450700",
                贵港市: "450800",
                玉林市: "450900",
                百色市: "451000",
                贺州市: "451100",
                河池市: "451200",
                来宾市: "451300",
                崇左市: "451400",
                海口市: "460100",
                三亚市: "460200",
                三沙市: "460300",
                成都市: "510100",
                自贡市: "510300",
                攀枝花市: "510400",
                泸州市: "510500",
                德阳市: "510600",
                绵阳市: "510700",
                广元市: "510800",
                遂宁市: "510900",
                内江市: "511000",
                乐山市: "511100",
                南充市: "511300",
                眉山市: "511400",
                宜宾市: "511500",
                广安市: "511600",
                达州市: "511700",
                雅安市: "511800",
                巴中市: "511900",
                资阳市: "512000",
                阿坝藏族羌族自治州: "513200",
                甘孜藏族自治州: "513300",
                凉山彝族自治州: "513400",
                贵阳市: "520100",
                六盘水市: "520200",
                遵义市: "520300",
                安顺市: "520400",
                黔西南布依族苗族自治州: "522300",
                黔东南苗族侗族自治州: "522600",
                黔南布依族苗族自治州: "522700",
                昆明市: "530100",
                曲靖市: "530300",
                玉溪市: "530400",
                保山市: "530500",
                昭通市: "530600",
                丽江市: "530700",
                普洱市: "530800",
                临沧市: "530900",
                楚雄彝族自治州: "532300",
                红河哈尼族彝族自治州: "532500",
                文山壮族苗族自治州: "532600",
                西双版纳傣族自治州: "532800",
                大理白族自治州: "532900",
                德宏傣族景颇族自治州: "533100",
                怒江傈僳族自治州: "533300",
                迪庆藏族自治州: "533400",
                拉萨市: "540100",
                昌都地区: "542100",
                山南地区: "542200",
                日喀则地区: "542300",
                那曲地区: "542400",
                阿里地区: "542500",
                林芝地区: "542600",
                西安市: "610100",
                铜川市: "610200",
                宝鸡市: "610300",
                咸阳市: "610400",
                渭南市: "610500",
                延安市: "610600",
                汉中市: "610700",
                榆林市: "610800",
                安康市: "610900",
                商洛市: "611000",
                兰州市: "620100",
                嘉峪关市: "620200",
                金昌市: "620300",
                白银市: "620400",
                天水市: "620500",
                武威市: "620600",
                张掖市: "620700",
                平凉市: "620800",
                酒泉市: "620900",
                庆阳市: "621000",
                定西市: "621100",
                陇南市: "621200",
                临夏回族自治州: "622900",
                甘南藏族自治州: "623000",
                西宁市: "630100",
                海东地区: "632100",
                海北藏族自治州: "632200",
                黄南藏族自治州: "632300",
                海南藏族自治州: "632500",
                果洛藏族自治州: "632600",
                玉树藏族自治州: "632700",
                海西蒙古族藏族自治州: "632800",
                银川市: "640100",
                石嘴山市: "640200",
                吴忠市: "640300",
                固原市: "640400",
                中卫市: "640500",
                乌鲁木齐市: "650100",
                克拉玛依市: "650200",
                吐鲁番地区: "652100",
                哈密地区: "652200",
                昌吉回族自治州: "652300",
                博尔塔拉蒙古自治州: "652700",
                巴音郭楞蒙古自治州: "652800",
                阿克苏地区: "652900",
                克孜勒苏柯尔克孜自治州: "653000",
                喀什地区: "653100",
                和田地区: "653200",
                伊犁哈萨克自治州: "654000",
                塔城地区: "654200",
                阿勒泰地区: "654300",
                自治区直辖县级行政区划: "659000",
                台湾省: "710000",
                香港特别行政区: "810100",
                澳门特别行政区: "820000",
            }

            // var that = this

            // 点击触发
            myChart.on("click", param => {
                if (param.name in provinces) {
                    // 处理省模块
                    let names = param.name
                    for (let key in provinces) {
                        if (names == key) {
                            showProvince(provinces[key], key)
                            break
                        }
                    }
                } else if (param.name in cityMap) {
                    // 处理市模块
                    let names = param.name
                    for (let key in cityMap) {
                        if (names == key) {
                            showCitys(cityMap[key], key)
                            break
                        }
                    }
                } else {
                    let option = myChart.getOption()
                    console.log(option)
                    option.geo[0].regions.push(
                        {
                            name: param.name,
                            itemStyle: {
                                color: this.color,
                                areaColor: this.color
                            }
                        }
                    )
                    myChart.setOption(option)
                }
            })
            myChart.on("contextmenu", param => {
                param.event.stop()
                if (!(param.name in provinces) & !(param.name in cityMap)) {
                    let option = myChart.getOption()
                    console.log(option)
                    option.geo[0].regions.push(
                        {
                            name: param.name,
                            itemStyle: {
                                color: '#D1DBDD',
                                areaColor: '#D1DBDD'
                            }
                        }
                    )
                    myChart.setOption(option)
                }
            })

            //展示对应的省
            function showProvince(eName, param) {
                $.getJSON(`/map/province/${eName}.json`, data => {
                    var data_prov = { "features": [] }

                    for (let c in data.features) {
                        $.ajax({
                            url: `/map/city/${data.features[c].id}.json`,
                            dataType: 'json',
                            async: false,
                            success: function (data2) {
                                data_prov = mergeGeo(data_prov, data2);
                            }
                        });
                    }
                    echarts.registerMap(param, data_prov)
                    initEcharts(param)
                })
            }

            //展示对应市
            function showCitys(cName, param) {
                console.log(cName, param)
                // 显示县级地图
                $.getJSON(`/map/city/${cName}.json`, data => {
                    echarts.registerMap(param, data)
                    // alert("县")
                    initEcharts(param)
                })
            }
        },
    },
}
</script>

<style scoped>
/* #app {
  text-align: center;
  margin: 20px;
} */

#container {
    width: 1600px;
    height: 900px;
    margin: 0px auto 0;
    display: flex;
}

#left {
    width: 40%;
}

#right {
    width: 60%;
}

.btn {
    position: absolute;
    right: 10%;
    z-index: 999;
}

.sp-container * {
    box-sizing: content-box;
}

.sp-thumb-el {
    display: block;
    position: relative;
    float: left;
    cursor: pointer;
    width: 14px;
    height: 14px;
    margin: 2px;
    border: 1px solid #d0d0d0;
    /* background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAwAAAAMCAIAAADZF8uwAAAAGUlEQVQYV2M4gwH+YwCGIasIUwhT25BVBADtzYNYrHvv4gAAAABJRU5ErkJggg==); */
}

.sp-alpha-inner,
.sp-preview-inner,
.sp-thumb-inner {
    display: block;
    position: absolute;
    top: -1px;
    left: -1px;
    bottom: -1px;
    right: -1px;
    border: 1px solid var(--border-color);
    transition: transform .25s;
    line-height: 14px;
    text-align: center;
    font-weight: 700;
}

.sp-thumb-inner:hover {
    transform: scale(1.2)
}

.sp-palette {
    max-width: 220px;
    border-top: 1px solid var(--border-color);
    padding-top: 10px;
}

.color-box {
    width: 14px;
    height: 14px;
    cursor: pointer;
}
</style>