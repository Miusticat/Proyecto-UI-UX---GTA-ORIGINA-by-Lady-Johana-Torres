<template>
    <div class="speedometershow">
        <div style="height: 2px; background-color: transparent" v-if="speedometershow">
            <div class="info.vehicle">
            <div class="group-container" style="position: absolute;">
                <!-- Componente vue-ellipse-progress para mostrar el medidor de velocidad -->
                <div style="position: absolute; top: 348px; left: 66%; transform: translate(-50%, -50%);">
                    <vue-ellipse-progress :progress="speedProgress" :angle="-36" color="#F80B52" emptyColor="transparent"
                        :size="290" :thickness="8" emptyThickness="0%" animation="reverse 700 400" lineMode="out-over"
                        :legend="false" legendClass="legend-custom-style" dash="60 0.9" :noData="false" :loading="false"
                        fontColor="white" :half="true" fontSize="1.5rem">
                        <p class="kmhtext">
                            {{ speed2 }} KM/H
                        </p>
                    </vue-ellipse-progress>
                </div>
                <!-- Icono del grupo -->
                <img class="group-icon" alt="" src="../assets/images/hud/vc1.png" style="width: 100%;" />
                <!-- Etiquetas para mostrar la velocidad en formato numérico -->
                <div class="div10" style="position: absolute; top: 58%; left: 63%; transform: translate(-50%, -50%);">{{ speed2 }}</div>
                <div class="div11" style="position: absolute; top: 58%; left: 63%; transform: translate(-50%, -50%);">{{ speed2 }}</div>

                 <!-- Icono de vehículo -->
                 <img v-if="vehiclengine == 1" src="../assets/images/hud/veh_abierto.svg" alt="Car" style="position: absolute; top: 400px; left: 395px; transform: translate(-50%, -50%);">
                 <img v-else src="../assets/images/hud/veh_cerrado.svg" alt="Car" style="position: absolute; top: 400px; left: 395px; transform: translate(-50%, -50%);">
                 <!-- Icono de llave -->
                 <img v-if="locked == 1" src="../assets/images/hud/veh_abierto.svg" alt="Key" style="position: absolute; top: 400px; left: 395px; transform: translate(-50%, -50%);">
                 <img v-else src="../assets/images/hud/veh_cerrado.svg" alt="Key" style="position: absolute; top: 400px; left: 395px; transform: translate(-50%, -50%);">
                 <!-- Icono de cinturón -->
                 <img v-if="belt == 1" src="../assets/images/hud/nobelt.svg" alt="Belt" style="position: absolute; top: 422px; left: 378px; transform: translate(-50%, -50%);">
                 <img v-else src="../assets/images/hud/belt.svg" alt="Belt"  style="position: absolute; top: 422px; left: 378px; transform: translate(-50%, -50%);">
                 <!-- Icono de aceite -->
                 <img v-if="oel >= 35" src="../assets/images/hud/oil.svg" alt="Oil" style="position: absolute; top: 350px; left: 417px; transform: translate(-50%, -50%);">
                 <img v-else-if="oel <= 35 && oel > 5" src="../assets/images/hud/oil_yellow.svg" alt="Oil" style="position: absolute; top: 350px; left: 417px; transform: translate(-50%, -50%);">
                 <img v-else src="../assets/images/hud/oil_red.svg" alt="Oil"  style="position: absolute; top: 350px; left: 417px; transform: translate(-50%, -50%);">
         
             
        
            </div>
        </div>
            <div class="info vehicle others">
                <div class="col-md-12">
                        <div class="icon" v-if="maxfuel > 0">
                            <i class="fas fa-gas-pump" style="color:#3F6791;text-shadow: 0 0 2px #000;"><span
                                    class="ml-3"
                                    style="font-family: 'Exo', sans-serif;color:white">{{ setfuel }}%</span></i>
                        </div>
                        <div class="icon" v-if="maxfuel <= 0">
                            <i class="fas fa-gas-pump" style="color:#3F6791;text-shadow: 0 0 2px #000;"><span
                                    class="ml-3" style="font-family: 'Exo', sans-serif;color:white">/</span></i>
                        </div>
                    </div>
                </div>
            </div>

             <div  v-if="showhud4">
          
          
            <div class="row">
             
                <img  class="image-removebg-preview-1-1" src="../assets/images/inventory/Faust.png"
                    :class="[(actualWeapon == 'faust') ? 'weaponimg1 mr-3' : 'weaponimg2 mr-3']">
                <img v-for="(weapon, index) in weapons" :key="index" :src="getImgUrl(weapon.description)"
                    :class="[(actualWeapon == weapon.description.toLowerCase()) ? [(IsMelee(weapon.description.toLowerCase())) ? 'weaponimg3 mr-3' : 'weaponimg1 mr-3'] : [(IsMelee(weapon.description.toLowerCase())) ? 'weaponimg4 mr-3' : 'weaponimg2 mr-3']]">
            </div> </div>
  
        <div v-if="showhud4">
            <div class="weapon2"
                v-if="weapons && weapons.length > 0 && !IsMelee(actualWeapon) && actualWeapon != 'schlagring' && actualWeapon != 'faust' && actualWeapon != 'n/A' && actualAmmo < 5000">
                <span class="weapontext1">{{ actualAmmo }}</span>
            </div>
     
        </div>
        <!------HUD ORIGINS EDITADO BY MIUSTICAT------------>
        <div style="height: 100%; Width: 100%; background-color: transparent;" v-if="showhud2">
            <div class="final-inner">
                <div class="rectangle-container">
                  <div class="group-child12" />
                  <div class="alta-street">ID</div>
                  <div class="div16"> {{ id }}</div>
                </div>
              </div>
             <div class="doa-artworks">
                        <span class="doa">GTA </span>
                        <b class="artworks">ORIGINS</b>
                      </div>
                      <div class="civilian-doa-container">
                        <span>Version - </span>
                        <span class="doa-toprak">1.1</span>
                      </div>
                      <div class="div1"> {{ time }}</div>
                      <div class="div2"> 18-06-2024 </div>
     
                <div class="group-parent2">
                    <div  v-if="voicerp == 1 || voicerp == 2">
                        <img class="group-child8" v-if="voicerp == 1 && talkstate == 0" src="../assets/images/hud/microfono.svg" >
                        <img class="group-child8" v-if="(voicerp == 1 && talkstate == 1)" src="../assets/images/hud/microfonoazul.svg" >
                        <img class="group-child8" v-if="(voicerp == 1 && (talkstate == 2 || talkstate == -1 || talkstate == -2))" src="../assets/images/hud/microfono.svg" >
                        <img class="group-child8" v-if="(voicerp == 2 && talkstate2 == 1)" src="../assets/images/hud/microfonoazul.svg" >
                        <img class="group-child8" v-if="(voicerp == 2 && talkstate2 >= 2)" src="../assets/images/hud/microfonoverde.svg" >
                        <img class="group-child8" v-if="(voicerp == 2 && talkstate2 == 0)" src="../assets/images/hud/microfono.svg" >
                    </div>
                </div>
                
    
            <!--------- FIn-->
            <div class="crosshair" v-if="crosshairshow && crosshair > 0">
                <img :src="getCrosshair(crosshair)" alt="Crosshair">
            </div>
        </div>
        <div v-if="infomessage && showhud4" class="text-center"
            style="width: 42vw;max-height:3.55vw;background-color: rgba(0, 0, 0, 0.5);border-radius: 0.5vw;margin-top:-0.6vw;margin-left:30vw;text-shadow: 0 0 0.3px #000">
            <div
                style="display: flex; justify-content: center; align-items: center;margin-top:-0.5vw;font-family: 'Exo', sans-serif;">
                <span style="margin-top:0.4vw;color:white;font-size:1vw"><span style="color:#3F6791">Info:</span>
                    {{ infomessage }}</span>
            </div>
        </div>
        <!----
        <div style="height: 100%; Width: 100%; background-color: transparent;" v-if="showhud3">
            <div class="leftinfo">
                <i class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000;margin-top:4.65vw"><span
                        class="ml-2 text-center" style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.2vw;margin-top: 0.15vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-bars float-left"></i><span
                            style="margin-left: 1vw;font-size:0.75vw">[F2]</span></span></i>
                <i class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000"><span class="ml-2 text-center"
                        style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.2vw;margin-top: 0.15vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-mobile-screen float-left"></i><span
                            style="margin-left: 1.1vw;font-size:0.75vw">[F5]</span></span></i>
                <i class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000"><span class="ml-2 text-center"
                        style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.2vw;margin-top: 0.15vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-hand-dots float-left"></i><span
                            style="margin-left: 1.05vw;font-size:0.75vw">[X]</span></span></i>
                <i class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000"><span class="ml-2 text-center"
                        style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.2vw;margin-top: 0.15vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-user-pen float-left"></i><span
                            style="margin-left: 0.9vw;font-size:0.75vw">[I]</span></span></i>
                <i v-if="voicerp == 1" class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000"><span
                        class="ml-2 text-center" style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.2vw;margin-top: 0.15vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-microphone-lines float-left"></i><span
                            style="margin-left: 1.32vw;font-size:0.75vw">[^]</span></span></i>
                <i class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000"><span class="ml-2 text-center"
                        style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.2vw;margin-top: 0.16vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-fingerprint float-left"></i><span
                            style="margin-left: 1.02vw;font-size:0.75vw">[F]</span></span></i>
                <i class="textstyle" style="color:#3F6791;text-shadow: 0 0 2px #000"><span class="ml-2 text-center"
                        style="font-family: 'Exo', sans-serif;color:white"><i
                            style="font-size: 0.9vw; margin-left: 1.525vw;margin-top: 0.16vw;text-shadow: 0 0 2px #000;color:#3F6791"
                            class="fa-solid fa-solid fa-arrow-pointer float-left"></i><span
                            style="margin-left: 0.64vw;font-size:0.75vw">[F10]</span></span></i>
            </div>
        </div>
        -->
    </div>
</template>

<script>
    import Vue from 'vue'
    import VueEllipseProgress from 'vue-ellipse-progress';
    Vue.use(VueEllipseProgress);
    export default {
        name: 'Speedometer',
        data: function() {
            return {
                voicerp: 1,
                crosshairshow: false,
                crosshair: 0,
                speedometershow: false,
                showhud2: false,
                showhud3: false,
                showhud4: false,
                checkspeedo: false,
                speedProgress: 0,
                speed: 0,
                speed2: 0,
                health: 100,
                fuel: 100,
                oel: 100,
                battery: 100,
                maxfuel: 100,
                setfuel: 100,
                setBattery: 100,
                maxSpeed: 490,
                locked: 2,
                belt: 1,
                vehiclengine: 0,
                id: 0,
                ort: 'Ort',
                time: '00:00',
                windowHeight: window.innerHeight,
                windowWidth: window.innerWidth,
                talkstate: -1,
                talkstate2: 0,
                infomessage: '',
                infotimeout: null,
                weapons: [],
                actualWeapon: '',
                actualAmmo: 0
            }
        },
        watch: {
            windowHeight: function() {
                this.$forceUpdate();
            },
        },
        mounted() {
            this.$nextTick(() => {
                window.addEventListener('resize', this.onResize);
            })
        },
        beforeDestroy() {
            window.removeEventListener('resize', this.onResize);
        },
        methods: {
            getImgUrl(pic) {
                return require('../assets/images/inventory/' + pic + '.png')
            },
            setvoicerp: function(voicerp) {
                this.voicerp = voicerp;
            },
            updateWeaponList: function(weapons, actualWeapon, actualAmmo) {
                this.weapons = JSON.parse(weapons);
                if (this.weapons) {
                    this.weapons = this.weapons.filter(weapon => weapon.type == 5 && weapon.props.split(',')[1] ==
                        1 && !weapon.description.includes("Schutzweste"));
                }
                this.actualWeapon = actualWeapon;
                this.actualAmmo = actualAmmo;
            },
            IsMelee: function(itemname) {
                switch (itemname.toLowerCase()) {
                    case "dolch": {
                        return 1;
                    }
                    case "baseballschläger": {
                        return 1;
                    }
                    case "brechstange": {
                        return 1;
                    }
                    case "taschenlampe": {
                        return 1;
                    }
                    case "golfschläger": {
                        return 1;
                    }
                    case "axt": {
                        return 1;
                    }
                    case "messer": {
                        return 1;
                    }
                    case "machete": {
                        return 1;
                    }
                    case "klappmesser": {
                        return 1;
                    }
                    case "schlagstock": {
                        return 1;
                    }
                    case "poolcue": {
                        return 1;
                    }
                }
                return 0;
            },
            showCrosshair: function(crosshair) {
                this.crosshair = crosshair;
                this.crosshairshow = true;
            },
            hideCrosshair: function() {
                this.crosshairshow = false;
            },
            getCrosshair(crosshair) {
                return require('../assets/images/crosshair/' + crosshair + '.png')
            },
            setInfomessage: function(info, time) {
                if (this.infotimeout != null) {
                    clearTimeout(this.infotimeout);
                }
                this.infomessage = info;
                var self = this;
                this.infotimeout = setTimeout(function() {
                    self.infomessage = '';
                    self.infotimeout = null;
                }, time);
            },
            setTalkState(settalkstate) {
                this.talkstate = settalkstate;
            },
            setTalkState2(settalkstate2) {
                this.talkstate2 = settalkstate2;
            },
            onResize() {
                this.windowHeight = window.innerHeight
                this.windowWidth = window.innerWidth
            },
            showHud2: function(id, ort) {
                this.id = id;
                var replacedort = ort;
                if (this.windowWidth <= 850) {
                    if (ort.length >= 8) {
                        replacedort = ort.substring(0, 7);
                        replacedort = replacedort + '.';
                    }
                } else {
                    if (ort.length >= 21) {
                        replacedort = ort.substring(0, 20);
                        replacedort = replacedort + '.';
                    }
                }
                this.ort = replacedort;
                var a = new Date();
                var b = a.getHours();
                var c = a.getMinutes();
                if (b < 10) b = '0' + b;
                if (c < 10) c = '0' + c;
                var zeit = b + ':' + c;
                this.time = zeit;
                this.showhud2 = !this.showhud2;
                this.showhud3 = !this.showhud3;
                this.showhud4 = !this.showhud4;
                if (this.speedometershow == true) {
                    this.checkspeedo = true;
                    this.speedometershow = false;
                } else {
                    if (this.checkspeedo == true) {
                        this.checkspeedo = false;
                        this.speedometershow = true;
                    }
                }
            },
            hideHud: function() {
                this.showhud2 = false;
                this.showhud3 = false;
                this.showhud4 = false;
                this.speedometershow = false;
                this.checkspeedo = false;
            },
            reloadHud: function() {
                var oldspeedoShow = this.speedometershow;
                this.showhud2 = false;
                this.showhud3 = false;
                this.showhud4 = false;
                this.speedometershow = false;
                var self = this;
                setTimeout(function() {
                    self.showhud2 = true;
                    self.showhud3 = true;
                    self.showhud4 = true;
                    self.speedometershow = oldspeedoShow;
                    self.$forceUpdate();
                }, 555);
            },
            updateHud3: function() {
                this.showhud3 = !this.showhud3;
                this.showhud4 = !this.showhud4;
            },
            updateHud2: function(ort) {
                var replacedort = ort;
                if (this.windowWidth <= 850) {
                    if (ort.length >= 8) {
                        replacedort = ort.substring(0, 7);
                        replacedort = replacedort + '.';
                    }
                } else {
                    if (ort.length >= 21) {
                        replacedort = ort.substring(0, 20);
                        replacedort = replacedort + '.';
                    }
                }
                this.ort = replacedort;
                var a = new Date();
                var b = a.getHours();
                var c = a.getMinutes();
                if (b < 10) b = '0' + b;
                if (c < 10) c = '0' + c;
                var zeit = b + ':' + c;
                this.time = zeit;
            },
            showSpeedometer: function(maxspeed) {
                this.speed = 0;
                this.speedProgress = 0;
                this.speedometershow = !this.speedometershow;
                this.maxspeed = (maxspeed - 2);
            },
            updateMaxSpeed: function(maxspeed) {
                this.maxspeed = (maxspeed - 2);
            },
            updateSpeedometerSpeed: function(speed, health, locked, engine, belt, fuel, maxfuel, battery, oel) {
                speed = parseInt(speed);
                health = parseInt(health);
                if (speed < 0) {
                    speed = 0;
                }
                this.speed2 = speed;
                if (speed > this.maxspeed) {
                    speed = parseInt(this.maxspeed);
                }
                this.speed = speed;
                this.speedProgress = parseInt((100 / this.maxspeed) * speed);
                this.health = parseInt(100 / 1000 * health);
                this.locked = locked;
                this.vehiclengine = parseInt(engine);
                this.belt = parseInt(belt);
                this.fuel = Math.ceil(fuel);
                this.oel = parseInt(oel);
                this.battery = parseInt(battery);
                this.maxfuel = parseInt(maxfuel);
                if (this.maxfuel > 0) {
                    this.setfuel = parseInt((this.fuel * 100) / this.maxfuel);
                } else {
                    this.setfuel = 0;
                }
                if (this.battery > 0) {
                    this.setbattery = parseInt((this.battery * 100) / 100);
                } else {
                    this.setbattery = 0;
                }
            },
        }
    }
</script>

<style scoped>
html,
body,
template,
* {
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -o-user-select: none;
    user-select: none;

      /* fonts */
  --font-poppins: Poppins;
  --font-open-sans: "Open Sans";

  /* font sizes */
  --font-size-sm: 14px;
  --font-size-smi: 13px;
  --font-size-45xl: 64px;
  --font-size-mini-5: 14.5px;
  --font-size-11xl-2: 30.2px;
  --font-size-2xl: 21px;

  /* Colors */
  --color-white: #fff;
  --color-crimson-100: #f80b53;
  --color-crimson-200: #f80b52;
  --color-silver-100: #c8c8c8;

  /* Border radiuses */
  --br-8xs: 5px;
}

.rectangle-parent {
    position: absolute;
    top: 492px;
    left: 1740px;
    width: 334px;
    height: 37px;
    text-align: center;
    font-size: 16.2px;
    color: #c4c4c4;
  }
  .final-item {
    position: absolute;
    top: 757px;
    left: 22px;
    width: 365px;
    height: 229px;
    object-fit: cover;
  }
  .doa {
    font-weight: 600;
  }
  .artworks {
    color: #f80b53;
  }
  .span {
    color: #a0a0a0;
  }
  
  .ellipse-div {
    position: absolute;
    top: 7px;
    left: 128px;
    box-shadow: 0px 0px 15px #f00b50;
    border-radius: 50%;
    background: linear-gradient(122.91deg, #f80b52 4.44%, rgba(248, 11, 82, 0));
    width: 24px;
    height: 24px;
  }
  .doa-artworks {
    position: absolute;
    top: 46px;
    left: 1785px;
    font-size: 16px;
    color: white;
    z-index: -1;
  }
  .doa-toprak {
    color: white;
  }
  .civilian-doa-container {
    position: absolute;
    top: 73px;
    left: 1813px;
    font-size: var(--font-size-smi);
    font-weight: 600;
    color: #f80b53;
    z-index: -1;
  }
  .div1 {
    position: absolute;
    top: 99px;
    left: 1853px;
    font-size: var(--font-size-smi);
    font-weight: 600;
    color: white;
    z-index: -1;
  }
  .div2 {
    position: absolute;
    top: 99px;
    left: 1790px;
    font-size: var(--font-size-smi);
    font-weight: 600;
    color: white;
    z-index: -1;
  }
  .vector-icon1 {
    position: absolute;
    height: 1.2%;
    width: 0.68%;
    top: 9.44%;
    right: 1.56%;
    bottom: 89.35%;
    left: 97.76%;
    max-width: 100%;
    overflow: hidden;
    max-height: 100%;
  }
  .vector-icon2 {
    position: absolute;
    height: 1.38%;
    width: 0.68%;
    top: 9.44%;
    right: 4.9%;
    bottom: 89.18%;
    left: 94.43%;
    max-width: 100%;
    overflow: hidden;
    max-height: 100%;
  }

.weaponimg1 {
    height: 2.75vh;
}

.weaponimg2 {
    height: 2.75vh;
    opacity: 0.5;
}

.weaponimg3 {
    height: 2.75vh;
    width: 11.5vh;
}

.weaponimg4 {
    height: 2.75vh;
    width: 11.5vh;
    opacity: 0.5;
}

.weapontext1 {
    font-family: 'Exo', sans-serif;
    z-index: -1;
    text-shadow: 1px 0 0 #000, 0 -1px 0 #000, 0 1px 0 #000, -1px 0 0 #000;
    font-size: 1.015vw;
    color: #689149;
}

.bordericon {
    display: inline-block;
    border-radius: 5vw;
    color: rgba(0, 0, 0, 0.5);
    background-color: rgba(0, 0, 0, 0.5);
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
    padding: 0.5em 0.6em;
}

.kmhtext {
    color: white;
    font-size: 29.5px;
    font-family: 'Exo', sans-serif;
    margin-top: -1.3em;
    text-shadow: 0 0 9px #000;
    text-align: center;
}

.icon {
    font-size: 1.75vh;
    display: block;
    position: relative;
    padding: 0.03vh 1vh;
    margin: 10px 3px 0 5px;
    width: 11.1vh;
    max-width: 11.2;
    height: 2.6vh;
    max-height: 2.7vh;
    border-radius: 10px;
    overflow: hidden;
    background: rgba(0, 0, 0, 0.5);
    text-align: center;
}

.info.vehicle {
    margin: 0;
    position: absolute;
    bottom: 0;
    left: 50%;
    margin-right: -50%;
    transform: translate(-50%, 27%);
    z-index: 3;
    text-align: center;
}

@media (max-height: 900px) {
    .info.vehicle {
        margin: 0;
        position: absolute;
        bottom: 0;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, 25%);
        z-index: 3;
        text-align: center;
    }

    .kmhtext {
        color: white;
        font-size: 17px;
        font-family: 'Exo', sans-serif;
        margin-top: -0.6em;
        text-shadow: 0 0 9px #000;
        text-align: center;
    }

    .icon {
        font-size: 1.75vh;
        display: block;
        position: relative;
        padding: 0.13vh 1vh;
        margin: 10px 3px 0 5px;
        width: 11.1vh;
        max-width: 11.2;
        height: 2.6vh;
        max-height: 2.7vh;
        border-radius: 10px;
        overflow: hidden;
        background: rgba(0, 0, 0, 0.5);
        text-align: center;
    }
}

@media (min-width: 1070px) {
    .info.vehicle {
        margin: 0;
        position: absolute;
        bottom: 0;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, 25%);
        z-index: -1;
        text-align: center;
    }

    .kmhtext {
        color: white;
        font-size: 29.5px;
        font-family: 'Exo', sans-serif;
        margin-top: -1.3em;
        text-shadow: 0 0 9px #000;
        text-align: center;
    }
}

@media (max-height: 720px) and (max-width: 1280px) {
    .info.vehicle {
        margin: 0;
        position: absolute;
        bottom: 0;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, 23%);
        z-index: -1;
        text-align: center;
    }

    .kmhtext {
        color: white;
        font-size: 15.5px;
        font-family: 'Exo', sans-serif;
        margin-top: -0.8em;
        text-shadow: 0 0 9px #000;
        text-align: center;
    }
}

@media (min-width: 2600px) {
    .info.vehicle {
        margin: 0;
        position: absolute;
        bottom: 0;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, 24%);
        z-index: -1;
        text-align: center;
    }

    .kmhtext {
        color: white;
        font-size: 45px;
        font-family: 'Exo', sans-serif;
        margin-top: -1.8em;
        text-shadow: 0 0 9px #000;
        text-align: center;
    }
}

.info.vehicle.others {
    position: absolute;
    transform: translate(-50%, -5%);
    padding-top: 5%;
    z-index: -1;
    text-align: center;
}

.info.server.others {
    margin: 0;
    position: absolute;
    top: 0.2vh;
    left: 50%;
    margin-bottom: 0.5%;
    transform: translate(-50%, -18%);
    z-index: -1;
    text-align: center;
}

.icon2 {
    font-size: 1.5vh;
    display: block;
    position: relative;
    padding: 0.18vh 1.7vh;
    margin: 10px 0.5px 0 5px;
    width: 12.3vh;
    max-width: 12.4vh;
    height: 2.6vh;
    max-height: 2.7vh;
    border-radius: 10px;
    overflow: hidden;
    background: rgba(0, 0, 0, 0.5);
    text-align: center;
}

@media (max-height: 803px) {
    .icon2 {
        font-size: 1.5vh;
        display: block;
        position: relative;
        padding: 0.165vh 2.0vh;
        margin: 10px 0.5px 0 5px;
        width: 14.1vh;
        max-width: 14.2vh;
        height: 2.6vh;
        max-height: 2.7vh;
        border-radius: 10px;
        overflow: hidden;
        background: rgba(0, 0, 0, 0.5);
        text-align: center;
    }
}

.icon3 {
    font-size: 1.15vh;
    display: block;
    position: relative;
    padding: 0.32vh 0.3vh;
    margin: 0.6vh 0.15vh 0.3vh 0.25vh;
    width: 16vh;
    height: 2.25vh;
    border-radius: 10px;
    overflow: hidden;
    background: rgba(0, 0, 0, 0.5);
    text-align: center;
}

@media (max-width: 1635px) {
    .icon3 {
        font-size: 1.15vh;
        display: block;
        position: relative;
        padding: 0.3vh 7px;
        margin: 0.6vh 0.15vh 0.3vh 0.25vh;
        width: 16vh;
        height: 2.25vh;
        border-radius: 10px;
        overflow: hidden;
        background: rgba(0, 0, 0, 0.5);
        text-align: center;
    }
}

@media (max-width: 1165px) {
    .icon3 {
        font-size: 1.15vh;
        display: block;
        position: relative;
        padding: 0.24vh 7px;
        margin: 0.6vh 0.15vh 0.3vh 0.25vh;
        width: 16vh;
        height: 2.15vh;
        border-radius: 10px;
        overflow: hidden;
        background: rgba(0, 0, 0, 0.5);
        text-align: center;
    }

    .iconnw {
        display: none;
    }
}

@media (max-width: 800px) {
    .icon3 {
        font-size: 1.15vh;
        display: block;
        position: relative;
        padding: 0.30vh 7px;
        margin: 0.6vh 0.15vh 0.3vh 0.25vh;
        width: 16vh;
        height: 2.15vh;
        border-radius: 10px;
        overflow: hidden;
        background: rgba(0, 0, 0, 0.5);
        text-align: center;
    }

    .iconnw {
        display: none;
    }
}

@media (max-height: 1024px) and (max-width: 1280px) {
    .info.vehicle {
        margin: 0;
        position: absolute;
        bottom: 0;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, 25%);
        z-index: -1;
        text-align: center;
    }

    .icon3 {
        font-size: 1.15vh;
        display: block;
        position: relative;
        padding: 0.3vh 7px;
        margin: 0.9vh 0.15vh 0.3vh 0.25vh;
        width: 16vh;
        height: 2.25vh;
        border-radius: 10px;
        overflow: hidden;
        background: rgba(0, 0, 0, 0.5);
        text-align: center;
    }

    .iconnw2 {
        display: none;
    }
}

@media (max-height: 768px) and (max-width: 1366px) {
    .kmhtext {
        color: white;
        font-size: 17.5px;
        font-family: 'Exo', sans-serif;
        margin-top: -0.7em;
        text-shadow: 0 0 9px #000;
        text-align: center;
    }
}

.leftinfo {
    margin: 0;
    position: absolute;
    top: 21.5%;
    right: 0.5vw;
    margin-bottom: 0.5%;
    transform: translate(-1%, 21.5%);
    z-index: -1;
    text-align: left;
}

.textstyle {
    background-color: rgba(0, 0, 0, 0.5);
    font-weight: bold;
    border-radius: 2vw;
    width: 6vw;
    height: auto;
    font-size: 0.8vw;
    display: block;
    position: relative;
    margin: 1.2vh 0.15vh 0.2vh 0.15vh;
}

@media (max-width: 800px) {
    .textstyle {
        background-color: rgba(0, 0, 0, 0.5);
        font-weight: bold;
        border-radius: 2vw;
        width: 6vw;
        height: auto;
        font-size: 0.8vw;
        display: block;
        position: relative;
        margin: 1.2vh 0.15vh 0.2vh 0.15vh;
        margin-top: 0.45vw;
    }
}

.crosshair {
    position: absolute;
    right: 50%;
    top: 50%;
    transform: translate(50%, -50%);
}

.weapon {
    position: absolute;
    right: 1.3%;
    top: 94%;
    padding-top: 0.5vw;
}

.weapon2 {
    position: absolute;
    right: 0.2%;
    top: 96.5%;
    padding-top: 0.5vw;
}


.group-parent2 {
    position: absolute;
    top: 1014px;
    left: 310px;
    width: 81px;
    height: 81px;

  }
  .group-child8 {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 65px;
    height: 65px;
  }

  .rectangle-container {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 46px;
    height: 20px;
  }
  .final-inner {
    position: absolute;
    top: 21px;
    left: 1844px;
    width: 46px;
    height: 20px;
    font-size: var(--font-size-smi);
    color: #ff0451;
  }
  .final-child1 {
    position: absolute;
    top: 1002.1px;
    left: 386px;
    width: 61.8px;
    height: 61.8px;
    object-fit: contain;
  }
  .final-child2 {
    position: absolute;
    top: 1002px;
    left: 313.1px;
    width: 61.8px;
    height: 61.8px;
    object-fit: contain;
  }

  .group-child12 {
    position: absolute;
    top: 2px;
    left: 16px;
    border-radius: 2px;
    background-color: #000;
    width: 30px;
    height: 15px;
    opacity: 0.6;
  }
  .div16 {
    position: absolute;
    top: 2px;
    left: 22px;
    font-size: 11px;
    color: var(--color-white);
    text-align: center;
    display: inline-block;
    width: 17px;
    height: 15px;
  }
  .alta-street {
    position: absolute;
    top: 0px;
    left: 0px;
    font-weight: 600;
  }
  .hawick-ave {
    position: absolute;
    top: 28px;
    left: 0px;
    font-size: var(--font-size-sm);
    color: var(--color-silver-100);
  }
  .alta-street-parent {
    position: absolute;
    top: 6px;
    left: 624px;
    width: 112px;
    height: 49px;
  }  


  /* INICIO DE LA ZONA DE ARMAS*/

  .vector-icon {
    position: absolute;
    top: 11px;
    left: 24px;
    width: 12px;
    height: 13.1px;
    object-fit: contain;
  }
  .frame-child {
    position: absolute;
    top: -149px;
    left: -84px;
    filter: blur(239px);
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.25);
    width: 187px;
    height: 187px;
  }
  .frame-item {
    position: absolute;
    top: 8px;
    left: -1px;
    border-radius: 1px;
    width: 5px;
    height: 22px;
  }
  .frame-inner {
    position: absolute;
    top: 27.5px;
    left: 154.7px;
    border-radius: 50%;
    background-color: #404040;
    width: 24px;
    height: 24px;
    transform: rotate(165deg);
    transform-origin: 0 0;
  }

  .group-child {
    position: absolute;
    top: 16px;
    left: 100px;
    border-radius: 0.5px;
    background-color: var(--color-crimson-100);
    width: 3px;
    height: 4px;
  }
  .span {
    color: #a0a0a0;
  }
  .div {
    position: absolute;
    top: 8px;
    left: 45px;
    font-weight: 800;
  }

  .r {
    position: absolute;
    top: 14px;
    left: 137px;
    font-weight: 800;
  }

  .ellipse-parent {
    position: absolute;
    top: 0px;
    left: 0px;
    border-radius: var(--br-8xs);
    background-color: rgba(255, 255, 255, 0.01);
    width: 334px;
    height: 37px;
    overflow: hidden;
    font-size: 8.1px;
    color: #7d7d7d;
  }

  .image-1-icon {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 1920px;
    height: 1090px;
    object-fit: cover;
  }
  .black-icon {
    position: absolute;
    top: -2px;
    left: -1px;
    width: 1922px;
    height: 1083px;
  }
  .image-removebg-preview-1-1 {
    position: absolute;
    top: 437px;
    left: 1744px;
    width: 144.8px;
    height: 41px;
    object-fit: contain;
  }
  .final-child {
    position: absolute;
    top: 552px;
    left: 1770px;
    width: 128.4px;
    height: 19.8px;
  }


  /* VELOCIMETRO */

  .group-icon {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 540.2px;
    height: 540.2px;
    object-fit: contain;
  }
  .div10 {
    position: absolute;
    top: 216px;
    left: 218px;
    font-weight: 500;
    color: #515151;
  }
  .div11 {
    position: absolute;
    top: 216px;
    left: 259px;
    font-weight: 500;
    text-shadow: 0px 0px 26px #ff0451;
  }
  .kmh {
    position: absolute;
    top: 291px;
    left: 240px;
    font-size: 22px;
    font-weight: 500;
    text-align: left;
    text-shadow: 0px 0px 26px #ff0451;
  }
  .group-container {
    position: absolute;
    top: 550px;
    left: 1410px;
    width: 460.2px;
    height: 540.2px;
    text-align: center;
    font-size: var(--font-size-45xl);
    color: var(--color-crimson-200);
  }

  .originsall{
    position: absolute;
    top: -180px;
 
  }
</style>
