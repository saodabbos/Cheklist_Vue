<template>
  <div id = "app">
                <ul>
                    <div v-for = '(item, index) in items' :key="index">
                    <li>
                       <span>
                        <span @dblclick = 'editItem($event.target.value)'> {{item}} </span>
                        <input  type = "checkbox" @click = 'editCheck($event)'>
                    </span>
                        <a href="#" @click = 'del($event)'>удалить</a>
                    </li>
                    </div>
            </ul>
            <input type="text" v-model = 'item' @keyup.enter = 'add($event.target.value)' class = "inp">
  </div>
</template>
<script>

export default {
  name: 'App',
  data () {
    return {
      item:'',
      items:[]
    }
  },
  methods: {
            add(){
                if(this.item != ''){
                    this.items.push(this.item);
                    this.item = '';
                }
            },
            editItem(event){
                let tar = event.target;
                let input = document.createElement('input');
                input.value = tar.innerHTML;
                tar.innerHTML = '';
                input.addEventListener('keypress',function(event){
                    if(event.key == 'Enter'){
                        tar.innerHTML = this.value;
                    this.value = '';
                    }
                })
                tar.appendChild(input);
            },
            editCheck(event){
                let tar = event.target;
                tar.parentElement.classList.add('ty');
                tar.parentElement.parentElement.classList.add('back');
                tar.parentElement.removeChild(tar);
            },
            del(event){
                event.preventDefault();
                let tar = event.target;
                tar.parentElement.remove();
            }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
 .ty {
        text-decoration: line-through;
    }
    .back {
        border: none;
        background-color: lightslategrey;
    }
    ul {
        margin: 0;
        padding: 0;
    }
    li {
        display: flex;
        justify-content: space-between;
        border: 1px solid blue;
        background-color: rgba(16, 103, 129, 0.151);
        margin-top:3px;
        font-size: 20px;
        padding: 5px;
    }
    .inp{
      margin-top:20px
    }
</style>
