<template>
<div class="inventory">
    <div style="z-index: 1; overflow-x: hidden; overflow-x: hidden; background-color:transparent; scrollbar-width: none;" v-if="inventoryshow1||inventoryshow2">
        <div style="height: 100%; background-color: transparent;">
         
                   <!----- INICIO CODIGO MIUUSTICAT-->
                   <div class="final">
            
                    <img class="final-child" loading="lazy" alt="" src="../assets/images/inv-origins/rectangle-52@2x.png" />
                    <div class="structure">
                    </div>
              <!-- CASILLAS A LA IZQUIERDA 7 ITEMS DE USO RAPIDO PARA EL USUARIO -->

<div class="right-panel">
  <div class="frame-group">
    <div class="content-area-wrapper">
      <div v-for="index in 7" :key="'vertical-item-' + index" class="items-use">
     
      </div>
    </div>
    <!-- INVENTARIO, DERECHA BY MIUSTICAT-->  
                   
    <div class="frame-container">
      <div class="grid-container">
        <!-- Casillas horizontales existentes -->
        <div v-for="(item, index) in inventory1selected" :key="'item-' + index" class="grid-item" :style="{ order: index }" @click="showOptionsMenu(item)">
          <img :src="getImgUrl(item.description)" width="45%" />
        </div>
        <div v-for="index in (30 - inventory1selected.length)" :key="'empty-' + index" class="grid-item"></div>
      </div>
<!-- fin INVENTARIO, DERECHA BY MIUSTICAT-->
                          <img
                            class="frame-child12"
                            loading="lazy"
                            alt=""
                            src="../assets/images/inv-origins/rectangle-51@2x.png"
                          />
                        </div>
                      </div>
                    </div>
                  </div>
        </div>
      </div>
    </div>
</template>

<script>
import Swal from 'sweetalert2/dist/sweetalert2.js'
import draggable from 'vuedraggable'


export default {
    name: 'inventory',
    data() {
        return {
            inventoryshow1: false,
            inventoryshow2: false,
            itemselect1: -1,
            itemselect2: -1,
            inventory1: [],
            inventory1selected: [],
            maxweight1: 25000,
            inventory2: [],
            inventory2selected: [],
            maxweight2: 30000,
            valeur: 0,
            valeur2: 0,
            mouseX: 0,
            mouseY: 0,
            selectedItemId: null,
            clicked: 0,
            showMenu: false
        }
    },
    components: {
        draggable
    },
    mounted() {},
    methods: {
        // Método para verificar si un elemento tiene propiedades adicionales
        hasExtraProps(element) {
            return element.props && element.props.length > 3 && element.type != 5 && element.type != 6;
        },
        // Método para verificar si un elemento es un arma
        hasGunProps(element) {
            return element.props && element.props.length > 2 && element.type == 5 && !this.IsNoMelee(element.description) && element.description != 'Taser';
        },
        // Método para verificar si un elemento es especial
        isSpecialItem(description) {
            const specialItems = ['Dietrich', 'Zigaretten', '55$-Prepaidkarte', 'Handyvertrag', 'Grippofein-C', 'Antibiotika', 'Ibuprofee-400mg', 'Ibuprofee-800mg', 'Morphin-10mg', 'Bandage', 'Materialien', 'Marihuanasamen', 'Marihuana', 'Papes', 'Joint', 'Kokain', 'Kokablatt', 'Kokainsamen', 'Space-Cookies'];
            return specialItems.includes(description);
        },
        // Método para copiar texto al portapapeles
        copyToClipboard(text) {
            const dummy = document.createElement("textarea");
            document.body.appendChild(dummy);
            dummy.value = text;
            dummy.select();
            document.execCommand("copy");
            document.body.removeChild(dummy);
        },
        // Método para obtener la URL de la imagen
        getImgUrl(pic) {
            try {
                return require(`../assets/images/inventory/${pic}.png`);
            } catch (e) {
                return require('../assets/images/inventory/fragezeichen.png');
            }
        },


        onInventoryChange(newOrder) {

          
this.inventory1selected = newOrder;
},
        coverInventory() {
            var self = this;
            //Inventory 1
            self.inventory1selected = [];
            if (self.itemselect1 <= -1) {
                self.inventory1.forEach(function (element) {
                    self.inventory1selected.push(element);
                });
            } else if (self.itemselect1 == 0) {
                self.inventory1.forEach(function (element) {
                    if (element.type == 1 || element.type == 2) {
                        self.inventory1selected.push(element);
                    }
                });
            } else if (self.itemselect1 == 1) {
                self.inventory1.forEach(function (element) {
                    if (element.description.toLowerCase().includes("schlüssel")) {
                        self.inventory1selected.push(element);
                    }
                });
            } else if (self.itemselect1 == 2) {
                self.inventory1.forEach(function (element) {
                    if (element.type == 5 || element.type == 6) {
                        self.inventory1selected.push(element);
                    }
                });
            } else if (self.itemselect1 >= 2) {
                self.inventory1.forEach(function (element) {
                    if ((element.type == 3 || element.type == 4) && !element.description.toLowerCase().includes("schlüssel")) {
                        self.inventory1selected.push(element);
                    }
                });
            }
            //Inventory 2
            self.inventory2selected = [];
            if (self.itemselect2 <= -1) {
                self.inventory2.forEach(function (element) {
                    self.inventory2selected.push(element);
                });
            } else if (self.itemselect2 == 0) {
                self.inventory2.forEach(function (element) {
                    if (element.type == 1 || element.type == 2) {
                        self.inventory2selected.push(element);
                    }
                });
            } else if (self.itemselect2 == 1) {
                self.inventory2.forEach(function (element) {
                    if (element.description.toLowerCase().includes("schlüssel")) {
                        self.inventory2selected.push(element);
                    }
                });
            } else if (self.itemselect2 == 2) {
                self.inventory2.forEach(function (element) {
                    if (element.type == 5 || element.type == 6) {
                        self.inventory2selected.push(element);
                    }
                });
            } else if (self.itemselect2 >= 2) {
                self.inventory2.forEach(function (element) {
                    if ((element.type == 3 || element.type == 4) && !element.description.toLowerCase().includes("schlüssel")) {
                        self.inventory2selected.push(element);
                    }
                });
            }
            self.$forceUpdate();
        },
        selectItems1(select) {
            this.itemselect1 = select;
            this.coverInventory();
        },
        selectItems2(select) {
            this.itemselect2 = select;
            this.coverInventory();
        },
        countweightinventory1() {
            var count = 0.0;
            if (this.inventory1) {
                var value = 0;
                this.inventory1.forEach(function (element) {
                    value = element.props.split(",")[0];
                    if (value > 5000) {
                        value = 0;
                    }
                    if (element.type != 5) {
                        count += (element.weight * element.amount);
                    } else {
                        if (element.description == 'Flaregun') {
                            count += (element.weight + (value * 85));
                        } else {
                            count += (element.weight + (value * 3));
                        }
                    }
                });
            }
            return count;
        },
        countweightinventory2() {
            var count = 0.0;
            if (this.inventory2) {
                this.inventory2.forEach(function (element) {
                    if (element.type != 5) {
                        count += (element.weight * element.amount);
                    } else {
                        if (element.description == 'Flaregun') {
                            count += (element.weight + (element.amount * 85));
                        } else {
                            count += (element.weight + (element.amount * 3));
                        }
                    }
                });
            }
            return count;
        },
        moveItem2(item, from) {
            if ((Date.now() / 1000) > this.clicked) {
                this.moveItem(item, from);
                this.clicked = (Date.now() / 1000) + (3);
            }
        },
        async moveItem(item, from) {
            if (this.inventoryshow2 == true) {
                if (from == 'left') {
                    if (item.amount > 1) {
                        const {
                            value: dropvalue
                        } = await Swal.fire({
                            title: 'Bitte eine Menge angeben!',
                            input: 'text',
                            inputPlaceholder: '1',
                            inputAttributes: {
                                value: 1,
                                maxlength: 4,
                                autocapitalize: 'off',
                                autocorrect: 'off'
                            }
                        })
                        if (!dropvalue) {
                            // eslint-disable-next-line no-undef
                            mp.trigger("Client:UseInventory", "move", item.itemid, 0, "left");
                        } else {
                            // eslint-disable-next-line no-undef
                            mp.trigger("Client:UseInventory", "move", item.itemid, dropvalue, "left");
                        }
                    } else {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "move", item.itemid, 1, "left");
                    }
                } else {
                    if (item.amount > 1) {
                        const {
                            value: dropvalue
                        } = await Swal.fire({
                            title: 'Bitte eine Menge angeben!',
                            input: 'text',
                            inputPlaceholder: '1',
                            inputAttributes: {
                                value: 1,
                                maxlength: 4,
                                autocapitalize: 'off',
                                autocorrect: 'off'
                            }
                        })
                        if (!dropvalue) {
                            // eslint-disable-next-line no-undef
                            mp.trigger("Client:UseInventory", "move", item.itemid, 0, "right");
                        } else {
                            // eslint-disable-next-line no-undef
                            mp.trigger("Client:UseInventory", "move", item.itemid, dropvalue, "right");
                        }
                    } else {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "move", item.itemid, 1, "right");
                    }
                }
            }
        },
        showInventory(json, maxweight, toogle, json2, maxweight2, textinv2) {
            this.clicked = 0;
            this.inventoryshow1 = !this.inventoryshow1;
            if (this.inventoryshow2 == true) {
                this.inventoryshow2 = false;
            }
            if (json2 != null && json2 != 'null') {
                this.inventoryshow2 = !this.inventoryshow2;
            }
            if (!this.inventoryshow1) {
                Swal.close();
            }
            if (toogle) {
                this.inventory1 = JSON.parse(json);
                this.maxweight1 = maxweight;
                if (json2 != null && json2 != 'null') {
                    this.inventory2 = JSON.parse(json2);
                    this.maxweight2 = maxweight2;
                    this.textinv2 = textinv2;
                } else {
                    this.inventory2 = [];
                    this.maxweight2 = 30000;
                    this.textinv2 = '';
                }
                var self = this;
                setTimeout(function () {
                    self.updateProgressbar1();
                    if (json2 != null && json2 != 'null') {
                        self.updateProgressbar2();
                    }
                }, 150);
            }
            this.coverInventory();
        },
        updateInventory(json, json2) {
            if (json) {
                this.inventory1 = JSON.parse(json);
                this.updateProgressbar1();
            } else {
                this.inventory1 = [];
                this.maxweight1 = 25000;
            }
            if (json2) {
                this.inventory2 = JSON.parse(json2);
                this.updateProgressbar2();
            } else {
                this.inventory2 = [];
                this.maxweight2 = 30000;
                this.textinv2 = '';
            }
            this.coverInventory();
        },
     
        showOptionsMenu(item) {
  Swal.fire({
    title: 'Selecciona una opción',
    showCancelButton: true,
    showDenyButton: true,
    showConfirmButton: true,
    confirmButtonText: 'Usar',
    denyButtonText: 'Eliminar',
    cancelButtonText: 'Dar',
    showClass: {
      popup: 'animate__animated animate__fadeInDown'
    },
    hideClass: {
      popup: 'animate__animated animate__fadeOutUp'
    },
    customClass: {
      confirmButton: 'btn btn-success',
      denyButton: 'btn btn-danger',
      cancelButton: 'btn btn-secondary'
    },
    buttonsStyling: false
  }).then(result => {
    if (result.isConfirmed) {
      if (item.type === 6) {
        this.useItem2(item);
      } else if (item.type === 7) {
        Swal.fire({
          title: '¿Equipar arma?',
          icon: 'question',
          showCancelButton: true,
          confirmButtonText: 'Sí',
          cancelButtonText: 'No',
          showClass: {
            popup: 'animate__animated animate__fadeInDown'
          },
          hideClass: {
            popup: 'animate__animated animate__fadeOutUp'
          },
          customClass: {
            confirmButton: 'btn btn-success',
            cancelButton: 'btn btn-secondary'
          },
          buttonsStyling: false
        }).then((result) => {
          if (result.isConfirmed) {
            this.selectGun(item.itemid);
          }
        });
      } else {
        this.useItem(item.itemid);
      }
    } else if (result.isDenied) {
      this.trashItem(item);
    } else if (result.isDismissed && result.dismiss === Swal.DismissReason.cancel) {
      this.giveItem(item);
    }
  });
},

        useItem(itemid) {
            if ((Date.now() / 1000) > this.clicked) {
                this.clicked = (Date.now() / 1000) + (1);
                // eslint-disable-next-line no-undef
                mp.trigger("Client:UseInventory", "use", itemid, 1, "nothing");
            }
        },
        async useItem2(item) {
            if ((Date.now() / 1000) > this.clicked) {
                this.clicked = (Date.now() / 1000) + (1);
                if (item.amount > 1) {
                    const {
                        value: dropvalue
                    } = await Swal.fire({
                        title: 'Bitte eine Menge angeben!',
                        input: 'text',
                        inputPlaceholder: '1',
                        inputAttributes: {
                            value: 1,
                            maxlength: 4,
                            autocapitalize: 'off',
                            autocorrect: 'off'
                        }
                    })
                    if (!dropvalue) {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "use", item.itemid, 0, "nothing");
                    } else {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "use", item.itemid, dropvalue, "nothing");
                    }
                } else {
                    // eslint-disable-next-line no-undef
                    mp.trigger("Client:UseInventory", "use", item.itemid, 1, "nothing");
                }
            }
        },
        selectGun(itemid) {
            if ((Date.now() / 1000) > this.clicked) {
                this.clicked = (Date.now() / 1000) + (1);
                // eslint-disable-next-line no-undef
                mp.trigger("Client:SelectGun", itemid);
            }
        },
        showGun(props) {
            if ((Date.now() / 1000) > this.clicked) {
                this.clicked = (Date.now() / 1000) + (1);
                var ident = props.split(',')[3];
                this.copyToClipboard(ident);
                // eslint-disable-next-line no-undef
                mp.trigger("Client:SendNotificationWithoutButton", 'Waffenidentifikationsnummer: ' + ident + ' (( In die Zwischenablage kopiert! ))', 'info', 'top-left', '4250');
            }
        },
        showContextMenu(event, item) {
    event.preventDefault();
    this.mouseX = event.clientX;
    this.mouseY = event.clientY;
    this.selectedItem = item;
    this.showMenu = true;
  },
  hideContextMenu() {
    this.showMenu = false;
  },
        async trashItem(item) {
            if ((Date.now() / 1000) > this.clicked) {
                this.clicked = (Date.now() / 1000) + (1);
                if (item.amount > 1) {
                    const {
                        value: dropvalue
                    } = await Swal.fire({
                        title: 'Bitte eine Menge angeben!',
                        input: 'text',
                        inputPlaceholder: '1',
                        inputAttributes: {
                            value: 1,
                            maxlength: 4,
                            autocapitalize: 'off',
                            autocorrect: 'off'
                        }
                    })
                    if (!dropvalue) {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "trash", item.itemid, 0, "nothing");
                    } else {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "trash", item.itemid, dropvalue, "nothing");
                    }
                } else {
                    // eslint-disable-next-line no-undef
                    mp.trigger("Client:UseInventory", "trash", item.itemid, 1, "nothing");
                }
            }
        },
        async giveItem(item) {
            if ((Date.now() / 1000) > this.clicked) {
                this.clicked = (Date.now() / 1000) + (1);
                if (item.amount > 1) {
                    const {
                        value: dropvalue
                    } = await Swal.fire({
                        title: 'Bitte eine Menge angeben!',
                        input: 'text',
                        inputPlaceholder: '1',
                        inputAttributes: {
                            value: 1,
                            maxlength: 4,
                            autocapitalize: 'off',
                            autocorrect: 'off'
                        }
                    })
                    if (!dropvalue) {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "give", item.itemid, 0, "nothing");
                    } else {
                        // eslint-disable-next-line no-undef
                        mp.trigger("Client:UseInventory", "give", item.itemid, dropvalue, "nothing");
                    }
                } else {
                    // eslint-disable-next-line no-undef
                    mp.trigger("Client:UseInventory", "give", item.itemid, 1, "nothing");
                }
            }
        },
        IsNoMelee: function (itemname) {
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
                case "schlagring": {
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
                case "feuerlöscher": {
                    return 1;
                }
            }
            return 0;
        },
        updateProgressbar1: function () {
            // eslint-disable-next-line no-undef
            var invweight = this.countweightinventory1();
            if (invweight > 0) {
                this.valeur = ((100 / this.maxweight1) * invweight);
            } else {
                this.valeur = 0;
            }
            // eslint-disable-next-line no-undef
            console.log("updateProgressbar");
            // eslint-disable-next-line no-undef
            $('.progress-bar').css('width', this.valeur + '%').attr('aria-valuenow', this.valeur);
        },
        updateProgressbar2: function () {
            // eslint-disable-next-line no-undef
            var invweight = this.countweightinventory2();
            if (invweight > 0) {
                this.valeur2 = ((100 / this.maxweight2) * invweight);
            } else {
                this.valeur2 = 0;
            }
            // eslint-disable-next-line no-undef
            console.log("updateProgressbar2");
            // eslint-disable-next-line no-undef
            $('.progress-bar2').css('width', this.valeur2 + '%').attr('aria-valuenow', this.valeur2);
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

      /* Colors */
  --color-gray: rgba(11, 11, 11, 0.21);
  --color-silver: #c0b5b5;

  /* Paddings */
  --padding-xl: 20px;
  --padding-12xs: 1px;
  --padding-10xs: 3px;
}
/* INICIO DE CODIGO CSS BY MIUSTICAT*/

.image-1-icon {
    height: 1090px;
    width: 1920px;
    position: relative;
    object-fit: cover;
    display: none;
    max-width: 100%;
  }
  .image-2-icon {
    height: 1083px;
    width: 1921px;
    position: relative;
    object-fit: cover;
    display: none;
    max-width: 100%;
  }
  .final-child {
    margin-left: -378px;
    height: 77px;
    width: 310px;
    position: relative;
    object-fit: contain;
    flex-shrink: 0;
  }
  .frame-child {
    width: 105px;
    height: 107px;
    position: relative;
    object-fit: cover;
  }
  .frame-item {
    width: 105px;
    height: 107px;
    position: relative;
    object-fit: cover;
  }
  .frame-inner {
    width: 105px;
    height: 107px;
    position: relative;
    object-fit: cover;
  }
  .rectangle-icon {
    width: 105px;
    height: 107px;
    position: relative;
    object-fit: cover;
  }
  .frame-child1 {
    width: 105px;
    height: 107px;
    position: relative;
    object-fit: cover;
  }
  .frame-child2 {
    width: 105px;
    height: 107px;
    position: relative;
    object-fit: cover;
  }
  .rectangle-parent {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    gap: 12px;
  }
  .frame-child3 {
    height: 95px;
    width: 91px;
    position: relative;
    object-fit: cover;
  }
  .mixed-grid-inner {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 0px 0px var(--padding-10xs);
  }
  .mixed-grid-child {
    width: 91px;
    height: 95px;
    position: relative;
    object-fit: contain;
  }
  .frame-child4 {
    height: 95px;
    width: 91px;
    position: relative;
    object-fit: cover;
  }
  .frame-div {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 0px 0px var(--padding-10xs);
  }
  .frame-child5 {
    height: 95px;
    width: 91px;
    position: relative;
    object-fit: contain;
  }
  .mixed-grid-inner1 {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 0px 0px var(--padding-10xs) var(--padding-12xs);
  }
  .frame-child6 {
    height: 95px;
    width: 91px;
    position: relative;
    object-fit: cover;
  }
  .mixed-grid-inner2 {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 0px 0px 0px var(--padding-12xs);
  }
  .mixed-grid {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    gap: 21px;
  }
  .mixed-grid-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 9px 0px 0px;
  }
  .frame-parent {
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 0px var(--padding-xl) 0px 0px;
    gap: 18px;
    opacity: 0.95;
  }
  .structure {
    width: 411px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 196px 0px 0px;
    box-sizing: border-box;
    max-width: 100%;
    flex-shrink: 0;
  }
  .top-element {
    height: 42px;
    flex: 1;
    position: relative;
  }

  .rectangle-group {
    align-self: stretch;
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    gap: 16px;
  }
  .content-area-inner {
    align-self: stretch;
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 37px 0px 0px;
  }
  .content-area {
    align-self: stretch;
    flex: 1;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
  }
  .content-area-wrapper {
    align-self: stretch;
    width: 204px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 136px 0px 0px;
    box-sizing: border-box;
  }
  .frame-child12 {
    position: absolute;
    top: 0px;
    left: 369px;
    width: 505px;
    height: 178px;
    object-fit: contain;
    z-index: 3;
  }
  .frame-container {
    height: 636px;
    flex: 1;
    position: relative;
    max-width: calc(100% - 266px);
  }
  .frame-group {
    align-self: stretch;
    flex: 1;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: flex-start;
    gap: 90px;
    max-width: 100%;
  }
  .right-panel {
    height: 882px;
    width: 1106px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 18px 0px 0px;
    box-sizing: border-box;
    max-width: 100%;
    flex-shrink: 0;
  }
  .final {
    width: auto;
    background-color: #0c0c0cb2;
    overflow: hidden;
    display: flex;
    align-items: flex-start;
    justify-content: flex-start;
    padding: 15px 0px 167px 335px;
    box-sizing: border-box;
    gap: 68px;
    line-height: normal;
    letter-spacing: normal;
  }

  @media screen and (max-width: 1525px) {
    .final {
      flex-wrap: wrap;
      padding-left: var(--padding-xl);
      padding-right: var(--padding-xl);
      box-sizing: border-box;
    }
  }
  @media screen and (max-width: 1225px) {
    .structure {
      padding-top: 127px;
      box-sizing: border-box;
    }

    .content-area-wrapper {
      padding-top: 88px;
      box-sizing: border-box;
    }

    .frame-group {
      gap: 31px;
    }
  }
  @media screen and (max-width: 850px) {
    .content-area-wrapper {
      display: none;
    }

    .frame-container {
      max-width: 100%;
    }

    .frame-group {
      gap: 15px;
    }

    .final {
      gap: 34px;
    }
  }
  @media screen and (max-width: 450px) {
    .structure {
      padding-top: 83px;
      box-sizing: border-box;
    }

    .content-area-wrapper {
      padding-top: 57px;
      box-sizing: border-box;
    }

    .final {
      gap: 17px;
    }
  }

/* FIN DEL CODIGO CSS BY MIUSTICAT, INICIO DE CODIGO ORIGINAL*/


.centering {
    margin: 0;
    position: absolute;
    top: 95%;
    left: 4%;
    margin-right: -50%;
    transform: translate(-4%, -95%)
}

.card2:hover {
    border: 0.5px solid #fff;
    box-shadow: 0 10px 20px rgba(0, 0, 0, .12), 0 4px 8px rgba(0, 0, 0, .06);
    cursor: pointer;
}

.icon {
    color: red;
    font-size: 0.9vw;
    transform: translateY(0.355vw);
    padding-right: 0.45vw;
    float: right;
}

.icon:hover {
    color: green;
}

.icon2 {
    color: green;
    font-size: 0.9vw;
    transform: translateY(0.355vw);
    padding-right: 0.45vw;
    float: right;
}

.icon2:hover {
    color: red;
}

.icon3 {
    color: white;
    font-size: 0.9vw;
    transform: translateY(0.355vw);
    padding-right: 0.45vw;
    float: right;
}

.icon3:hover {
    color: #3F6791;
}

.iconresponsive {
    font-size: 0.9vw;
    transform: translateY(0.355vw);
    padding-right: 0.45vw;
}

.propsresponsive {
    transform: translateY(-0.0345vw);
    font-size: 0.8vw;
}

@media (max-height: 600px) {
    .propsresponsive {
        transform: translateY(-0.1345vw);
        font-size: 0.8vw;
    }

    .inventorytext2 {
        transform: translateY(-0.1345vw);
    }
}

.grenade {
    margin-left: 0.8vh;
    margin-right: 0.55vh;
}

@media (max-height: 600px) {
    .grenade {
        margin-left: 1.5vh;
        margin-right: 0.425vh;
    }
}

@media (min-height: 1600px) {
    .grenade {
        margin-left: 0.8vh;
        margin-right: 0.355vh;
    }
}


/* PANEL DE INVENTARIO - DERECHO BY MIUSTICAT*/

.grid-container {
  position: absolute;
  top: 173px;
  left: 0px;
  filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
  width: 691px;
  height: 463px;
  display: grid;
  grid-template-columns: repeat(6, 106px);
  grid-template-rows: repeat(4, 109px);
  gap: 10px;
  
}



.grid-item {
  width: 106px;
  height: 109px;
  background-color: var(--color-gray);
  border: 1px solid var(--color-silver);
  display: flex;
  align-items: center;
  justify-content: center;
}


.items-use {
position: relative;
  width: 95px;
  height: 95px;
  background-color: var(--color-gray);
  border: 1px solid var(--color-silver);
  display: flex;
  align-items: center;
  justify-content: center;
  left: 150px;
}

.grid-item:hover {
  opacity: 0.6; /* Cambiar la opacidad al pasar el mouse */
}
.items-use:hover {
  opacity: 0.8; /* Cambiar la opacidad al pasar el mouse */
}



</style>
