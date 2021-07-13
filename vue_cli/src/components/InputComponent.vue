<template>
  <div class="wrap">
    <div class="input-box">
      <input type="text" v-model="newInputItem" v-on:keyup.enter='addItem' placeholder="스케줄을 입력하세요!">
      <button v-on:click='addItem'>ADD</button>
    
    </div>
  </div>
</template>

<script>
export default {
  data() { //1. 데이터 메서드
    return {
      newInputItem:'',  //v-model 양방향 전송
      cnt:0
    }
  },
  methods:{
    addItem() { //2. addItem:function(){} ADD 버튼 클릭 이벤트 호출 메서드
                // alert('ADD 버튼 클릭 이벤트 호출 메서드');
      var value = this.newInputItem;
          // console.l og( value );
          // this.cnt++;
          //3. 로컬스토레이지
          // localStorage.setItem(this.cnt, value); 테스팅
          
          //4. 이벤트 전달속성 이름 에밋
          this.$emit('addItem', value); //전달인자(아규먼트)

          //5. 입력이 완료되면 전달되면 입력상자를 다음 입력을 위해서 지운다
          this.inputText(); //입력상자 지우기 메서스 호출 실행

          // 탬플릿트에 발생하는 이벤트는
          // 반드시 $emit() 으로 이벤트를 생성하여 생성된 이름을

          // 상위 컴포넌트에서 전달한다.
          // 그러면 상위 컴폰넌트는 전달받은 이벤트이름속성을 이용하영
          // 상위 컴포넌트에서 메서드를 호출하여 이벤트를 수행한다.

    },
    inputText(){
        this.newInputItem = '';
        // alert('삭제됨!!');
    }
  }
}
</script>

<style scoped>
.wrap {width:100%;}
.wrap .input-box {width:85%;margin:0 auto;padding:15px 0;display:flex;}
.wrap .input-box input[type='text'] {width:auto;height:50px;border:1px solid #ccc;box-sizing:border-box;width:100%;padding:0 15px;border-radius:8px 0px 0px 8px;margin-right:auto;/* 왼쪽정렬 */}
.wrap .input-box input[type='text']::placeholder {color:#bbb;}
.wrap .input-box button {width:auto;height:50px;border:0;background:#2c3e50;color:#fff;width:60px;border-radius:0px 8px 8px 0px;margin-left:auto;/* 오른쪽정렬 */}

</style>