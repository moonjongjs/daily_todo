<template>
  <div id="app">
      <header-component></header-component>
      <!-- <input-component v-on:하위컴포넌트에서에밋으로생성된이름='상위컴포넌트의메서드'></input-component> -->
      <input-component v-on:addItem='addItem'></input-component>
      <list-component v-bind:propsdata='itemArr'   v-on:chkevtemit='deleteFn'></list-component>
      <footer-component></footer-component>
  </div>
</template>


<script>
import HeaderComponent from './components/HeaderComponent.vue'
import InputComponent from './components/InputComponent.vue'
import ListComponent from './components/ListComponent.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  name: 'app',
  data () {
    return {
                    //리스트 목록이 나타날려면 로컬스토레이지에 저장된 모든 데이터를 가져와서 
                    //배열에 저장한다. created 메서드 에서 저장시작 그리고 리스트에 데이터 나타남
        itemArr:[]  //로컬스토레이지 데이터 저장 0 1 2 ... 인덱스 기억장소
                    //itemArr['우리나라', '조국', '대한민국', '웹앱 Vue.js', '반응형웹앱']
                    //배열 삭제 : 조국 삭제
                    //삭제할 인덱스 번호는 list목록에서 매개변수로 전달 받아서 삭제한다.
                    //ListComponent >> list목록
                    //itemArr.splice(인덱스번호,삭제항목갯수);
                    //itemArr.splice(1,1);
    }
  },
  components:{
    'header-component':HeaderComponent,
    'input-component':InputComponent,
    'list-component':ListComponent,
    'footer-component':FooterComponent
  }, 
  methods:{
    addItem(z){ //에밋에서 전달된 아규먼트값이 매개변수로 들어옴
      // alert('클릭이벤트가 전달되어서 상위 컴포넌트에서 메서드 호출 됨');
      
       //입력 폼에서 입력된 내용 z 변수로 가져옴
      localStorage.setItem(z, z);  // 로컬스토레이지 데이터 저장하기
      this.itemArr.push(z); //배열에 저장하기
    },
    deleteFn(item, index){ //체크박스 클릭하면 메서드 실행
        // console.log('하위컴포넌트에서 전달된 값과 인덱스번호 ', item, index);
        //1. 삭제 - 배열 삭제
        this.itemArr.splice(index, 1); //해당인덱스번호 1개삭제
        //2. 로컬스토레이지 삭제
        localStorage.removeItem(item); //스토레이지 목록 내용이 삭제
        alert('삭제 되었습니다.!!!');
    }
  },
  created() {
    //로컬스토레이지 데이터 가져와서 배열에 저장한다. 
    //그래야 배열을 v-for 반복문으로 반복처리
    console.log('localStorage.length ', localStorage.length );
    for(var i=0; i<localStorage.length; i++){
      this.itemArr[i] = localStorage.key(i);
    }

  }
}
</script>

<style>


</style>
