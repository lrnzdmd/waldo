<script setup>

async function normalizedClick(event) {
  const img = document.getElementById('image');
  const rect = img.getBoundingClientRect();

  const targetBox = document.getElementById('targetBox');

  const clickX = event.pageX;
  const clickY = event.pageY;
  

  targetBox.style.left = `${clickX}px`; 
  targetBox.style.top = `${clickY}px`; 
  targetBox.style.display = 'block'; 
  
  const absRect = {
    left: rect.left + window.scrollX,
    top: rect.top + window.scrollY,
    width: rect.width,
    height: rect.height
  };
  
  console.log('Absolute rectangle:', absRect);
  
  const normalizedX = (event.pageX - absRect.left) / absRect.width;
  const normalizedY = (event.pageY - absRect.top) / absRect.height;
  
  console.log('Normalized X:', normalizedX.toFixed(4));
  console.log('Normalized Y:', normalizedY.toFixed(4));
}

document.addEventListener('DOMContentLoaded', () => {
 

  
  document.addEventListener('click', normalizedClick)
})
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
  <div class="flex p-2 justify-center" >
    <div id="targetBox" class="absolute hidden">
    <div class="bg-white bg-opacity-70 border-dashed border-blue-700 border-4 aspect-square  " style="width: 4vw; transform: translate(-2.5vw, -2.5vw); "></div>
    
      <ul class="border-2 rounded-sm border-black bg-sky-200 w-full" style="transform: translateX(-5vw);">
        <li class="flex items-center gap-2 p-2 hover:bg-sky-100 cursor-pointer">
          <img class="w-3/12  rounded-sm border-2 border-black" src="@/assets/weedleicon.png" alt="weedle" draggable="false">
        <p class="font-semibold">Weedle</p>
        </li>
        <li class="flex items-center gap-2 p-2 hover:bg-sky-100 cursor-pointer">
          <img class="w-3/12  rounded-sm border-2 border-black" src="@/assets/shelldericon.jpg" alt="shellder" draggable="false">
      <p class="font-semibold">Shellder</p>
        </li>
        <li class="flex items-center gap-2 p-2 hover:bg-sky-100 cursor-pointer">
          <img class="w-3/12  rounded-sm border-2 border-black" src="@/assets/buttericon.jpg" alt="butterfree" draggable="false">
      <p class="font-semibold">Butterfree</p>
        </li>
      </ul>

    
  </div>
    <img class="w-full rounded-sm border-2 border-black mb-40" id="image" src="@/assets/pokemon.jpg" alt="pokemon" draggable="false">
  </div>


</template>