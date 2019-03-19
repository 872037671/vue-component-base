<template>
  <div class="hello">
    <div class="box" v-for="item in list">
      <img :src="item" alt="">
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pageIndex: {
      type: Number
    },
    list: {
      type: Array
    },
    pageSize: {
      type: Number
    },
    loading: {
      type: Boolean
    },
    getList: {
      type: Function
    }
  },
  name: 'HelloWorld',
  data () {
    return {
      judgeStatus: true
    }
  },
  watch: {
    list() {
      this.$nextTick(() => {
        this.onscroll()
      })
    },
  },
  methods: {
    judgeList() {
      if (this.loading) {
        this.$emit('getList')
      }
    },
    onscroll() {
      let Par = document.getElementsByClassName('hello')[0];
      let imgbox = Par.getElementsByTagName('div');
      window.onscroll = () => {
        let seeHeight = document.documentElement.clientHeight;
        let docHeight = Par.scrollHeight;
        let scrollTop = document.body.scrollTop || document.documentElement.scrollTop;
        if (docHeight<=scrollTop+seeHeight) {
          console.log(docHeight)
          console.log(document.body.scrollHeight)
          this.judgeList()
          window.onscroll = null;
        }
      }
    }
  },
  created() {
    if (this.loading) {
      this.$emit('getList')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
body {
  padding-bottom: 800px;
}
.hello {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.box {
  width: 50%;
}
img {
  width: 100%;
  display: block
}
</style>
