<template>
  <div class="registershow" style="overflow: hidden" v-if="registershow">
    <audio ref="audio" src="../assets/sound-track/origins-track.mp3" loop></audio>
    <div class="final">
      <video ref="video" class="background-video" src="../assets/origins-oficial/bc-logino.mp4" autoplay muted loop></video>
      <img ref="movableImage" class="rectangle-icon" loading="lazy" alt="" src="../assets/images/login/origins.png" @mousemove="handleMouseMove" />
      <div class="final-child"></div>
      <div class="final-item"></div>
      <div class="frame-parent">
        <div class="rectangle-wrapper">
          <div class="frame-child"></div>
        </div>
      </div>
      <!-- INPUT - FORMULARIO DE REGISTRO-->
      <div class="frame-group">
        <div class="rectangle-container"></div>
        <div class="frame-container">
          <div class="input-container">
            <img class="frame-child1" loading="lazy" alt="" src="../assets/images/login/originslogo.png" />
            <div class="warning" v-if="warning">{{ warning }}</div>
            <input class="input-field" id="name" name="name" v-model="username" placeholder="Nombre de usuario" maxlength="35" autocomplete="off" v-on:keyup.enter="onEnter" autofocus>
            <input class="input-field" type="password" name="password" id="password" v-model="password" placeholder="Contraseña" maxlength="35" autocomplete="off" v-on:keyup.enter="onEnter">
            <input class="input-field" type="password" name="password2" id="password2" v-model="password2" placeholder="Confirmar contraseña" maxlength="35" autocomplete="off" v-on:keyup.enter="onEnter">
       
          </div>
          <!-- BOTONES-->
          <div class="frame-wrapper">
            <div class="frame-div" v-if="!clicked">
              <div class="iniciar-sesin-wrapper">
                <div class="iniciar-sesin" @click="register">REGISTRARSE</div>
              </div>
              <div class="no-tienes-una-container" @click="showLogin()">
                <p class="no-tienes-una">Iniciar sesión</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RegisterWindow',
  data: function () {
    return {
      registershow: false,
      username: '',
      password: '',
      password2: '',
      warning: '',
      clicked: false
    }
  },
  methods: {
    handleMouseMove(event) {
      const image = this.$refs.movableImage;
      const x = (event.clientX / window.innerWidth) - 0.5;
      const y = (event.clientY / window.innerHeight) - 0.5;

      const moveX = x * 45; // valores para cambiar la intensidad del movimiento
      const moveY = y * 45;

      image.style.transform = `translate(${moveX}px, ${moveY}px)`;
    },
    onEnter: function () {
      this.register();
    },
    register: function () {
      this.warning = '';

      if (this.password.length < 6 || this.username.length < 3) {
        this.warning = '¡Nombre o contraseña demasiado cortos!';
      } else if (this.password.length > 35 || this.username.length > 35) {
        this.warning = '¡Nombre o contraseña demasiado largos!';
      } else if (this.password !== this.password2) {
        this.warning = '¡Las contraseñas no coinciden!';
      } else {
        // eslint-disable-next-line no-undef
        mp.trigger('Client:AccountRegister', this.username, this.password);
        return;
      }
        // Ocultar el mensaje de advertencia después de 2 segundos 
        setTimeout(() => {
        this.warning = '';
      }, 2000);
    },
    showRegister: function () {
      this.registershow = !this.registershow;
    },
    showLogin: function () {
      this.registershow = !this.registershow;
      mp.trigger('Client:ShowLogin');
    },
    setWarning: function (text) {
      this.warning = text;
      this.clicked = false;
    }
  }
}
</script>


<style scoped>
@import '../assets/css/bootstrap.min.css';
@import '../assets/css/main.css';
@import '../assets/css/util.css';
@import '../assets/css/font-awesome.min.css';
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");

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

  /* Colors */
  --origins2: #fff;

  /* Paddings */
  --padding-27xl: 46px;


}

.origins-3-1 {
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  
}
.image-1-icon {
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: none;
}
.image-2-icon {
  position: absolute;
  top: -2px;
  left: -1px;
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: none;
}
.image-3-icon {
  position: absolute;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: none;
}
.final-child {
  position: absolute;
  top: 0px;
  left: 1326px;
  border-top: 1px solid var(--origins2);
  box-sizing: border-box;
  width: 145px;
  height: 1px;
}
.final-item {
  position: absolute;
  top: 1080px;
  left: 1128px;
  border-top: 1px solid var(--origins2);
  box-sizing: border-box;
  width: 148px;
  height: 1px;
}
.frame-child {
  align-self: stretch;
  height: 42px;
  position: relative;
  z-index: 1;
}
.rectangle-wrapper {
  width: 99px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  padding: 169px 0px 0px;
  box-sizing: border-box;
}
.frame-parent {
  position: absolute;
  top: 0px;
  left: 814px;
  width: 1074px;
  height: 1080px;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: flex-start;
  padding: 0px 0px 869px;
  box-sizing: border-box;
  gap: 114px;
  max-width: 100%;
}
.rectangle-container {
  align-self: stretch;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: flex-start;
  padding: 0px var(--padding-27xl);
}
.frame-item {
  align-self: stretch;
  flex: 1;
  position: relative;
  max-width: 100%;
  overflow: hidden;
  max-height: 100%;
  z-index: 1;
}
.frame-inner {
  align-self: stretch;
  flex: 1;
  position: relative;
  max-width: 100%;
  overflow: hidden;
  max-height: 100%;
  z-index: 1;
}
.vector-parent {
  align-self: stretch;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  gap: 28px;
}
.iniciar-sesin {
  position: relative;
  font-weight: 600;
  text-shadow: 1px 0 0 #000, 0 1px 0 #000, -1px 0 0 #000, 0 -1px 0 #000;
  z-index: 1;
}

.iniciar-sesin:hover{
  opacity: 0.4;
}
.iniciar-sesin-wrapper {
  align-self: stretch;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: flex-start;
  padding: 0px 42px 0px 39px;
}
.no-tienes-una {
  margin: 0;
}
.regstrate-ahora {
  margin: 0;
}
.no-tienes-una-container {
  align-self: stretch;
  position: relative;
  font-size: 19px;
  font-weight: 600;
  text-align: center;
  z-index: 1;
}


.frame-div {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  gap: 30px;
}
.frame-wrapper {
  align-self: stretch;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: flex-end;
  padding: 0px var(--padding-27xl) 0px 48px;
}
.frame-container {
  align-self: stretch;
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: flex-start;
  gap: 56px;
}
.frame-group {
  position: absolute;
  top: 120px;
  left: 382px;
  width: 325px;
  height: 610px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  gap: 59px;
  z-index: 2;
}
.final {
  background-color: var(--origins2);
  overflow: hidden;
  line-height: normal;
  letter-spacing: normal;
  text-align: left;
  font-size: 20px;
  color: var(--origins2);
  font-family: var(--font-poppins);
}

@media screen and (max-width: 450px) {
  .iniciar-sesin {
    font-size: 16px;
  }
}

.rectangle-icon {
  opacity: 0.9;
width: 55%;
  flex: 1;
  right: -900px;
  top: 101px;
  position: relative;
  max-width: calc(100% - 213px);
  overflow: hidden;
  object-fit: cover;
  z-index: 1;
}

.frame-child1 {
  top: -40px;
  left: 71px;
 text-align: center;
  flex: 1;
  position: relative;
  max-width: 60%;
  overflow: hidden;
  object-fit: cover;
  z-index: 1;
}

/* ESTILO DE LOS INPUT */
.input-container {
  display: flex;
  flex-direction: column;
}

.input-field {
  width: 325px;
  height: 58px;
  margin-bottom: 40px;
  background-color: rgba(0, 0, 0, 0.25); /* Color negro con 25% de opacidad */
  border: 46% solid #D13B95;
  box-sizing: border-box; 
  color: #FFFFFF; /* Texto blanco para que sea legible sobre el fondo negro */
  padding: 10px; /* Espaciado interior para el texto */
  text-align: center;
}

.input-field:last-child {
  margin-bottom: 0; /* Elimina el margen inferior del último input */
}

.background-video {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1;
}

@keyframes neon-blink {
  0%, 100% {
    box-shadow: 0 0 5px rgba(255, 0, 255, 0.5);
  }
  50% {
    box-shadow: 0 0 10px rgba(255, 0, 255, 0.5);
  }
}

.input-field {
  border: 2px solid transparent;
  padding: 10px;
  font-size: 16px;
  outline: none;
  background-color: #000000a9;
  color: #fff; 
  animation: neon-blink 1s infinite;
  transition: box-shadow 0.3s ease-in-out;
}

.input-field::placeholder {
  color: #fff;
}

/* BOTONES */

.custom-button {
  background-color: #4CAF50; /* Color de fondo */
  color: white; /* Color del texto */
  padding: 10px 20px; /* Espacio alrededor del texto */
  border: none; /* Sin borde */
  border-radius: 5px; /* Bordes redondeados */
  cursor: pointer; /* Cursor de puntero */
  font-size: 16px; /* Tamaño del texto */
}

.custom-button:hover {
  background-color: #45a049; /* Color de fondo más oscuro al pasar el mouse */
}

/* Estilos adicionales */
.frame-wrapper {
  margin-top: 20px;
}

.no-tienes-una-container {
  margin-top: 10px;
}

.no-tienes-una, .regstrate-ahora {
  color: #fff;
  cursor: pointer;
}

.no-tienes-una:hover, .regstrate-ahora:hover {
  text-decoration: underline;
}


.audio-container {
  position: relative;
  z-index: -1; /* Coloca el audio detrás de otros elementos */
}


/* TEXTO DE FONDO */

.neon-text {
  z-index: 2;
  color: #ff00ff; /* rosa oscuro */
  font-family: 'Arial', sans-serif; /* ajusta la fuente según necesites */
  font-size: 48px; /* ajusta el tamaño de fuente según necesites */
  text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 30px #ff00ff, 0 0 40px #ff00ff, 0 0 70px #ff00ff, 0 0 80px #ff00ff, 0 0 100px #ff00ff, 0 0 150px #ff00ff; /* efecto neon */
  animation: neon-flicker 1.5s infinite alternate; /* animación de parpadeo */
}

@keyframes neon-flicker {
  from {
    text-shadow: 0 0 10px #ff00ff, 0 0 20px #ff00ff, 0 0 30px #ff00ff, 0 0 40px #ff00ff, 0 0 70px #ff00ff, 0 0 80px #ff00ff, 0 0 100px #ff00ff, 0 0 150px #ff00ff; /* efecto neon */
  }
  to {
    text-shadow: none; /* quita el efecto neon */
  }
}

.warning {
  text-align: center;
 font-size: 15px;
}


</style>


