<template>
    <div class="characterswitch" v-if="charactershow">
        <video ref="video" class="background-video" src="../assets/origins-oficial/bc-char.mp4" autoplay muted loop></video>
      <div class="row justify-content-center centering">
        <div class="card-container">
          <div
            class="card"
            v-for="(character, index) in characters"
            :key="character.id || index"
            :class="{ 'expanded': index === expandedIndex }"
          >
            <div class="card-content" v-if="!character.isSlotAvailable">
              <img
                class="character-image"
                :src="character.Screen"
                alt="Character Image"
              />
              <h2>{{ character.name }}</h2>
              <p>Facción: {{ character.Faction }}</p>
              <p>Dinero en mano: {{ character.Cash }}</p>
              <p>Trabajo: {{ character.Job }}</p>
              <button
                @click="selectCharacter(character.id)"
                type="button"
                class="select-button"
                :disabled="character.Closed === 1"
              >
                Seleccionar
              </button>
            </div>
            <div class="card-content" v-else>
              <h2>Slot disponible</h2>
              <button
                @click="createNewCharacter"
                type="button"
                class="select-button"
              >
                Crear personaje
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Swal from 'sweetalert2';
  
  export default {
    name: 'CharactersWitch',
    data() {
      return {
        expandedIndex: null,
        charactershow: false,
        characters: [
          {
            id: 1,
            name: 'Character 1',
            Faction: 'Faction A',
            Cash: 1000,
            Job: 'Job A',
            Closed: 0,
            isSlotAvailable: false,
          },
          {
            id: null,
            Screen: null,
            name: null,
            Faction: null,
            Cash: null,
            Job: null,
            Closed: 0,
            isSlotAvailable: true,
          },
          {
            id: 3,
            name: 'Character 3',
            Faction: 'Faction C',
            Cash: 3000,
            Job: 'Job C',
            Closed: 0,
            isSlotAvailable: false,
          },
        ],
        count: 3,
        clicked: Date.now() / 1000,
      };
    },
    mounted() {
      document.body.classList.add('dark-mode');
      this.expandCard(0);
    },
    methods: {
      expandCard(index) {
        this.expandedIndex = this.expandedIndex === index ? null : index;
      },
      hideCharacterSwitch() {
        this.charactershow = false;
      },
      showCharacterSwitch(characters, characterscount) {
        this.charactershow = true;
        if (characters !== -1) {
          this.characters = JSON.parse(characters);
          this.count = characterscount;
  
          const allSlotsAvailable = this.characters.every(
            (character) => character.isSlotAvailable
          );
          if (allSlotsAvailable) {
            this.createNewCharacter();
          }
        }
      },
      selectCharacter(characterid) {
        if (Date.now() / 1000 > this.clicked) {
          this.clicked = Date.now() / 1000 + 5;
          // eslint-disable-next-line no-undef
          mp.trigger('Client:SelectCharacter', characterid);
        }
      },
      deleteCharacter(characterid) {
        if (Date.now() / 1000 > this.clicked) {
          Swal.fire({
            title: '¿Realmente quieres eliminar este personaje?',
            showDenyButton: true,
            confirmButtonText: 'Nein',
            denyButtonText: 'Ja',
          }).then((result) => {
            if (result.isDenied) {
              this.clicked = Date.now() / 1000 + 1;
              // eslint-disable-next-line no-undef
              mp.trigger('Client:DeleteCharacter', characterid);
            }
          });
        }
      },
      createNewCharacter() {
        if (Date.now() / 1000 > this.clicked) {
          if (this.count >= 3) {
            Swal.fire({
              icon: 'error',
              title: 'Fehler',
              text: '¡Ya no tienes más espacios libres para personajes!',
            });
            return;
          }
          this.clicked = Date.now() / 1000 + 5;
          // eslint-disable-next-line no-undef
          mp.trigger('Client:CreateNewCharacter');
        }
      },
      characterError() {
        Swal.fire({
          position: 'center',
          icon: 'error',
          title: '¡Interacción no válida!',
          showConfirmButton: false,
          timer: 2500,
        });
      },
    },
  };
  </script>
  
  <style scoped>
  .characterswitch {
    z-index: 1;
    overflow: hidden;
    background-color: transparent;
    scrollbar-width: none;
    position: relative;
  }
  
  .card-container {
    
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    overflow-x: auto;
    padding: 20px;
    gap: 20px;
    max-width: 100%;
  }
  
  .card {
    width: 450px;
    height: 450px;
    transition: all 0.3s ease;
    overflow: hidden;
    position: relative;
    border-radius: 10px;
    animation: neon-blink 1s infinite;
    transition: box-shadow 0.3s ease-in-out;

  }

  @keyframes neon-blink {
    0%, 100% {
      box-shadow: 0 0 5px rgba(255, 0, 255, 0.5);
    }
    50% {
      box-shadow: 0 0 10px rgba(255, 0, 255, 0.5);
    }
  }

  

  
  .character-image {
    width: 100%;
    height: 60%;
    object-fit: cover;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
  }
  
  .card-content {
    width: 450px;
    height: 450px;
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.25); /* Color negro con 25% de opacidad */
    color: white;
    text-align: center;
  }
  
  .card h2 {
    margin-top: 10px;
    font-size: 1.5em;
  }
  
  .card p {
    margin-bottom: 8px;
  }
  
  .select-button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #e91e62a2;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 1em;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .select-button:hover {
    background-color: #e91e63;
  }
  
  .card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4);
  }
  
  .cutimage {
    width: 225px !important;
  }
  
  .centering2 {
    width: 100%;
    height: 100%;
    overflow: hidden;
    scrollbar-width: none;
    margin: auto;
    position: absolute;
    z-index: 1;
  }

  .background-video {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: -1;
  }
  </style>
  