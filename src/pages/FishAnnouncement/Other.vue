<template lang="html">
  <div class="container">
      <div class="normal" v-for="(item, index) in lists" :key="item" @click="displayDetail(item.id)">
        <div class="title">
          <div class="top" v-show="item.is_tui == 1">
            头条
          </div>
          <h1>{{item.title}}</h1>
        </div>
        <div class="content">
          {{item.description}}
        </div>
        <div class="time">
          {{item.create_time}}
        </div>
        <div class="mask"></div>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      Top: true,
      normal: false,
      lists: []
    }
  },
  methods: {
    displayDetail (id) {
      this.$router.push({
        name: 'AnnouncementDetail', params: { id: id }
      })
    }
  },
  mounted () {
    console.log(this.$store.state.fish.d)
    let param = new URLSearchParams()
    param.append('get_cate', '1')
    this.axios.post('http://yulejia.pnnnc.com/api/announce', param)
    .then(res => {
      console.log(res);
        console.log(res.data.data.data);
        this.lists = res.data.data.data[2]
    })
  },
  created () {
    this.lists.forEach(list => {
      list.isClicked = false
    })
  },
}
</script>

<style lang="css" scoped>
.normal {
  padding-top: .2rem;
  margin-left: .5rem;
  margin-right: .4rem;
  word-wrap: break-word;
}
.normal:nth-child(1) {
  margin-top: 1.34074074rem;
}
.title {
  height: .6rem;
  display: flex;
  margin-bottom: .3rem;
  overflow: hidden;
  text-overflow: ellipsis;
}
.top {
  width: 1rem;
  height: .6rem;
  background-color: #f39800;
  color: white;
  margin-right: .25rem;
  border-radius: 5px;
  text-align: center;
  line-height: .6rem;
}
h1 {
  display: block;
  font-size: 14px;
  color: #3e3a39;
  margin:0;
}
.content {
  font-size: 12px;
  font-family:Helvetica;
  color: #898989;
  text-overflow:
  -o-ellipsis-lastline;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  margin-bottom: .2rem;
}
.time {
  text-align: right;
  opacity: .65;
}
.mask {
  border-bottom: 1px solid #F0F0F0;
  width: 100%;
  height: .2rem;
}
</style>
s
