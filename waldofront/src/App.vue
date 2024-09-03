<script setup>
import { ref, onMounted } from 'vue';

const isBoxVisible = ref(false);
const boxPosition = ref({ left: '0px', top: '0px' });
const rightSide = ref(false);

function normalizedClick(event) {
  const img = document.getElementById('image');
  const rect = img.getBoundingClientRect();


  const clickX = event.clientX - rect.left;
  const clickY = event.clientY - rect.top;




  boxPosition.value = {
    left: `${clickX}px`,
    top: `${clickY}px`
  };


  isBoxVisible.value = !isBoxVisible.value;

  const normalizedX = clickX / rect.width;
  const normalizedY = clickY / rect.height;
  normalizedX > 0.5 ? rightSide.value = false : rightSide.value = true;

  console.log('Normalized X:', normalizedX.toFixed(4));
  console.log('Normalized Y:', normalizedY.toFixed(4));
}

onMounted(() => {
  const img = document.getElementById('image');
  img.addEventListener('click', normalizedClick);
});
</script>

<template>
  <header class="w-full text-center p-4">
    <h1 class="text-2xl font-bold mb-6">Find these pokèmon!</h1>
    <div class="flex justify-around">
      <div>
        <img class="rounded-sm border-2 border-black" src="@/assets/weedleicon.png" alt="weedle" draggable="false">
        <p class="font-semibold">Weedle</p>
      </div>
      <div>
      <img class="rounded-sm border-2 border-black" src="@/assets/shelldericon.jpg" alt="shellder" draggable="false">
      <p class="font-semibold">Shellder</p>
      </div>
      <div>
      <img class="rounded-sm border-2 border-black" src="@/assets/buttericon.jpg" alt="butterfree" draggable="false">
      <p class="font-semibold">Butterfree</p>
      </div>
    </div>
  </header>
  <div class="flex p-2 justify-center relative" >
    <div :class="isBoxVisible ? 'block' : 'hidden'" id="targetBox" class="absolute" :style="{ left: boxPosition.left, top: boxPosition.top }">

      <div class="bg-white bg-opacity-70 border-dashed border-blue-700 border-4 aspect-square lg:-translate-x-6 lg:-translate-y-6" :style="{ width: '4vw'}"></div>
    
      <ul :class="rightSide ? 'right-side-class' : 'left-side-class'" class="border-2 rounded-sm border-black bg-sky-200 w-full ">
        <li class="flex flex-wrap items-center gap-2 p-2 hover:bg-sky-100 cursor-pointer">
          <img class="w-3/12  rounded-sm border-2 border-black" src="@/assets/weedleicon.png" alt="weedle" draggable="false">
        <p class="font-semibold">Weedle</p>
        </li>
        <li class="flex flex-wrap items-center gap-2 p-2 hover:bg-sky-100 cursor-pointer">
          <img class="w-3/12  rounded-sm border-2 border-black" src="@/assets/shelldericon.jpg" alt="shellder" draggable="false">
      <p class="font-semibold">Shellder</p>
        </li>
        <li class="flex flex-wrap items-center gap-2 p-2 hover:bg-sky-100 cursor-pointer">
          <img class="w-3/12  rounded-sm border-2 border-black" src="@/assets/buttericon.jpg" alt="butterfree" draggable="false">
      <p class="font-semibold">Butterfree</p>
        </li>
      </ul>

     

    
  </div>
    <img class="w-full rounded-sm border-2 border-black mb-40" id="image" src="@/assets/pokemon.jpg" alt="pokemon" draggable="false">
  </div>


</template>

<style scoped>
.left-side-class {
  transform: translateX(-100%);
  right: 100%; /* Posiziona il menu sulla sinistra della box */
}

.right-side-class {
  left: 100%; /* Posiziona il menu sulla destra della box */
}
</style>