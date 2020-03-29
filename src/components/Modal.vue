<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >

        <section
          class="modal-body"
          id="modalDescription"
        >
          <slot name="body">
              <button
              type="button"
              class="btn-close"
              @click="close"
              aria-label="Close modal"
            >
              x
            </button>
            
            Aquí tienes tú Gif!
            <br/>
        <img/>
        <br/>
          <button
              type="button"
              class="btn-green"
              @click="goToURL"
              aria-label="Gif URL"
            >
                Gif URL
            </button>
          </slot>        
        </section>
      </div>
    </div>
  </transition>
</template>


<script>
  export default {

    
    name: 'Modal',
    data(){
        return{
            
        }
    },
    methods: {
      close() {
        this.$emit('close');
      },

      goToURL(){
          console.log('hola')
      }
    },
  };
</script>


<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(15, 39, 56, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: rgba(0,0,0,0.1);
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }


  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
  }

  .modal-fade-enter,
  .modal-fade-leave-active {
    opacity: 0;
  }

  .modal-fade-enter-active,
  .modal-fade-leave-active {
    transition: opacity .5s ease
  }
</style>
