
<script setup>
import Api from './Api.vue'
</script>
<template>
    <div>
      <!-- Barra de navegación -->
      <div class="bg-violet-700 p-4 mb-4 text-white text-center">
        <div class="flex flex-col items-center justify-center lg:flex-row lg:items-center lg:justify-center text-2xl gap-5">
          <img src="../assets/logo.svg" alt="Logo de SITMOTUL" class="w-20 mx-4 mb-2 lg:mb-0">
          <!-- Texto visible en dispositivos grandes -->
          <p class="hidden lg:block mt-5 mb-2 text-center text-xl lg:text-2xl font-bold">INSTITUTO TECNOLÓGICO SUPERIOR DE MOTUL</p>
        </div>
        <!-- Texto visible en dispositivos móviles -->
        <p class="lg:hidden mt-5 mb-2 text-center text-xl lg:text-2xl font-bold">SITMOTUL</p>
      </div>
  
      
      <Api></Api>
    </div>
  </template>