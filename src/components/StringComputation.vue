<template>
  <div class="absolute right-10 top-10 w-72 flex flex-col gap-6 dark:text-white text-black border dark:border-none border-1 bg-light dark:bg-light/10 p-4 rounded-md z-30">
    <div class="flex flex-col gap-1">
      <h1>String Computation</h1>
      <hr class="border border-black rounded-md dark:border-white" />
    </div>
    <div class="grid grid-cols-2 gap-3 max-h-[190px] overflow-y-scroll">
      <template v-for="i in system.inputs.length">
        <input v-model="system.inputs[i-1]" class="border dark:border-white border-1 rounded-md px-2"></input>
        <div v-if="system.verdicts[i-1] === 'Accepted'"><span class="text-green-600">{{system.verdicts[i-1]}}</span></div>
        <div v-else-if="system.verdicts[i-1] === 'Rejected'"><span class="text-red-400">{{system.verdicts[i-1]}}</span></div>
        <div v-else>{{system.verdicts[i-1]}}</div>
      </template>
    </div>
    <div class="flex flex-col gap-1">
      <label for="fil">Text file:</label>
      <input type="file" @change="onFile" accept=".txt" />
    </div>
    <div class="flex flex-col gap-1">
      <label for="acc">Acceptance type:</label>
      <select v-model="system.interp" name="Select" class="border dark:border-white rounded-md p-1" id="acc">
        <option disabled value="">Select one</option>
        <option value="bin">Binary string</option>
        <option value="dif">Spike difference</option>
      </select>
    </div>
    <button class="bg-primary py-1 rounded-md text-white hover:scale-105 disabled:bg-primary/50 disabled:hover:scale-100 transition-all" :disabled="navbar.running" @click="judge">Judge</button>
  </div>
</template>

<script setup>
import system from "@/stores/system";
import navbar from "@/stores/navbar";

const onFile = (e) => {
  const file = e.target.files[0];
  const reader = new FileReader();
  reader.readAsText(file);
  reader.onload = () => {
    system.inputs = reader.result.split('\n').filter(s => s.length);
    system.verdicts = new Array(system.inputs.length).fill('?');
  }
}

const judge = async () => {
  if (system.halted || system.reset) {
    system.ws = new WebSocket(
      `${import.meta.env.VITE_WS_API}/ws/compute`
    );
  }
  system.verdicts = new Array(system.inputs.length).fill("Loading...");
}
</script>
