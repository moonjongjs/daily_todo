<template>
  <div class="wrap">
    <div class="list-box">
        <ul>
          <li v-for='(item, index) in propsdata' v-bind:key='item'>
                                        <!-- 삭제할 메서드와 아규먼트 값, 인덱스번호 -->
            <span><input type="checkbox" v-on:change='deleteFn(item, index)' value=""></span>
            <div>{{ item }}</div>
          </li>
        </ul>
    </div>
  </div>
</template>

<script>
export default {
  //프롭스 설정
  props:['propsdata'],
  methods:{
    deleteFn(item, index){
        this.$emit('chkevtemit', item, index); //상위 컴포넌트로 전달될 이벤트속성이름과 아규먼트 값, 인덱스번호
    }
  }
}
</script>

<style scoped>
.wrap {width:100%;}
.wrap .list-box {width:100%;}
.wrap .list-box ul {margin:0 10px;text-align:left;}
.wrap .list-box ul li {background:#fff;margin:4px 0;line-height:47px;width:100%;display:flex;}
.wrap .list-box ul li span {margin-right:10px;}
.wrap .list-box ul li div {color:#555;font-size:15px;white-space:nowrap;text-overflow:ellipsis;overflow:hidden;width:100%;}
</style>