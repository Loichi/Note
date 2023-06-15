<template>
  <div class="container-fluid">
    <div class="row">
      <nav class="col-md-1 d-md-block bg-light sidebar">
        <div class="sidebar-sticky">
          <i :class="menuButtonClass" @click="handleIconClick"></i>
          <div v-if="showCircles" class="d-flex flex-column align-items-center justify-content-center mt-3">
            <div class="rotate-div bg-color-one rounded p-3" style="width: 20px; height: 20px;" @click="openModal('one')"></div>
            <div class="rotate-div bg-color-two rounded p-3 mt-2" style="width: 20px; height: 20px;" @click="openModal('two')"></div>
            <div class="rotate-div bg-color-three rounded p-3 mt-2" style="width: 20px; height: 20px;" @click="openModal('three')"></div>
            <div class="rotate-div bg-color-four rounded p-3 mt-2" style="width: 20px; height: 20px;" @click="openModal('four')"></div>
          </div>
          <!-- Modal -->
          <div class="modal" tabindex="-1" role="dialog" :class="{ 'd-block': isModalOpen }">
            <div class="modal-dialog" role="document">
              <div class="modal-content">
                <form @submit="submitForm">
                  <div class="modal-header">
                    <h5 class="modal-title">Ajouter une Note</h5>
                    <button type="button" class="close" @click="closeModal">
                      <span aria-hidden="true">&times;</span>
                    </button>
                  </div>
                  <div class="modal-body">
                    <input v-model="cardDescription" type="text" class="form-control" placeholder="Description" required />
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" @click="closeModal">Fermer</button>
                    <button type="submit" class="btn btn-primary">Ajouter</button>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>


export default {
  data() {
    return {
      showCircles: false,
      isIconClicked: false,
      isModalOpen: false,
      cardDescription: "",
      cardColor: "",
      id:0
    };
  },
  computed: {
    menuButtonClass() {
      return this.isIconClicked ? "menu-button bi bi-file-minus-fill" : "menu-button bi bi-file-plus-fill";
    },
  },
  methods: {
    handleIconClick() {
      this.showCircles = !this.showCircles;
      this.isIconClicked = !this.isIconClicked;
    },
    openModal(color) {
      this.cardColor = color;
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
      this.cardDescription = "";
      this.cardColor = "";
    },
    submitForm(event) {
      event.preventDefault();
      if (this.cardDescription.trim() === "") {
        return;
      }
      const newCard = {
        
        id: this.id,
        description: this.cardDescription,
        color: this.cardColor,
      };
      this.id++
      this.closeModal();
      this.$emit("card-added", newCard);
    },
  },
};
</script>


<style>
.sidebar {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: 100;
  padding: 48px 0;
  overflow-x: hidden;
  overflow-y: auto;
  background-color: #f8f9fa;
}

.sidebar-sticky {
  position: sticky;
  height: 20vh;
  display: flex;
  flex-direction: column;
  /* Ajoutez d'autres styles personnalisés ici */
}

/**
*Menu Button
*/
.menu-button {
  font-size: 40px;
}

.menu-button:hover {
  color: blue;
}

.bg-color-one {
  background-color: 	#ffd68f;
}

.bg-color-two {
  background-color: #ffac78;
}

.bg-color-three {
  background-color: #b3ff78;
}

.bg-color-four {
  background-color: #c08cff;
}

.rotate-div{
  transition: all 2s ease-in-out;
}
.rotate-div:hover{
  transform: rotate(360deg);
}
</style>
