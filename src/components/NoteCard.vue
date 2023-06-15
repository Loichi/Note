<template>
  <!-- Add the following lines to your HTML file -->



  <div class="note-card">
    <div :class="['carte', colorClass, { 'carte-added': isCardAdded }]">
      <div class="description" @click="handleUpdateCard">{{ truncatedDescription }}</div>
      <div class="carte-bottom">
        <div>{{ date }}</div>
        <ButtonDelete @delete-card="handleCardDelete" />
      </div>
    </div>
  </div>
   
</template>

<script>

import ButtonDelete from "./ButtonDelete.vue";

export default {
  name: "NoteCard",

  props: {
    id: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: false,
    },
    date: {
      type: Date,
      required: true,
      default: () => {
        const currentDate = new Date();
        const year = String(currentDate.getFullYear()).slice(-2);
        const month = String(currentDate.getMonth() + 1).padStart(2, "0");
        const day = String(currentDate.getDate()).padStart(2, "0");
        return `${day}.${month}.${year}`;
      },
    },
    color: {
      type: String,
      required: false,
    },
  },


  data() {
    return {
      showModal: false,
      editedDescription: '',
    };
  },


  computed: {
    truncatedDescription() {
      const maxLength = 100;
      if (this.description && this.description.length > maxLength) {
        return this.description.slice(0, maxLength) + "...";
      }
      return this.description;
    },
    colorClass() {
      return this.color ? `bg-color-${this.color}` : "";
    },
  },


  methods: {


    handleCardDelete() {
      this.$emit("delete-card", this.id);
    },


  },



  components: {
    ButtonDelete
  },
};
</script>

<style>
.carte {
  height: 25vh;
  width: 13vw;
  border-radius: 8%;
  padding: 20px;
  text-align: start;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 1vw;
  margin-bottom: 2vh;
}

.description {
  word-wrap: break-word;
  height: 20vh;
}

.carte-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.bg-color-one {
  background-color: #ffd68f;
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
</style>
