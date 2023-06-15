<template>
 <div class="delete-circle"  @click="handleDeleteCard">
   <div class="iconito">
     <i class="bi bi-trash3"></i>
   </div>
</div>
  </template>
  
  <script>

  
  export default {
    name: 'ButtonDelete',
    methods:{

    handleDeleteCard() {
      this.$emit("delete-card");
    },

    }
  }
  </script>
  
  <style scoped>
  .delete-circle{
  width: 40px;
  height: 40px;
  text-align: center;
  color: #000;
  box-shadow: 0 0 20px 10px rgba(0, 0, 0, 0.05);

  border-radius: 50%;
  position: relative;
overflow: hidden;
transition: 0.5s;
}

.delete-circle .iconito {

  font-size: 15px;
  line-height: 40px;
  position: relative;
  z-index: 10;
  transition: color 0.5s;

}

.delete-circle::after{
  content: '';
  width: 100%;
  height: 100%;
  top: -90px;
  left: 0;
  background: linear-gradient(-45deg, #ed1c94, #ff1717);
  position: absolute;
  transition: 0.5s;
}

.delete-circle:hover::after{
  top: 0;
}

.delete-circle:hover .iconito{
  color: #fff;
}

.delete-circle:hover{
  transform: translateY(-10px);
}

  </style>
  