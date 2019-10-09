<template>
<div>
<Header />
  <div class="container">
    <ul class="breadcrumb">
      <li class="breadcrumb-item">
        <a href="javascript:;">蛋壳公寓</a>
      </li>
      <li class="breadcrumb-item">
        <a href="javascript:;">北京租房</a>
      </li>
    </ul>
    <div id="ss">
      <div class="ss-search">
        <input type="text" placeholder="请输入区域、地铁、小区名" class="ss-input">
        <button class="ss-btn">搜索</button>
        <button class="ss-a">地图找房</button>
      </div>
      <div class="ss-list">
        <a href="javascript:;">现房</a>
        <a href="javascript:;">一居室</a>
        <a href="javascript:;">回龙观</a>
        <a href="javascript:;">双井</a>
        <a href="javascript:;">天通苑</a>
        <a href="javascript:;">青年路</a>
        <a href="javascript:;">望京</a>
        <a href="javascript:;">所有房源</a>
      </div>
      <div class="filter-options">
        <ul>
          <li>位置:</li>
          <li><a href="javascript">不限</a></li>
          <li v-for="(item,i) of lists" :key='i'>
            <a href="javascript" @mouseover="show" @mouseout="hide" v-text='item.uname'></a>
            <div class="sub-option-list"   @mouseover="show2" @mouseout="hide2" >
              <a href="javascript:;" v-for="(child,i) of item.children" :key='i' v-text='child'></a>
            </div>
          </li>
        </ul>
        <ul>
          <li>价格:</li>
          <li>不限</li>
          <li>1500元以下</li>
          <li>1500~2000元</li>
          <li>2000~2500元</li>
          <li>2500~3000元</li>
          <li>3000元以上</li>
        </ul>
        <ul>
          <li>居室:</li>
          <li>不限</li>
          <li>一居室</li>
          <li>两居室</li>
          <li>三居室</li>
          <li>四居室以上</li>
        </ul>
        <ul>
          <li>类型:</li>
          <li>不限</li>
          <li>整租</li>
          <li>合租</li>
        </ul>
      </div>
    </div>
    <div id="box" v-for="(house,i) of houses" :key="i">
      <a href="javascript:;">
        <img :src="house.url1">
      </a>
      <div class="box-cen">
        <h5 v-text="house.h"></h5> 
        <img :src="house.url2"><span v-text="house.p1" class="small"></span><br>
        <img :src="house.url3"><span v-text="house.p2" class="small"></span><i v-text="house.i"></i><br>
        <span v-text="house.sp"></span>
      </div>
      <div class="box-money">
        <div><span v-text="house.price"></span>元/月</div>
        <router-link to="detail">
          <a href="javascript:;">查看详情</a>
        </router-link>
      </div>
    </div>
    <div id="page">
      <a href="javascript:;"><</a>
      <a href="javascript:;">1</a>
      <a href="javascript:;">2</a>
      <a href="javascript:;">3</a>
      <a href="javascript:;">4</a>
      <a href="javascript:;">5</a>
      <a href="javascript:;">></a>
    </div>
    <div class="good">好房推荐</div>
    <div id="y-like">
      <div class="y-like-room" v-for="(room,i) of rooms" :key='i'>
        <div>
          <img :src="room.url4">
        </div>
        <span class="price" v-text="room.p3"></span><span>元/月</span>
        <p v-text="room.p4"></p>
        <p v-text="room.p5"></p>
      </div>
    </div>
  </div>
<Footer />
</div>
</template>
<script>

//加载头部
import Header from './Header.vue'
//加载底部
import Footer from './Footer.vue'

export default {
  data:function(){
    return{
      lists:[
        {uname:'东城区',children:['北新桥','磁器口','崇文门','灯市口','东四','广渠门内','广渠门外','安定门','北京站','东单','东四十条','和平里北街','景泰','永定门外','天坛东门','桥湾','前门','天安门东','张自忠路','雍和宫','安德里北街','中国美术馆','天桥']},
        {uname:'西城区',children:['北土城','菜市口','东公庄','东公庄西','达官营','阜成门',' 鼓楼大街','广安门内','虎坊桥','积水潭','健德门','木樨地','南礼士路','陶然亭','西直门','新街口','宣武门','长椿街','珠市口','复兴门','西单','灵境胡同','西四','平安里','红莲南路','二里沟','金融街','牛街']},
        {uname:'朝阳区',children:['安华桥','黄渠','常营','四惠','大望路','欢乐谷景区','三元桥','北苑','金台路','光熙门','北苑路北','双井','四惠东','惠新西街南口','草房','团结湖','阜通','望京','太阳宫','百子湾','青年路','南楼梓庄','十里堡','呼家楼','潘家园','九龙山','劲松','朝阳门','望京南','建国门','成寿寺','管庄','十里河','枣营','惠新西街北口','传媒大学','双桥','柳芳','褡裢坡','立水桥南','国贸','东湖渠','芍药居','高碑店','关庄','望京西','安贞门','立水桥','安立路','东风北桥','奥体中心','大屯路东','东大桥','东直门','和平西桥','将台','金台夕照','亮马桥','永安里','小红门','肖村','焦化厂','双合','平乐园','化工','大郊亭','农业展览馆','奥林匹克公园','马泉营','孙河','北工大西门','来广营','朝阳公园','望京东','高家园','垡头','安贞桥','西坝河','芳园里','酒仙桥','北岗子','东风','管庄路口西','勇士营','香河园','石佛营','平房村','东坝中街','楼梓庄','豆各庄','红庙']},
        {uname:'海淀区',children:['慈寿寺','五道口','上地','车道沟','人民大学','清华东路西口','知春路','西二旗','永泰庄','白堆子','白石桥南','北沙滩','大钟寺','动物园','公主坟','海淀五路居','花园桥','军事博物馆','林萃桥','六道口','牡丹园','苏州街','万寿路','魏公村','五棵松','西钓鱼台','西土城','西小口','长春桥','知春里','中关村','国家图书馆','火器营','北京大学东门','西苑','圆明园','北宫门','安河桥北','马连洼','农大南路','西北旺','万寿寺','北安河','稻香湖路','永丰','永丰南','远大路','苏州桥','蓟门桥','马甸','田村','廖公庄','清河']},
        {uname:'丰台区',children:['刘家窑','石榴庄','蒲黄榆','宋家庄','角门东','北京南站','公益西桥','六里桥','六里桥东','马家堡','首经贸','湾子','新宫','郭公庄','丰台科技园','科怡路','丰台南路','纪家庙','草桥','大红门','角门西','丰台站','分钟寺','丰台东大街','张郭庄','泥洼','大瓦窑','郭庄子','大井','方庄','七里庄','西局','莲花桥','陶然桥','北京西站','丽泽商务区','菜户营','西铁营','木樨园','海户屯','大红门南','和义','东高地','火箭万源']},
        {uname:'石景山区',children:['八宝山','玉泉路','八角游乐园','古城','苹果园','金安桥','杨庄','西黄村']},
        {uname:'通州区',children:['果园','九棵树','通州北苑','同济南路','次渠南','土桥','临河里','梨园','北运河西','八里桥','通州北关','物资学院路','北运河东','通运门','高楼金']},
        {uname:'昌平区',children:['龙泽','育知路','回龙观东大街','育新','平西府','回龙观','天通苑','天通苑南','霍营','生命科学园','天通苑北','朱辛庄','沙河','沙河高教园','南邵','昌平','昌平东关','北邵洼','天通苑东']},
        {uname:'大兴区',children:['亦庄桥','亦庄文化园','荣京东街','天宫院','生物医药基地','义和庄','黄村火车站','黄村西大街','清源路','枣园','高米店南','高米店北','荣昌东街','经海路','西红门','次渠','万源街','旧宫','五福堂','德茂','瀛海']},
        {uname:'顺义区',children:['国展','花梨坎','后沙峪','南法信','石门','俸伯','顺义']},
        {uname:'房山区',children:['苏庄','良乡大学城','良乡南关','良乡大学城西','良乡大学城北','广阳城','篱笆房','长阳','稻田','阎村','星城','马各庄','饶乐府']},
        {uname:'门头沟区',children:['桥户营','栗园庄','小园']}
      ],
      houses:[
        {url1:"image/search/house1.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2590"},
        {url1:"image/search/house2.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2490"},
        {url1:"image/search/house3.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2450"},
        {url1:"image/search/house4.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2420"},      
        {url1:"image/search/house5.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2650"},
        {url1:"image/search/house6.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2770"},
        {url1:"image/search/house7.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2590"},
        {url1:"image/search/house8.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2590"},      
        {url1:"image/search/house9.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2060"},
        {url1:"image/search/house10.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2290"},
        {url1:"image/search/house11.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2880"},
        {url1:"image/search/house12.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2180"},      
        {url1:"image/search/house13.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2660"},
        {url1:"image/search/house14.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2430"},
        {url1:"image/search/house15.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2550"},
        {url1:"image/search/house16.jpg",h:"褡裢坡  定福庄北里1号院 4室1厅",url2:"image/search/1.png",p1:" 距6号线褡裢坡站550米",url3:"image/search/2.png",p2:" 建筑面积约11㎡ | 5楼 | 4室1卫 | 朝南 ",i:"合",sp:"集中供暖",price:"2340"},      
      ],
      rooms:[
        {url4:"image/search/house17.jpg",p3:"¥2230",p4:"西红门 鸿坤理想城礼域府 朝南 B室",p5:"地铁 4号线大兴线 / 约13平米 / 独立阳台"},
        {url4:"image/search/house18.jpg",p3:"¥3060",p4:"北工大西门 农光南路 朝南 A室",p5:"地铁 14号线东段 / 约12平米 / 独立阳台"},
        {url4:"image/search/house19.jpg",p3:"¥2790",p4:"丽泽商务区 万泉盛景园 朝南 C室",p5:"地铁 10号线 / 约16平米 / 独立阳台"},
        {url4:"image/search/house20.jpg",p3:"¥3890",p4:"长阳 半岛v公馆 1室1厅",p5:"地铁 房山线 / 约62平米"},
          
      ]
    }
  },
  methods: {
    show(e){
      e.target.nextElementSibling.style.display="block"
    },
    hide(e){
      e.target.nextElementSibling.style.display="none"
    },
    show2(e){
      e.target.style.display="block"
    },
    hide2(e){
      e.target.style.display="none"
    }

  },
  components:{
    Header,
    Footer
  }
}
</script>
<style scoped>
  ul{
    list-style:none;
    margin:0;
    padding:0;
  }
  a{
    color:#333;
  }
  a:hover{
    text-decoration:none;
  }
  button{
    font-family:微软雅黑
  }
  .container{
    padding:0;
  }
  .breadcrumb{
    background:transparent;
    margin:2rem 0 1rem;
    padding:0;
  }
  .breadcrumb-item a{
    font-size:0.8rem;
    color:#999;
  }
  .breadcrumb-item a:hover{
    text-decoration:none;
  }
  #ss{
    background:#f0f0f0;
    border:0.08rem solid #f0f0f0;
  }
  
  #ss .ss-search{
    padding-top:1.5rem;
    padding-left:1rem;
  }
  #ss .ss-input{
    width:60%;
    height:3rem;
    padding-left:2rem;
    border-top-left-radius:0.3rem;
    border-bottom-left-radius:0.3rem;
    border:none;
    outline:none;
    font-size:0.8rem;
    color:#999;
  }
  #ss .ss-btn{
    width:6rem;
    height:3rem;
    border-top-right-radius:0.3rem;
    border-bottom-right-radius:0.3rem;
    border:none;
    background:#00a4ac;
    color:#fff;
  }
  #ss .ss-a{
    width:7rem;
    height:3rem;
    margin-left:1rem;
    border-radius:0.3rem;
    border:none;
    background:#00a4ac;
    color:#fff;
  }
  #ss .ss-list{
    padding:1rem 0 1rem 2rem;
  }
  #ss .ss-list a{
    color:#888;
    font-size:0.8rem;
    margin-right:0.8rem;
  }
  #ss .ss-list a:hover{
    text-decoration:none;
    color:red;
  }
  #ss .filter-options{
    height:12rem;
    background:#fff;
    padding:1rem;
    position:relative;
  }
  #ss .filter-options ul{
    display:flex;
    margin-bottom:0.9rem;
    flex-wrap:wrap;
  }
  #ss .filter-options ul li:nth-child(2){
    background:#3dbcc6;
    color:#fff;
  }
  #ss .filter-options ul li:nth-child(2):hover{
    background:#3dbcc6;
    color:#fff;
  }
  #ss .filter-options ul li:nth-child(2) a{
    color:#fff;
  }
  #ss .filter-options ul li:nth-child(2) a:hover{
    color:#fff;
  }
  #ss .filter-options ul li:hover{
    color:#3dbcc6
  }
  #ss .filter-options ul li a:hover{
    color:#3dbcc6
  }
  #ss li{
    font-size:0.7rem;
    margin-right:0.4rem;
    padding:0.2rem 1rem ;
    border-radius:0.3rem;
  }
  #ss .sub-option-list{
    position:absolute;
    display:flex;
    border:0.1rem solid #f0f0f0;
    left:4rem;
    width:50rem;
    padding:0.4rem 1.5rem 0.4rem 0.9rem;
    flex-flow:row wrap;
    z-index:1;
    background:#fff;
  }
  #ss .sub-option-list a{
    margin-right:0.6rem;
  } 
  #ss .filter-options li a+div{
    display:none;
  }
  #ss .filter-options div{
    margin-top:-0.1rem;
  }
  #box{
    display:flex;
    width:100%;
    height:17rem;
    padding:2rem 0;
    justify-content:space-between;
  }
  #box>a{
    display:block;
    width:17rem;
    height:10rem;
    overflow: hidden;
  }
  #box a img{
    width:100%;
    transition: all .5s;
  }
  #box a img:hover{
    width:100%;
    transform: scale(1.2)
  }
  #box .box-cen{
    margin:0 0 0 -23rem ;
  }
  @media (min-width:992px) and (max-width:1200px){
    #box .box-cen{
       margin-left:-13rem;
    }
  }
  @media (min-width:768px) and (max-width:991px){
    #box .box-cen{
       margin-left:0rem;
    }
  }
  
  #box h5{
    margin-bottom:1.5rem;
  }
  #box h5:hover{
    color:red;
    text-decoration:underline;
  }
 
  #box .box-cen .small{
    font-size:0.5rem;
    margin:0.5rem 0;
  }
  #box .box-cen span:last-child{
    display:block;
    border:1px solid orange;
    font-size:0.5rem;
    padding:0.2rem 0.4rem;
    color:orange;
    margin-top:0.5rem;
    width:4rem;
  }
 
  #box .box-money div{
    font-size:1rem;
    margin-left:1rem;;
  }
  #box .box-money div span{
    font-size:2rem;
    color:red;
  }
  #box .box-money a{
    display:block;
    border:1px solid #999;
    width:8rem;
    height:2rem;
    line-height:2rem;
    text-align:center;
    color:#b4b4b4;
  }
  #box .box-cen img{
    width:0.7rem;
    margin-top:-0.2rem;
  }
  #box .box-cen i{
    font-size:0.5rem;
    background:#77d0d7;
    font-style:normal;
    color:#fff;
    border-radius:0.1rem;
    padding:0 0.1rem;
  }
  #page{
    display:flex;
    margin-left:28rem;
  }
  @media (min-width:768px) and (max-width:991px){
    #page{
       margin-left:20rem;
    }
  }
  #page a{
    display:block;
    width:2rem;
    height:2rem;
    line-height:2rem;
    text-align:center;
  }
  #page a:nth-child(2){
    background:#00a4ac;
  }
  
  .good{
    font-size:1.5rem;
    height:5rem;
    line-height:5rem;
    margin-bottom:1.5rem;
    border-bottom:1px solid #efefef;
  }
  #y-like{
    display:flex;
   /* flex-wrap: wrap;*/
  }
  #y-like .y-like-room{
    border:1px solid #d8d6d6;
    width:24%;
    margin-right:1%;
    overflow: hidden;
  }
  #y-like .y-like-room div{
    width:100%;
    height:12.5rem;
    overflow: hidden;
  }
  #y-like .y-like-room img{
    width:100%;
    margin-bottom:0.5rem;
    transition:all .5s ease-out;
  }
  @media (min-width:992px) and (max-width:1200px){
    #y-like .y-like-room div{
       height:10.5rem;
    }
  }
  @media (min-width:768px) and (max-width:991px){
    #y-like .y-like-room div{
       height:8rem;
    }
  }
  #y-like .y-like-room img:hover{
    width:100%;
    transform: scale(1.2);
  }
 
 
  #y-like .y-like-room p{
    margin:0.4rem 0;
  }
  #y-like .y-like-room .price{
    color:#ff7966;
    font-size:1.5rem; 
    font-weight:bold; 
  }
  #y-like .y-like-room  span{
    color:#b8b8b8;
    font-size:0.8rem; 
  }
  #y-like .y-like-room p:nth-child(4){
    font-weight:bold; 
  }
  #y-like .y-like-room p:nth-child(5){
    font-size:0.9rem;
    color:#333;
  }
</style>