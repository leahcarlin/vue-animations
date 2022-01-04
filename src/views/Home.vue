<template>
  <div class="home">
    <transition name="toast-fade">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
    <transition name="fade">
      <div v-if="showP">Hello</div>
    </transition>
    <button @click="showP = !showP">toggle</button>
  </div>
</template>

<script>
import { ref } from "vue";
import Toast from "../components/Toast";
import Todos from "../components/Todos";

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false);
    const showP = ref(false);

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };

    return { showToast, triggerToast, showP };
  },
};
</script>

<style>
/* where you start */
.fade-enter-from {
  opacity: 0; /* want it to be invisible */
}
/* state you want to go to (sometimes you don't need because opacity 1 is default state) */
.fade-enter-to {
  opacity: 1;
}
/* control the transition (how long and ease) */
.fade-enter-active {
  transition: all 2s ease;
}
/* state on page before we transition it out */
.fade-leave-from {
  opacity: 1;
}
/* where we want to end up (sometimes you don't need)*/
.fade-leave-to {
  opacity: 0;
}
/* controls leave transition */
.fade-leave-active {
  transition: all 2s ease;
}

.toast-fade-enter-active {
  animation: wobble 0.5s ease;
}
.toast-fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.toast-fade-leave-to {
  opacity: 0;
  transform: translateY(-60px);
}
.toast-fade-leave-active {
  transition: all 0.3s ease;
}

@keyframes wobble {
  0% {
    transform: translateY(-60px);
    opacity: 0;
  }
  50% {
    transform: translateY(0);
    opacity: 1;
  }
  60% {
    transform: translateX(8px);
  }
  70% {
    transform: translateX(-8px);
  }
  80% {
    transform: translateX(4px);
  }
  90% {
    transform: translateX(-4px);
  }
  100% {
    transform: translateX(0px);
  }
}
</style>
