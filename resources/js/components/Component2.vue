<template>
  <div class="main">
    <div class="menu">

      <div class="menu-item home">Home</div>
      <div class="menu-item projects">Projects</div>
      <div class="menu-item profils">Profils</div>
      <div class="menu-item agenda">Agenda</div>
      <div class="menu-item salle">Salle</div>
      <div class="menu-item intranet">Intranet</div>
      <div class="menu-item smartdesk">Smartdesk</div>
      

    </div>
    <splitpanes class="default-theme" @resize="log($event)" @resized="resizedLog($event)" style="height: 100vh;">
      <pane :size="paneSize" min-size="30" max-size="50">
        <div class="m-5 border ">
          <span id="open-slit" class="open-slit" v-on:click="closeNav()">
            <svg width="11" height="17" viewBox="0 0 11 17" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M2 8.5L1.29289 7.79289L0.585786 8.5L1.29289 9.20711L2 8.5ZM8.79289 16.7071C9.18342 17.0976 9.81658 17.0976 10.2071 16.7071C10.5976 16.3166 10.5976 15.6834 10.2071 15.2929L8.79289 16.7071ZM8.79289 0.292893L1.29289 7.79289L2.70711 9.20711L10.2071 1.70711L8.79289 0.292893ZM1.29289 9.20711L8.79289 16.7071L10.2071 15.2929L2.70711 7.79289L1.29289 9.20711Z" fill="#35373C"/>
            </svg>
          </span>
          
          <draggable
            class="row row-dorg"
            :list="list1"
            :options="{animation:200}"
            group="people"
            @change="log"
            itemKey="name"
          >
            <div class="card element-card m-3 col-3" v-for="element in list1" :key="element.id">
              <div class="card-body">
                {{element.name}} - {{element.id}}
              </div>
            </div>

          </draggable>
        </div>
      </pane>

      <pane :size="100 - paneSize" min-size="50" max-size="70">
        <div class="m-5 p-grid p-fluid border dashboard">
           <span id="open-slit-right" class="open-slit-right" v-on:click="openNav()">
              <svg width="11" height="17" viewBox="0 0 11 17" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M9 8.5L9.70711 9.20711L10.4142 8.5L9.70711 7.79289L9 8.5ZM2.20711 0.292893C1.81658 -0.0976321 1.18342 -0.0976321 0.792895 0.292893C0.40237 0.683417 0.40237 1.31658 0.792895 1.70711L2.20711 0.292893ZM2.20711 16.7071L9.70711 9.20711L8.29289 7.79289L0.792893 15.2929L2.20711 16.7071ZM9.70711 7.79289L2.20711 0.292893L0.792895 1.70711L8.29289 9.20711L9.70711 7.79289Z" fill="#35373C"/>
              </svg>
           </span>

          <draggable
            class="row row-dorg"
            :list="list2"
            :options="{animation:200}"
            group="people"
            @change="log"
            itemKey="name"
          >
            <div class="card element-card  m-3 col-3" v-for="element in list2" :key="element.id">
              <div class="card-body">
                {{element.name}} - {{element.id}}
              </div>
            </div>        
          </draggable>
        </div>
      </pane>
    </splitpanes>
  </div>
</template>
<script>
import { Splitpanes, Pane } from 'splitpanes'
import 'splitpanes/dist/splitpanes.css'
import draggable from 'vuedraggable'

export default {
  components: {Splitpanes, Pane, draggable},
  data () {
    return {
      opened: false,
      paneSize: 40,
      list1: [
        { name: "John", id: 9 },
        { name: "Joao", id: 10 },
        { name: "Jean", id: 11 },
        { name: "Gerard", id: 12 },
        { name: "OKay", id: 13 },
        { name: "Franck", id: 14 },
        { name: "TOTO", id: 15 },
        { name: "Derm", id: 16 }
      ],
      list2: [
        { name: "Juan", id: 1 },
        { name: "Edgard", id: 2 },
        { name: "Johnson", id: 3 },
        { name: "Task", id: 4 },
        { name: "Calender", id: 5 },
        { name: "Option", id: 6 },
        { name: "Span", id: 7 },
        { name: "DIv", id: 8 }
      ]
    }
  },
  methods: {
    add: function() {
      this.list.push({ name: "Juan" });
    },
    replace: function() {
      this.list = [{ name: "Edgard" }];
    },
    clone: function(el) {
      return {
        name: el.name + " cloned"
      };
    },
    log: function(evt) {
      this.paneSize = evt[0].size
      let toto = 50 - this.paneSize
      let val = 50 - toto
      let val1 = 50 + toto
      document.getElementById("open-slit-right").style.left = val + '%';
      document.getElementById("open-slit").style.right = val1 + '%';
      console.log(val1);
    },
    resizedLog(evt){
      if(evt[0].size == 50){
        document.getElementById("open-slit-right").style.display = 'none';
         document.getElementById("open-slit").style.display = '';
      }else if(evt[0].size == 30){
        document.getElementById("open-slit-right").style.display = '';
        document.getElementById("open-slit").style.display = 'none';
      }else{
        document.getElementById("open-slit-right").style.display = '';
        document.getElementById("open-slit").style.display = '';
      }
    },
    openOrClose(){
      if(this.opened){
        this.closeNav();
      }else{
        this.openNav();
      }
    },
    openNav() {
      this.opened = true;
      this.paneSize = 50
      document.getElementById("open-slit-right").style.display = 'none';
      document.getElementById("open-slit").style.display = '';
      document.getElementById("open-slit-right").style.left = this.paneSize + '%'
      document.getElementById("open-slit").style.right = this.paneSize + '%'

    },
    closeNav() {
      this.opened = false;
      this.paneSize = 30
      document.getElementById("open-slit-right").style.display = '';
      document.getElementById("open-slit").style.display = 'none';
      document.getElementById("open-slit-right").style.left = this.paneSize + '%'
      document.getElementById("open-slit").style.right = '70%'
    }
  },
  computed: {

  }
}
</script>

<style>
.splitpanes__splitter {width: 0px !important; border: 1px solid #000000 !important; position: relative;}
.open-slit {
  position: absolute;
  top: 47%;
  right: 60%;
  font-size: 20px;
  cursor: pointer;
  padding: 8px;
  z-index: 999;
}
.open-slit-right {
  position: absolute;
  top: 47%;
  left: 40%;
  font-size: 20px;
  cursor: pointer;
  padding: 8px;
  z-index: 999;
}
.menu{
  
  height: 56px;
  left: 0px;
  top: 0px;
  background: #000000;
}
.menu-item{
  position: absolute;
  width: 71px;
  height: 34px;
  top: 15px;
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 170.19%;
  letter-spacing: 0.06em;
  color: #FFFFFF;
}
.home{
  left: 49px;
}
.projects{
  left: 319px;
}
.profils{
  left: 466px;
}
.agenda{
  left: 613px;
}
.salle{
  left: 760px;
}
.intranet{
  left: 907px;
}
.smartdesk{
  right: 49px;
}

.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0.5s;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.row-dorg {
  min-height: 50px;
}
.element-card {
  cursor: move;
}
.element-card i {
  cursor: pointer;
}
</style>

