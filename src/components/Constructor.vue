<script setup lang="ts">
    import Button from "./Button.vue";
    import {ref} from "vue";

    defineProps({
      name: String
    })

    interface Hammer {
      top: string;
      left: string;
      fontSize: string;
    }

    const hammers = ref<Hammer[]>([]);

    function spawnHammer(): void {
      hammers.value.push({
        top: Math.random() * 95 + "vh",
        left: Math.random() * 95 + "vw",
        fontSize: 1 + (Math.random() * 3) + "rem"
      })
    }

</script>

<template>
  <Button ref="buildBtn" @clicked='spawnHammer'>Click me!</Button>
  <div v-for="hammer in hammers" class="hammer"  :style="{ fontSize: hammer.fontSize, left: hammer.left, top: hammer.top}">🔨</div>
</template>

<style>
  .hammer {
    position: absolute;
    overflow: auto;
  }
</style>
