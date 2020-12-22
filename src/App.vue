<template>
  <div id="app">
    <div>
      <h1 :class="runAnimation">Animate.css</h1>
      <h2>Just-add-water CSS animations</h2>
      <button class="openMenuBtn" @click="menu()">See Animations</button>
    </div>
    <div class="box" :class="res == true ? 'open' : ''" >
      <button class="closeMenuBtn" @click="res = false">Close List</button>
      <ul>
        <li v-for="(data, index) in allData" :key="index">
          <p class="bold">{{ data.title }}</p>
          <ul>
            <li v-for="(item, index) in data.text" :key="index"
                @click="runAnimation = 'animate__animated animate__'+item; startAnimation()">
                <span>{{ item }}</span>

                <i @click="copyAnimation = 'animate__animated animate__'+item; copy();"
                   class="far fa-copy"></i>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="link" @click="copyToLink()">Click to copy Animate.css library link</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      res : false,
      runAnimation : "",
      copyAnimation : "",
      timeout : "",
      allData : [
        {title: "Attention Seekers", text: ["bounce", "flash", "pulse", "rubberBand", "shakeX", "shakeY", "headShake", "swing", "tada",
            "wobble", "jello", "heartBeat"]},
        {title: "Back Entrances", text: ["backInDown", "backInLeft","backInRight","backInUp"]},
        {title: "Back Exits", text: ["backOutDown","backOutLeft", "backOutRight", "backOutUp"]},
        {title: "Bouncing Entrances", text: ["bounceIn", "bounceInDown", "bounceInLeft", "bounceInRight", "bounceInUp"]},
        {title: "Bouncing Exits", text: ["bounceOut", "bounceOutDown", "bounceOutLeft", "bounceOutRight", "bounceOutUp"]},
        {title: "Fading Entrances", text: ["fadeIn", "fadeInDown", "fadeOutDownBig", "fadeOutLeft", "fadeOutLeftBig", "fadeOutRight",
            "fadeOutRightBig", "fadeOutUp", "fadeOutUpBig", "fadeOutTopLeft", "fadeOutTopRight",
            "fadeOutBottomRight", "fadeOutBottomLeft"]},
        {title: "Flippers", text: ["flip", "flipInX", "flipInY", "flipOutX", "flipOutY"]},
        {title: "Lightspeed", text: ["lightSpeedInRight", "lightSpeedInLeft", "lightSpeedOutRight", "lightSpeedOutLeft"]},
        {title: "RotatingEntrances", text: ["rotateIn", "rotateInDownLeft", "rotateInDownRight", "rotateInUpLeft", "rotateInUpRight"]},
        {title: "Rotating Exits", text: ["rotateOut", "rotateOutDownLeft", "rotateOutDownRight", "rotateOutUpLeft", "rotateOutUpRight"]},
        {title: "Specials", text: ["hinge", "jackInTheBox", "rollIn", "rollOut"]},
        {title: "Zooming Entrances", text: ["zoomIn", "zoomInDown", "zoomInLeft", "zoomInRight", "zoomInUp"]},
        {title: "Zooming Exits", text: ["zoomOut", "zoomOutDown", "zoomOutLeft", "zoomOutRight", "zoomOutUp"]},
        {title: "Sliding Entrances", text: ["slideInDown", "slideInLeft", "slideInRight", "slideInUp"]},
        {title: "Sliding Exits", text: ["slideOutDown", "slideOutLeft", "slideOutRight", "slideOutUp"]},
        ]
    }
  },
  methods : {
    copy(){
      var textarea = document.createElement('textarea');
      textarea.value = this.copyAnimation;
      document.body.appendChild(textarea);
      textarea.select();

      let old_div = document.querySelector('.alert');
      if (old_div){
          old_div.parentNode.removeChild(old_div);
      }

      let alert = document.createElement('div');
      alert.className = 'alert';
      alert.innerText = "Copied "+this.copyAnimation + '!'
      console.log(alert.innerText)
      document.body.appendChild(alert)
      setTimeout(() => alert.classList.add('active'), 1);
      setTimeout(() => alert.classList.remove('active'), 3000);
      setTimeout(() => { document.body.removeChild(alert) }, 3500);

      document.execCommand('copy');
      document.body.removeChild(textarea);
    },
    startAnimation(){
      window.clearTimeout(this.timeout)
      let cm = this;
      this.timeout = setTimeout(() => {
        cm.runAnimation = ""
      }, 1500)
    },
    menu(){
      if(this.res == false){
        this.res = true;
      }else{
        this.res = false;
      }
    },
    copyToLink(){
      var textarea = document.createElement('textarea');
      textarea.value = 'https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css';
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);
    },
  }
}


</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  outline: 0;
  list-style: none;
}
body,
html{
  width: 100vw;
  height: 100vh !important;
  overflow: hidden;
}
#app{
  width: 100%;
  height: 100vh;
  background: #FCE5CD;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
h1{
  display: inline-block;
  width: 100%;
  text-align: center;
  font-size: 80px;
  color: #351C75;
  font-family: sans-serif;
}
h2{
  display: inline-block;
  width: 100%;
  text-align: center;
  font-size: 26px;
  color: #EA9D4F;
  font-family: sans-serif;
}
.alert{
  position: fixed;
  top: -150px;
  left: 20px;
  padding: 10px 30px;
  background: #0C1226;
  color: #fff;
  font-size: 18px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  border-radius: 30px;
  transition: 300ms;
}
.alert.active{
  top: 20px;
}
.alert::selection{
  background: none;
}
.box{
  position: absolute;
  padding: 50px 40px;
  width: 15% !important;
  min-width: 320px;
  height: 100vh;
  top: 0;
  right: 0;
  background: #F7D7B5;
  overflow: scroll;
  z-index: 10;
}
.bold{
  display: inline-block;
  margin-top: 20px !important;
  margin-bottom: 10px !important;
  font-size: 20px !important  ;
  font-weight: bold;
  font-family: sans-serif;
  cursor: default;
}
li{
  margin-bottom: 9px;
  font-size: 16px;
  font-family: sans-serif;
  cursor: pointer;
  transition: opacity 300ms;
}
ul li ul li{
  position: relative;
}
ul li ul li:hover span{
   opacity: .6;
   transition: opacity 300ms;
}
ul li ul li:hover .far{
  visibility: visible;
}
ul li ul li .far{
  color: black;
  opacity: .5;
  position: absolute;
  right: 0;
  font-size: 18px;
  transition: opacity 500ms;
  visibility: hidden;
}
ul li ul li .far:hover{
  opacity: 1;
  transition: opacity 500ms;
}
.openMenuBtn, .closeMenuBtn{
  background: none;
  border: none;
  cursor: pointer;
  margin: 10px 0;
  font-size: 16px;
  border: 1px solid #351C75;
  padding: 8px 16px;
  color: #351C75;
  border-radius: 5px 16px 5px 16px;
  transition: all .5s ease-in-out;
  display: none !important;
}
.openMenuBtn:hover, .closeMenuBtn:hover{
  background: #351c75 !important;
  color: #fff;
  transition: all .2s;
}
.openMenuBtn{
  display: block;
  margin: 20px auto;
}
.link{
  position: absolute;
  bottom: 3%;
  left: 3%;
  font-size: 20px;
  cursor: pointer;
  transition: 300ms;
}
.link:hover{
  opacity: .7;
}
@media(max-width: 1200px){
  .box{
    display: none;
  }
  .box.open{
    display: block;
  }
  .openMenuBtn, .closeMenuBtn{
    display: block !important;
  }
}

</style>
