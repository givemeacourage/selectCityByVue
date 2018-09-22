<template>
  <div class="conatainer">
    <div>
        <input type="radio" name="dancheng" id="dangcheng" v-model="select" value="单程"><span>单程</span>
        <input type="radio" name="fangcheng" id="fangcheng" v-model="select" value="返程"><span>返程</span>
    </div>
      <div>
          <span>出发城市：</span><input type="text" placeholder="城市名" v-model="cityName" class="cityName"  @focus = "showAllCity" @keyup="inputHandle" @blur="blurHandle">
          <!--<span>出发日期：</span><input type="text" placeholder="yyyy-mm-dd">-->
          <!--<span>到达城市：</span><input type="text" placeholder="城市名">-->
          <!--<span>返程日期：</span><input type="text" placeholder="yyyy-mm-dd">-->
          <div class="dataShow" v-show="isTrue">
              <ul v-for="value in filterData" >
                  <li @click="selValue(value)" class="itemLi">{{value}}</li>
              </ul>
              <ul v-for="value in findData" >
                  <li class="itemLi" style="color:red;">{{value}}</li>
              </ul>
          </div>
      </div>
      <div class="hotCity" v-if="isShow">
          <p>热门城市/国家(支持汉字/拼音/英文字母)</p>
          <ul class="tab_item">
              <li @click="changeCity(0)" :class="{onStyle: style1}">热门城市</li>
              <li @click="changeCity(1)" :class="{onStyle: style2}">ABCDE</li>
              <li @click="changeCity(2)" :class="{onStyle: style3}">FGHJ</li>
              <li @click="changeCity(3)" :class="{onStyle: style4}">KLMNP</li>
              <li @click="changeCity(4)" :class="{onStyle: style5}">QRSTW</li>
              <li @click="changeCity(5)" :class="{onStyle: style6}">XYZ</li>
          </ul>
          <div class="content_item" v-show="hotCity">
              <dl>
                  <dt></dt>
                  <dd @click="selectCity(0)">北京</dd>
                  <dd @click="selectCity(1)">重庆</dd>
                  <dd @click="selectCity(2)">武汉</dd>
                  <dd @click="selectCity(3)">青岛</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd @click="selectCity(4)">上海</dd>
                  <dd @click="selectCity(5)">厦门</dd>
                  <dd @click="selectCity(6)">长沙</dd>
                  <dd @click="selectCity(7)">天津</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd @click="selectCity(8)">广州</dd>
                  <dd @click="selectCity(9)">昆明</dd>
                  <dd @click="selectCity(10)">南京</dd>
                  <dd @click="selectCity(11)">三亚</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd @click="selectCity(12)">深圳</dd>
                  <dd @click="selectCity(13)">杭州</dd>
                  <dd @click="selectCity(14)">大连</dd>
                  <dd @click="selectCity(15)">海口</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd @click="selectCity(16)">成都</dd>
                  <dd @click="selectCity(17)">西安</dd>
                  <dd @click="selectCity(18)">郑州</dd>
                  <dd @click="selectCity(19)">乌鲁木齐</dd>
              </dl>
          </div>
          <div class="content_item" v-show="AE">
              <dl>
                  <dt>A</dt>
                  <dd>安庆</dd>
                  <dd>阿勒泰</dd>
                  <dd>安康</dd>
                  <dd>阿克苏</dd>
                  <dd>安顺</dd>
              </dl>
              <dl>
                  <dt>B</dt>
                  <dd>包头</dd>
                  <dd>北海</dd>
                  <dd>北京</dd>
                  <dd>百色</dd>
                  <dd>保山</dd>
              </dl>
              <dl>
                  <dt>C</dt>
                  <dd>长治</dd>
                  <dd>长春</dd>
                  <dd>常州</dd>
                  <dd>昌都</dd>
                  <dd>朝阳</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>常德</dd>
                  <dd>长白山</dd>
                  <dd>成都</dd>
                  <dd>重庆</dd>
                  <dd>长沙</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>赤峰</dd>
                  <dd>潮州</dd>
              </dl>
              <dl>
                  <dt>D</dt>
                  <dd>大同</dd>
                  <dd>大连</dd>
                  <dd>达县</dd>
                  <dd>东营</dd>
                  <dd>大庆</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>丹东</dd>
                  <dd>大理</dd>
                  <dd>敦煌</dd>
                  <dd>稻城</dd>
                  <dd>德令哈</dd>
              </dl>
              <dl>
                  <dt>E</dt>
                  <dd>鄂尔多斯</dd>
                  <dd>恩施</dd>
              </dl>
          </div>
          <div class="content_item" v-show="FJ">
              <dl>
                  <dt>F</dt>
                  <dd>福州</dd>
                  <dd>阜阳</dd>
              </dl>
              <dl>
                  <dt>G</dt>
                  <dd>贵阳</dd>
                  <dd>桂林</dd>
                  <dd>广州</dd>
                  <dd>广元</dd>
                  <dd>格尔木</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>固原</dd>
              </dl>
              <dl>
                  <dt>H</dt>
                  <dd>呼和浩特</dd>
                  <dd>哈密</dd>
                  <dd>黑河</dd>
                  <dd>海拉尔</dd>
                  <dd>哈尔滨</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>海口</dd>
                  <dd>黄山</dd>
                  <dd>杭州</dd>
                  <dd>邯郸</dd>
                  <dd>合肥</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>汉中</dd>
                  <dd>和田</dd>
                  <dd>淮安</dd>
                  <dd>河池</dd>
              </dl>
              <dl>
                  <dt>J</dt>
                  <dd>晋江</dd>
                  <dd>九寨沟</dd>
                  <dd>锦州</dd>
                  <dd>景德镇</dd>
                  <dd>嘉峪关</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>井冈山</dd>
                  <dd>济宁</dd>
                  <dd>九江</dd>
                  <dd>佳木斯</dd>
                  <dd>济南</dd>
              </dl>
              <dl>
                  <dt></dt>
                  <dd>揭阳</dd>
              </dl>
          </div>
          <div class="content_item" v-show="KP">
              KLMNP
          </div>
          <div class="content_item" v-show="QW">
              QRSTW
          </div>
          <div class="content_item" v-show="XZ">
              XYZ
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: '',
  data () {
    return {
        select: '单程',
        // 城市变量 用于切换显示城市
        hotCity: true,
        AE: false,
        FJ: false,
        KP: false,
        QW: false,
        XZ: false,
        //所有城市
        allCity: [

            "安庆","阿勒泰","安康","阿克苏","安顺",

            "包头","北海","北京","百色","保山",

            "长治","长春","常州","昌都","朝阳","常德","长白山","成都","重庆","长沙","赤峰","潮州",

            "大同","大连","达县","东营","大庆","丹东","大理","敦煌","稻城","德令哈",

            "鄂尔多斯","恩施",

            "福州","阜阳",

            "贵阳","桂林","广州","广元","格尔木","固原",

            "呼和浩特","哈密","黑河","海拉尔","哈尔滨","海口","黄山","杭州","邯郸","合肥","汉中","和田","淮安","河池",

            "晋江","九寨沟","锦州","景德镇","嘉峪关","井冈山","济宁","九江","佳木斯","济南","揭阳",
            "喀什","昆明","康定","克拉玛依","库尔勒","库车",

            "兰州","洛阳","丽江","拉萨","黎平","连城","连云港","临沧","临汾","临沂","林芝","六盘水","柳州","泸州",

            "牡丹江","芒市","满洲里","绵阳","梅县","漠河",

            "南京","南充","南宁","南阳","南通","那拉提","南昌","宁波",

            "攀枝花",
            "衢州","秦皇岛","庆阳","齐齐哈尔","青岛",

            "深圳","石家庄","三亚","沈阳","上海","思茅","神农架","邵阳",

            "铜仁","塔城","腾冲","台州","泰州","天津","通辽","太原",

            "威海","武汉","梧州","文山","无锡","潍坊","武夷山","乌兰浩特","温州","乌鲁木齐","万州","乌海",

            "兴义","西昌","厦门","西安","襄阳","西宁","锡林浩特","西双版纳","忻州","徐州",

            "义乌","永州","榆林","延安","运城","烟台","银川","宜昌","宜宾","盐城","延吉","玉树","伊宁","扬州",

            "珠海","昭通","张家界","舟山","郑州","中卫","芷江","湛江","遵义新舟","遵义茅台"
        ],

        //
        selfData: ['没有了','skr','找不到了'],
        // 热门城市变量
        cityName: '',
        // 城市面板变量
        isShow: false,
        // 过滤数据显示切换 变量
        isTrue : false,

        // 样式 动画切换
        style1: true,
        style2: false,
        style3: false,
        style4: false,
        style5: false,
        style6: false
    }
  },
  methods:{
      changeCity (index) {
            if (index === 0) {
                this.hotCity = true;
                this.AE = false;
                this.FJ = false;
                this.KP = false;
                this.QW = false;
                this.XZ = false;

                this.style1 = true;
                this.style2 = false;
                this.style3 = false;
                this.style4 = false;
                this.style5 = false;
                this.style6 = false;
            }
            if (index === 1) {
                this.hotCity = false;
                this.AE = true;
                this.FJ = false;
                this.KP = false;
                this.QW = false;
                this.XZ = false;

                this.style1 = false;
                this.style2 = true;
                this.style3 = false;
                this.style4 = false;
                this.style5 = false;
                this.style6 = false;
            }
          if (index === 2) {
              this.hotCity = false;
              this.AE = false;
              this.FJ = true;
              this.KP = false;
              this.QW = false;
              this.XZ = false;

              this.style1 = false;
              this.style2 = false;
              this.style3 = true;
              this.style4 = false;
              this.style5 = false;
              this.style6 = false;
          }
          if (index === 3) {
              this.hotCity = false;
              this.AE = false;
              this.FJ = false;
              this.KP = true;
              this.QW = false;
              this.XZ = false;

              this.style1 = false;
              this.style2 = false;
              this.style3 = false;
              this.style4 = true;
              this.style5 = false;
              this.style6 = false;
          }
          if (index === 4) {
              this.hotCity = false;
              this.AE = false;
              this.FJ = false;
              this.KP = false;
              this.QW = true;
              this.XZ = false;

              this.style1 = false;
              this.style2 = false;
              this.style3 = false;
              this.style4 = false;
              this.style5 = true;
              this.style6 = false;
          }
          if (index === 5) {
              this.hotCity = false;
              this.AE = false;
              this.FJ = false;
              this.KP = false;
              this.QW = false;
              this.XZ = true;

              this.style1 = false;
              this.style2 = false;
              this.style3 = false;
              this.style4 = false;
              this.style5 = false;
              this.style6 = true;
          }

      },
      //选择热门城市逻辑
      selectCity (index) {
          if (index === 0) {
              this.cityName = '北京'
              this.hideData();
          }
          if (index === 1) {
              this.cityName = '重庆';
              this.hideData();
          }
          if (index === 2) {
              this.cityName = '武汉';
              this.hideData();
          }
          if (index === 3) {
              this.cityName = '青岛';
              this.hideData();
          }
          if (index === 4) {
              this.cityName = '上海';
              this.hideData();
          }
          if (index === 5) {
              this.cityName = '厦门';
              this.hideData();
          }
          if (index === 6) {
              this.cityName = '长沙';
              this.hideData();
          }
          if (index === 7) {
              this.cityName = '天津';
              this.hideData();
          }
          if (index === 8) {
              this.cityName = '广州';
              this.hideData();
          }
          if (index === 9) {
              this.cityName = '昆明';
              this.hideData();
          }
          if (index === 10) {
              this.cityName = '南京';
              this.hideData();
          }
          if (index === 11) {
              this.cityName = '三亚';
              this.hideData();
          }
          if (index === 12) {
              this.cityName = '深圳';
              this.hideData();
          }
          if (index === 13) {
              this.cityName = '杭州';
              this.hideData();
          }
          if (index === 14) {
              this.cityName = '大连';
              this.hideData();
          }
          if (index === 15) {
              this.cityName = '海口';
              this.hideData();
          }
          if (index === 16) {
              this.cityName = '成都';
              this.hideData();
          }
          if (index === 17) {
              this.cityName = '西安';
              this.hideData();
          }
          if (index === 18) {
              this.cityName = '郑州';
              this.hideData();
          }
          if (index === 19) {
              this.cityName = '乌鲁木齐';
              this.hideData();
          }

      },
      // 显示所有城市面板  获得Input焦点事件
      showAllCity () {
          this.isShow = true
      },
      // 键盘输入事件
      inputHandle () {
          this.isShow = false; // 当input输入值时，隐藏城市面板
          this.isTrue = true;  // 显示过滤数据列表
          if (this.cityName === '') { // 如果input值为空 ，显示城市面板，隐藏过滤数据列表
              this.isShow = true;
              this.isTrue = false;
          }
          if (this.cityName !== '') {  // 如果input框有值，隐藏城市面板
              this.isShow = false;
          }

      },
      // input失焦事件
      blurHandle () {       // input框失焦之后延迟觖发
          setTimeout(() => {
              this.isTrue = false;
          },200)
      },
      selValue (value) {
          this.cityName = value;
      },
      // 定义函数 隐藏城市面板， 隐藏数据面板
      hideData () {
          this.isShow = false;
          this.isTrue = false;
      }
  },
    computed:{
      filterData () {  // 根据input值过滤数据
          if (this.cityName) {
             return this.allCity.filter((value)=>{  // 如果包含返回true
                return value.includes(this.cityName)
              })
          }
      },
        findData () {  // 找不到值默认显示
            if (this.cityName && this.allCity.indexOf(this.cityName) === -1) {
                return this.selfData;
            }
        }
    },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;

}
a {
  color: #42b983;
}
dl{
   display: inline-block;
}
dd:hover{
   cursor: pointer;
    background-color: pink;
}

.hotCity {
    width: 780px;
    border:1px solid #000;

    margin:0 auto;
}
.hotCity .tab_item {
    margin: 0;
}
.hotCity .tab_item li {
    color: blue;
    margin: 0 5px;
}
.hotCity .tab_item li:hover {
    cursor: pointer;
    color: red;
}
.hotCity .content_item {
    border-top: 1px solid gainsboro;

}

.dataShow{
    width: 200px;
    border: 1px solid #000;
    margin: 0 auto;

}
.itemLi:hover {
    width: 100%;
    cursor: pointer;
    background-color: deepskyblue;
}
.onStyle {
    border: 1px solid gainsboro;
    border-bottom: 1px solid #fff !important;


}
</style>
