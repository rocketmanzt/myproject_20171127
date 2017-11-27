<template>
	<div>
		<div v-show="isShow" class="box1">这是box1</div>
		<div class="news-main">
		<h1>{{msg}}</h1>
		<template v-for="item in newsList">
			<a :href="item.href">{{item.title}}</a>
			<br>
			<p>{{item.content}}</p>
		</template>
		</div>
		<div class="imgs-main">
		<h1>{{img}}</h1>
		<template v-for="item in imgsList">
           <a :href="item.href">{{item.name}}</a>
		</template>
		<button @click="pop" >弹出</button>
		</div>
	</div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'hello',
      img: '图片',
      isShow: false,
      newsList: [
        {
          title: 'news1',
          content: '这是新闻1内容',
          href: 'https://www.baidu.com/'
        },
        {
          title: 'news2',
          content: '这是新闻2内容这是新闻2内容这是新闻2内容',
          href: 'https://www.baidu.com/'
        }
      ],
      imgsList: []
    }
  },
  created: function () {
    this.$http.get('http://localhost:3000/getImgsList')
    .then((res) => {
      this.imgsList = res.data
    }, (err) => {
      console.log(err)
    })
  },
  methods: {
    pop () {
      this.isShow = !this.isShow
    }
  }
}
</script>

<style scoped>
.news-main,.imgs-main{
	width: 1200px;
	text-align: center;
	margin: 0 auto;
}
.news-main h1{
  font-size:20px;
}
.box1{
	width: 100%;
	height: 100%;
	position: relative;
	background: #666;
	opacity: 0.5;
}
</style>