<template>
    <div class="page">
        <div class="total">共<i>{{defaults.totalData}}</i>条</div>

        <div v-show="defaults.mode === 'fixed'">
            <a href="javascript:;" @click="changePage(index-1)" :class="defaults.prevCls">{{defaults.prevContent}}</a>
            <a href="javascript:;" @click="changePage(defaults.coping && defaults.homePage ? defaults.homePage : 1)"
               v-show="defaults.coping" data-page="1">
                {{defaults.coping && defaults.homePage ? defaults.homePage : 1}}
            </a>
            <template v-for="(item,i) in (fixedStart(),fixedEnd())">
                    <a @click="changePage(fixedStart()+i)" v-bind:key="i" v-if="(fixedStart()+i) != current()" href="javascript:;" :data-page="fixedStart()+i">{{fixedStart()+i}}</a>
                    <span v-bind:key="i" v-else :class="defaults.activeCls">{{fixedStart()+i}}</span>
            </template>
            <a @click="changePage(pageCount())" href="javascript:;" v-if="defaults.coping" :data-page="pageCount()"> {{copingEnd()}}</a>
            <a @click="changePage(index+1)" href="javascript:;" :class="defaults.nextCls">{{defaults.nextContent}}</a>
        </div>

        <div v-show="defaults.mode === 'unfixed'">
            <a @click="changePage(index-1)" href="javascript:;" v-show="defaults.keepShowPN || current() > 1" :class="defaults.prevCls">{{defaults.prevContent}}</a>
            <template v-if="defaults.coping && funFuture1()">
                <a @click="changePage(1)" href="javascript:;" data-page="1">{{home()}}</a><span>...</span>
            </template>

            <template v-for="(item,i) in (unfixedStart(),unfixedEnd())">
                <template v-if="unfixedStart() <= pageCount() && unfixedStart() >= 1">
                    <a @click="changePage(unfixedStart()+i)" v-bind:key="i" v-if="(unfixedStart()+i) !== current()" href="javascript:;" :data-page="unfixedStart()+i">{{unfixedStart()+i}}</a>
                    <span v-bind:key="i" v-else :class="defaults.activeCls">{{unfixedStart()+i}}</span>
                </template>
            </template>
            <template v-if="defaults.coping && funFuture2()">
                <span>...</span><a @click="changePage(pageCount())" href="javascript:;" :data-page="pageCount()">{{copingEnd()}}</a>
            </template>
            <a @click="changePage(index+1)" v-show="defaults.keepShowPN || current() < pageCount()" href="javascript:;" :class="defaults.nextCls">{{defaults.nextContent}}</a>
        </div>
        <template v-if="defaults.jump">
            <input @keyup.enter="jumpPageEnter()" @input="jumpPageInput()" v-model="jumpPage"  type="text" :class="defaults.jumpIptCls"><a @click="jumpPageEnter()" href="javascript:;" :class="defaults.jumpBtnCls">{{defaults.jumpBtn}}</a>
        </template>
    </div>
</template>

<script>
export default {
  name: 'Pageination',
  props: {
    msg: String
  },
  data: function () {
    return {
      index: 1,
      jumpPage: null,
      defaults: {
        totalData: 0, // 数据总条数
        showData: 0, // 每页显示的条数
        pageCount: 0, // 总页数,默认为9
        current: 1, // 当前第几页
        prevCls: 'prev', // 上一页class
        nextCls: 'next', // 下一页class
        prevContent: '<', // 上一页内容
        nextContent: '>', // 下一页内容
        activeCls: 'active', // 当前页选中状态
        coping: false, // 首页和尾页
        isHide: false, // 当前页数为0页或者1页时不显示分页
        homePage: '', // 首页节点内容
        endPage: '', // 尾页节点内容
        keepShowPN: false, // 是否一直显示上一页下一页
        mode: 'unfixed', // 分页模式，unfixed：不固定页码数量，fixed：固定页码数量
        count: 4, // mode为unfixed时显示当前选中页前后页数，mode为fixed显示页码总数
        jump: false, // 跳转到指定页数
        jumpIptCls: 'jump-ipt', // 文本框内容
        jumpBtnCls: 'jump-btn', // 跳转按钮
        jumpBtn: '跳转', // 跳转按钮文本
        callback: function () {
        } // 回调
      }
    }
  },
  created: function () {
    // this.defaults = {...this.defaults,totalData:20,showData:10,pageCount:2,mode:'unfixed',keepShowPN:true,jump:true}
    console.log(this.defaults)
  },
  methods: {
    current: function () { // 获得当前页码
      return parseInt(this.index) || parseInt(this.defaults.current)
    },
    pageCount: function () { // 获得总页码
      return this.defaults.totalData && this.defaults.showData
        ? Math.ceil(parseInt(this.defaults.totalData) / this.defaults.showData) : this.defaults.pageCount
    },
    fixedStart: function () { // fixed模式的开始页数
      return this.current() > this.defaults.count - 1
        ? this.current() + this.defaults.count - 1 > this.pageCount()
          ? this.current() - (this.defaults.count - (this.pageCount() - this.current())) : this.current() - 2 : 1
    },
    fixedEnd: function () { // fixed模式的结束页数
      return this.current() + this.defaults.count - 1 > this.pageCount() ? this.pageCount() : this.fixedStart() + this.defaults.count
    },
    copingEnd: function () {
      return this.defaults.coping && this.defaults.endPage ? this.defaults.endPage : this.pageCount()
    },
    home: function () {
      return this.defaults.coping && this.defaults.homePage ? this.defaults.homePage : '1'
    },
    funFuture1: function () { // TODO 待取合适方法名
      return this.current() >= this.defaults.count + 2 && this.current() !== 1 && this.pageCount() !== this.defaults.count
    },
    funFuture2: function () { // TODO 待取合适方法名
      return this.current() + this.defaults.count < this.pageCount() && this.current() >= 1 && this.pageCount() > this.defaults.count
    },
    unfixedStart: function () {
      return (this.current() - this.defaults.count) <= 1 ? 1 : (this.current() - this.defaults.count)
    },
    unfixedEnd: function () {
      var newVar = (this.current() + this.defaults.count) >= this.pageCount() ? this.pageCount()
        : (this.current() + this.defaults.count)
      console.log('end' + newVar)
      return newVar
    },
    changePage: function (index) {
      console.log('===' + index)
      if (index <= 0) {
        return
      }
      if (index > this.pageCount()) {
        return
      }
      this.index = index
      typeof this.defaults.callback === 'function' && this.defaults.callback()
    },
    jumpPageInput: function () {
      this.jumpPage = this.jumpPage.replace(/[^\d]/g, '')
    },
    jumpPageEnter: function () {
      this.changePage(this.jumpPage)
    },
    changeF: function () {
      console.log('子组件单击开始')
      this.$emit('changeP')
    },
    parentHandleclick (e) {
      console.log(e)
      this.childMsg = e
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .m-style {
        position: absolute;
        right:25px;
        text-align: center;
        zoom: 1;
    }

    .m-style:before,
    .m-style:after {
        content: "";
        display: table;
    }

    .m-style:after {
        clear: both;
        overflow: hidden;
    }

    .m-style span {
        float: left;
        margin: 0 5px;
        width: 38px;
        height: 38px;
        line-height: 38px;
        color: #bdbdbd;
        font-size: 14px;
        border-radius: 6px;
    }

    .m-style .total {
        float: left;
        margin: 0 5px;
        height: 38px;
        line-height: 38px;
        color: #bdbdbd;
        font-size: 14px;
        border-radius: 6px;
    }

    .m-style .active {
        float: left;
        margin: 0 5px;
        width: 38px;
        height: 38px;
        line-height: 38px;
        background: #2db7f5;
        color: #fff;
        font-size: 14px;
        border: 1px solid #2db7f5;
        border-radius: 6px;
    }

    .m-style a {
        float: left;
        margin: 0 5px;
        width: 38px;
        height: 38px;
        line-height: 38px;
        background: #fff;
        border: 1px solid #ebebeb;
        color: #bdbdbd;
        font-size: 14px;
    }

    .m-style a:hover {
        color: #fff;
        background: #2db7f5;
    }

    .m-style .next,
    .m-style .prev {
        font-family: "Simsun";
        font-size: 16px;
        font-weight: bold;
    }

    .now,
    .count {
        padding: 0 5px;
        color: #f00;
    }

    .eg img {
        max-width: 800px;
        min-height: 500px;
    }

    .m-style input {
        float: left;
        margin: 0 5px;
        width: 38px;
        height: 38px;
        line-height: 38px;
        text-align: center;
        background: #fff;
        border: 1px solid #ebebeb;
        outline: none;
        color: #bdbdbd;
        font-size: 14px;
    }
</style>
