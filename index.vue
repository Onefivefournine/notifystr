<style lang="scss">
$red: #ff482a;
$green: #6ae2a2;
.notifystr {
  &__container {
    position: fixed;
    top: 20px;
    width: 35%;
    right: 20px;
  }
  &__toast {
    color: #fff;
    box-sizing: border-box;
    animation: fadeIn 0.2s ease-in forwards;
    cursor: pointer;
    padding: 20px 40px;
    width: 100%;
    min-height: 40px;
    margin-bottom: 10px;
    border-radius: 5px;
    background-color: #444; // fallback color
    &--fadeout {
      animation: fadeOut 0.2s ease-in forwards
    }
    &--info {
      &.notifystr__toast--hovered {
        background-color: rgba(lightblue, 0.6);
      }
      color: #555;
      background-color: lightblue;
    }
    &--success {
      &.notifystr__toast--hovered {
        background-color: rgba($green, 0.6);
      }
      background-color: $green;
    }
    &--danger {
      &.notifystr__toast--hovered {
        background-color: rgba($red, 0.6);
      }
      background-color: $red
    }
    &--warning {
      &.notifystr__toast--hovered {
        background-color: rgba(gold, 0.6);
      }
      color: #222;
      background-color: gold
    }
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    margin-top: -10px;
  }
  to {
    opacity: 1;
    margin-top: 0;
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
    margin-top: 0;
  }
  to {
    opacity: 0;
    margin-top: -10px;
  }
}
</style>
<template>
  <div class="notifystr__container">
    <div v-for="toast in toasts"
      class="notifystr__toast"
      :class="'notifystr__toast--'+toast.type + (toast.fading?' notifystr__toast--fadeout':'') + (toast.hovered?' notifystr__toast--hovered':'')"
      @click="_fadeToast(toast)"
      @mouseover="stopFade(toast)"
      @mouseout="startFade(toast,1500)">
      <b>{{toast.title}}</b>
      <br>
      <span>{{toast.message}}</span>
    </div>
  </div>
</template>
<script>
import Vue from 'vue';
export default {
  data() {
    return {
      toasts: []
    }
  },
  created() {
    let self = this
    if(!this.$notifystr){
     Vue.prototype.$notifystr = {
            success(title, message,duration) {
                self._toast('success', title, message,duration)
            },
            info(title, message,duration) {
                self._toast('info', title, message,duration)
            },
            warning(title, message,duration) {
                self._toast('warning', title, message,duration)
            },
            danger(title, message,duration) {
                self._toast( 'danger', title, message,duration )
            },
        }
    } else {
      console.warn('WARNING! Notifystr used more than once!')
    }
  },
  methods: {
    _toast( type, title, message,duration=2500 ) {
      let toast = {
        _innerId: ( Math.random() * 1e7 ).toFixed(),
        type,
        title,
        message,
        fading: false,
        hovered: false
      }
      this.toasts.push( toast );
      this.startFade( toast, duration )
    },
    _fadeToast( toast ) {
      if ( !toast.fading ) {
        Vue.set( toast, 'fading', true );

        setTimeout( () => {
          let i = this.toasts.map( ( el ) => el._innerId ).indexOf( toast._innerId );
          if ( ~i ) this.toasts.splice( i, 1 );
        }, 300 );
      }
    },
    startFade( toast, timeout ) {
      Vue.set( toast, 'hovered', false );
      if ( !toast.fadingTimeout ) {
        const to = setTimeout( this._fadeToast, timeout, toast );
        Vue.set( toast, 'fadingTimeout', to )
      }
    },
    stopFade( toast ) {
      clearTimeout( toast.fadingTimeout )
      Vue.delete( toast, 'fadingTimeout' )
      Vue.set( toast, 'fading', false );
      Vue.set( toast, 'hovered', true );
    }
  },
}
</script>
