<template>
    <div class="page">
        <div class="total">共<i>{{defaults.totalData}}</i>条</div>
        <div v-show="defaults.mode === 'fixed'">
            <a href="javascript:;" class="{{defaults.prevCls}}">{{defaults.prevContent}}</a>
            <a href="javascript:;" v-show="defaults.coping" data-page="1">{{defaults.coping && defaults.homePage ? defaults.homePage : 1}}</a>
        </div>

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
                defaults: {
                    totalData: 0, //数据总条数
                    showData: 0, //每页显示的条数
                    pageCount: 9, //总页数,默认为9
                    current: 1, //当前第几页
                    prevCls: 'prev', //上一页class
                    nextCls: 'next', //下一页class
                    prevContent: '<', //上一页内容
                    nextContent: '>', //下一页内容
                    activeCls: 'active', //当前页选中状态
                    coping: false, //首页和尾页
                    isHide: false, //当前页数为0页或者1页时不显示分页
                    homePage: '', //首页节点内容
                    endPage: '', //尾页节点内容
                    keepShowPN: false, //是否一直显示上一页下一页
                    mode: 'unfixed', //分页模式，unfixed：不固定页码数量，fixed：固定页码数量
                    count: 4, //mode为unfixed时显示当前选中页前后页数，mode为fixed显示页码总数
                    jump: false, //跳转到指定页数
                    jumpIptCls: 'jump-ipt', //文本框内容
                    jumpBtnCls: 'jump-btn', //跳转按钮
                    jumpBtn: '跳转', //跳转按钮文本
                    callback: function () {
                    } //回调
                }
            };
        },
        created: {
            this.defaults = {...this.defaults,totalData:20,showData:10,pageCount:2}
        },
        methods: {
            changeF: function () {
                console.log("子组件单击开始");
                this.$emit('changeP');
            },
            parentHandleclick(e) {
                console.log(e)
                this.childMsg = e;
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
