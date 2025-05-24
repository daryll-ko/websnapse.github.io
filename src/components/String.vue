<template>
  <div class="absolute right-10 top-10 w-72 flex flex-col gap-6 dark:text-white text-black border dark:border-none border-1 dark:bg-light/10 p-4 rounded-md">
    <div class="flex flex-col gap-1">
      <h1>String Computation</h1>
      <hr class="border border-black rounded-md dark:border-white" />
    </div>
    <div class="grid grid-cols-2 gap-3">
      <template v-for="n in 5">
        <input class="border dark:border-white border-1 rounded-md px-2"></input>
        <div>&lt;verdict&gt;</div>
      </template>
    </div>
    <div class="flex flex-col gap-1">
      <label for="fil">Text file:</label>
      <input type="file"/>
    </div>
    <div class="flex flex-col gap-1">
      <label for="acc">Acceptance type:</label>
      <select name="Select" class="border dark:border-white rounded-md p-1" id="acc">
        <option value="bin">Binary string</option>
        <option value="diff">Spike difference</option>
      </select>
    </div>
    <button class="bg-primary py-1 rounded-md text-white hover:scale-105 transition-all">Judge</button>
  </div>
</template>
