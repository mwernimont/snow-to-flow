<template>
  <div class="sidebar collapsed">
    <div class="sidebarContent">
      <div class="titleAndExit">
        <button
          class="reveal"
          @click="toggle"
        >
          <slot name="sidebarTitle">
            Reveal
          </slot>
        </button>
        <div
          class="exit hidden"
          @click="toggle"
        >
          X
        </div>
      </div>
      <div class="messageArea">
        <div class="message">
          <slot name="sidebarMessage">
            Message
          </slot>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
    name: "SidebarTwo",
    mounted(){
        this.$nextTick(function(){
            this.setDimensions();
        });
    },
    methods:{
        setDimensions(){
            const sidebar = this.$el;
            const button = this.$el.querySelector(".reveal").getBoundingClientRect();
            sidebar.style.height = `${button.height}px`;
            sidebar.style.width = `${button.width}px`;
        },
        toggle(){
            const exit = this.$el.querySelector(".exit");
            exit.classList.toggle("hidden");
            if(this.$el.classList.contains("expanded")){
                
                this.$el.classList.remove("expanded");
                this.$el.classList.add("collapsed");
                this.setDimensions();
            }else{
                this.$el.classList.remove("collapsed");
                this.$el.classList.add("expanded");
                this.$el.style.width = "auto";
                this.$el.style.height = "auto";
            }   
        }
    }
}
</script>
<style lang="scss" scoped>
.sidebar{
    display: flex;
    flex-direction: column;
    margin-top: 15px;
    transition: width 2s, height 2s, transform 2s;
    will-change: width;
    background: rgb(100,100,100);
}
.titleAndExit{
    position: relative;
    color:#fff;
    font-weight: bold;
}
.reveal{
    padding: 5px 10px;
    outline: none;
}
.exit{
    position: absolute;
    right: 0;
    top: 0;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5em;
    padding: 10px;
    cursor: pointer;
    &:hover{
        background: #fff;
        color:#000;
    }
}
.messageArea{
    padding:0 10px 10px 10px;
}
.message{
    background: #fff;
    padding: 10px;
    p{
        margin: 0;
        padding: 0;
    }
}
.collapsed{
    .message{
        width: 0;
        height: 0;
        opacity: 0;
    }
}
.hidden{
    display: none;
}
</style>