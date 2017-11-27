<template>
  <div class="index-wrap">     
    <div class="index-left">
      <div class="index-left-block">
      	<h2>全部产品</h2>
       <template v-for="product in productsList">
       <h3>{{product.title}}</h3>
        <ul>
        <li v-for="item in product.list">
           	<a :href="item.url">{{item.name}}</a>
        </li>	
        </ul>
        <div v-if="product.last" class="hr"></div>	
      </template> 
      </div>
      <div class="index-left-block lastest-news">
        <h2>最新消息</h2>
         <template v-for="news in homeNewsList">
         	<h3>{{news.title}}</h3>
         	<ul>
         		<li v-for="item in news.list">
         			<a :href="item.url">{{item.name}}</a>
         		</li>
         	</ul>
         </template>	
      </div>
    </div>
    <div class="index-right">
    	<button @click="onchange">点击</button>
    </div>
  </div>
</template>


<script>
export default {
  data () {
    return {
      msg: 'hello',
      productsList: {},
      homeNewsList: []
    }
  },
  created: function () {
    this.$http.get('http://localhost:3000/getProducts')
    .then((res) => {
      this.productsList = res.data
    }, (err) => {
      console.log(err)
    })
  },
  methods: {
    onchange: function () {
      this.$http.post('http://localhost:3000/getProducts')
      .then((res) => {
        this.productsList = res.data
      }, (err) => {
        console.log(err)
      })
    }
  },
  mounted: function () {
    this.$http.get('http://localhost:3000/getHomeNewsList')
    .then((res) => {
      this.homeNewsList = res.data
    }, (err) => {
      console.log(err)
    })
  }
}
</script>
<style scoped>
.index-wrap {
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.index-left {
  float: left;
  width: 300px;
  text-align: left;
}
.index-right {
  float: left;
  width: 900px;
}
.index-left-block {
  margin: 15px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
}
.index-left-block .hr {
  margin-bottom: 20px;
}
.index-left-block h2 {
  background: #4fc08d;
  color: #fff;
  padding: 10px 15px;
  margin-bottom: 20px;
}
.index-left-block h3 {
  padding: 0 15px 5px 15px;
  font-weight: bold;
  color: #222;
}
.index-left-block ul {
  padding: 10px 15px;
}
.index-left-block li {
  padding: 5px;
}
.index-board-list {
  overflow: hidden;
}
.index-board-item {
  float: left;
  width: 400px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
  padding: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
}
.index-board-item-inner {
  min-height: 125px;
  padding-left: 120px;
}
.index-board-item h2 {
  font-size: 18px;
  font-weight: bold;
  color: #000;
  margin-bottom: 15px;
}
.line-last {
  margin-right: 0;
}
.index-board-button {
  margin-top: 20px;
}
.lastest-news {
  min-height: 512px;
}
.hot-tag {
  background: red;
  color: #fff;
}
.new-item {
  display: inline-block;
  width: 230px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>