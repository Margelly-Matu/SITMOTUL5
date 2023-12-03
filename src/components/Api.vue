<template>
	<!-- Sección 1 -->
    <div class="grid grid-cols-1 md:grid-cols-2">
      <div class="md:flex md:items-center md:justify-center bg-purple-200 w-full md:w-3/4 mx-auto rounded-lg py-8 p-6 mb-3 mt-10">
        <div v-if="info" class="flex flex-row-2 grid grid-cols-2 gap-5">
          <!-- ... (contenido existente) -->
<div class="bg-purple-400 rounded-lg">
	<div class="  bg-purple-300 rounded-lg mt-3 mx-3 mb-3 text-center md: ">
						<img src="../assets/evaluado.png" alt="Logo de evaluados" class="w-20 mx-auto py-2">
						<p class="font-sans text-lg text-black font-bold">Alumnos Evaluados: {{ info.alEvaluados }}</p>
					</div>
</div>
<div class="bg-purple-400 rounded-lg">		
					<div class="  bg-purple-300 rounded-lg mt-3 mx-3 mb-3 text-center ">
						<img src="../assets/alumno1.png" alt="Logo de alumnos totales" class="w-20 mx-auto py-2">
						<p class="font-sans text-lg text-black font-bold">Total de Alumnos: {{ info.alTotal }}</p>
					</div>
					</div>
					<div class="bg-purple-400 rounded-lg ">	
					<div class=" bg-purple-300 rounded-lg  mt-3 mx-3 mb-3 text-center ">
						<img src="../assets/periodo.png" alt="Logo de periodo" class="w-20 mx-auto py-2">
						<p class="font-sans text-lg text-black font-bold">Periodo: {{ info.periodo }}</p>
					</div>
					</div>
					
					<div class="bg-purple-400 rounded-lg ">	
					<div class=" bg-purple-300 rounded-lg  mt-3 mx-3 mb-3 text-center ">
						<img src="../assets/porcentaje2.png" alt="Logo de periodo" class="w-20 mx-auto py-2">
        <p class="font-sans text-lg text-black font-bold"> Porcentaje de Alumnos Evaluados: {{ calcularPorcentaje(info.alEvaluados, info.alTotal) }}%
        </p>
      </div>
	  </div>
	  
				</div>
			</div>



			 <!-- Sección 2 -->
			 <div class="md:flex md:items-center md:justify-center bg-purple-200 w-full md:w-3/4 mx-auto rounded-lg py-8 p-4 mb-3 mt-10">
        <div v-if="info" class="flex flex-row-4 grid grid-cols-2 gap-5 ">

					<div class="bg-purple-400 rounded-lg">	
					<div class=" gap-5 bg-purple-300 rounded-lg mt-3 mx-3 mb-3 text-center   ">
						<img src="../assets/inicio.png" alt="Logo de inicio de evaluación" class="w-20 mx-auto py-4">
						<p class="font-sans text-lg text-black font-bold">Inicio: {{ formatDate(info.inicio) }}</p>
					</div>
					</div>
					<div class="bg-purple-400 rounded-lg">	
					<div class=" gap-5 bg-purple-300 rounded-lg mt-3 mx-3 mb-3 text-center ">
						<img src="../assets/fin.png" alt="Logo de fin de evaluación" class="w-20 mx-auto py-2">

						<p class="font-sans text-lg text-black font-bold">Fin: {{ formatDate(info.fin) }}</p>

					</div>
					</div>
					<div class="bg-purple-400 rounded-lg">	
					<div class=" gap-5 bg-purple-300 rounded-lg  mt-3 mx-3 mb-3 text-center">
						<!-- <div class=" gap-5  bg-gray-500 rounded-lg mb-3"> -->
						<img src="../assets/horas.png" alt="Logo de fin de evaluación" class="w-20 mx-auto py-2 ">
						<p class="font-sans text-lg text-black font-bold">Horas restantes: {{ calculateHoursRemaining(info.fin) }}</p>

</div>
					</div>
					<div class="bg-purple-400 rounded-lg ">	
					<div class=" bg-purple-300 rounded-lg  mt-3 mx-3 mb-3 text-center ">
						<img src="../assets/porcentaje1.png" alt="Logo de periodo" class="w-20 mx-auto py-2">
        <p class="font-sans text-lg text-black font-bold"> Porcentaje de Alumnos Pendientes de Evaluar: {{ calcularPorcentajePendientes(info.alEvaluados, info.alTotal) }}%
        </p>
      </div>
	  </div>

				</div>
			</div>

		</div>
 <!-- Título -->
 <div class="flex items-center justify-center mt-4">
      <p class="font-serif text-lg text-white font-bold">Estado de la evaluación por ingeniería</p>
    </div>
		
		<!-- Sección 3 -->
		<div class="md:flex md:items-center md:justify-center bg-purple-200 w-full md:w-3/4 mx-auto rounded-lg py-8 p-4 mb-3 mt-10 ">
      <div v-if="datos" class="flex flex-col md:flex-row gap-5 w-full mr-0 ">
		
        <!-- Bloque 1 -->
        <div class="bg-purple-400 rounded-lg text-center md:w-1/6  ">
          <div class="gap-5 bg-purple-300 rounded-lg mt-4 mx-4 mb-2 text-center">
            <p class="font-sans text-2x1 text-black font-bold" v-if="datos.ISC"> Listas: {{ datos.ISC.listas }} Faltantes: {{ datos.ISC.faltantes }}</p>
			<label class="font-sans text-2X1 text-black font-bold" v-if="datos.ISC">Porcentaje completado: {{ Math.round(((datos.ISC.listas - datos.ISC.faltantes) / datos.ISC.listas) * 100) }}%</label>
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.ISC" :style="{ color: (datos.ISC.faltantes === 0) ? 'green' : 'darkred' }"> Porcentaje Faltante: {{ Math.round((datos.ISC.faltantes / datos.ISC.listas) * 100) }}%</p>
            <img src="../assets/ISC.png" alt="Logo de ISC" class="w-20 mx-auto py-2">
          </div>
          <p class="font-sans text-2x1 text-white font-bold mt-2 mb-2"> SISTEMAS COMPUTACIONALES</p>
        </div>

        <div class="bg-purple-400 rounded-lg text-center md:w-1/6 ">
          <div class="gap-5 bg-purple-300 rounded-lg mt-4 mx-4 mb-2 text-center">
			<p class="font-sans text-lg text-black font-bold" v-if="datos.IEM"> Listas: {{ datos.IEM.listas }} Faltantes: {{ datos.IEM.faltantes }}</p>
			<label class="font-sans text-2X1 text-black font-bold" v-if="datos.IEM">Porcentaje completado: {{ Math.round(((datos.IEM.listas - datos.IEM.faltantes) / datos.IEM.listas) * 100) }}%</label>
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.IEM" :style="{ color: (datos.IEM.faltantes === 0) ? 'green' : 'darkred' }"> Porcentaje Faltante: {{ Math.round((datos.IEM.faltantes / datos.IEM.listas) * 100) }}%</p>
            <img src="../assets/IEM.png" alt="Logo de IEM" class="w-40 mx-auto py-2">
          </div>
          <p class="font-sans text-2x1 text-white font-bold mt-2 mb-2"> ELECTROMECÁNICA</p>
        </div>

        <!-- Bloque 3 -->
        <div class="bg-purple-400 rounded-lg text-center md:w-1/6 ">
          <div class="gap-5 bg-purple-300 rounded-lg mt-4 mx-4 mb-2 text-center">
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.IER"> Listas: {{ datos.IER.listas }} Faltantes: {{ datos.IER.faltantes }}</p>
			<label class="font-sans text-2X1 text-black font-bold" v-if="datos.IER">Porcentaje completado: {{ Math.round(((datos.IER.listas - datos.IER.faltantes) / datos.IER.listas) * 100) }}%</label>
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.IER" :style="{ color: (datos.IER.faltantes === 0) ? 'green' : 'darkred' }"> Porcentaje Faltante: {{ Math.round((datos.IEM.faltantes / datos.IEM.listas) * 100) }}%</p>
            <img src="../assets/IER.png" alt="Logo de IER" class="w-20 mx-auto py-2">
          </div>
          <p class="font-sans text-2x1 text-white font-bold mt-2 mb-2"> ENERGÍAS RENOVABLES</p>
        </div>

        <!-- Bloque 4 -->
        <div class="bg-purple-400 rounded-lg text-center md:w-1/6 ">
          <div class="gap-5 bg-purple-300 rounded-lg mt-4 mx-4 mb-2 text-center">
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.IE"> Listas: {{ datos.IE.listas }} Faltantes: {{ datos.IE.faltantes }}</p>
			<label class="font-sans text-2X1 text-black font-bold" v-if="datos.IE">Porcentaje completado: {{ Math.round(((datos.IE.listas - datos.IE.faltantes) / datos.IE.listas) * 100) }}%</label>
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.IE" :style="{ color: (datos.IE.faltantes === 0) ? 'green' : 'darkred' }"> Porcentaje Faltante: {{ Math.round((datos.IE.faltantes / datos.IE.listas) * 100) }}%</p>
            <img src="../assets/IE.png" alt="Logo de IE" class="w-20 mx-auto py-2">
          </div>
          <p class="font-sans text-2x1 text-white font-bold mt-2 mb-2">ELECTRÓNICA </p>
        </div>

        <!-- Bloque 5 -->
        <div class="bg-purple-400 rounded-lg text-center md:w-1/6 ">
          <div class="gap-5 bg-purple-300 rounded-lg mt-4 mx-4 mb-2 text-center">
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.II"> Listas: {{ datos.II.listas }} Faltantes: {{ datos.II.faltantes }}</p>
			<label class="font-sans text-2X1 text-black font-bold" v-if="datos.II">Porcentaje completado: {{ Math.round(((datos.II.listas - datos.II.faltantes) / datos.II.listas) * 100) }}%</label>
			<p class="font-sans text-2X1 text-black font-bold" v-if="datos.II" :style="{ color: (datos.II.faltantes === 0) ? 'green' : 'darkred' }"> Porcentaje Faltante: {{ Math.round((datos.II.faltantes / datos.II.listas) * 100) }}%</p>
            <img src="../assets/II.png" alt="Logo de II" class="w-20 mx-auto">
          </div>
          <p class="font-sans text-2x1 text-white font-bold mt-2 mb-2"> INDUSTRIAL</p>
        </div>
      </div>
    </div>


</template>
  
<script setup>

import { onMounted } from 'vue'
import { ref } from 'vue'

const info = ref({})
const datos = ref({})
async function fetchData() {
	try {
		const response = await fetch('https://sitmotul.com.mx/api/statusEval');
		const data = await response.json();
		info.value = data;

		console.log('Datos recibidos:', data);
	} catch (error) {
		console.error('Error al obtener datos:', error);
	}
}

async function fetchData2() {
	try {
		const response = await fetch('https://sitmotul.com.mx/api/statusEvalIng');
		const data = await response.json();
		datos.value = data;

		console.log('Datos recibidos:', data);
	} catch (error) {
		console.error('Error al obtener datos:', error);
	}
}

onMounted(() => {
	fetchData();
	fetchData2();
})

function formatDate(fecha) {
	const meses = ["Enero", "Febrero", "Marzo", "Abril", "Mayo", "Junio", "Julio", "Agosto", "Septiembre", "Octubre", "Noviembre", "Diciembre"];

	const fechaActual = new Date(fecha);
	const dia = fechaActual.getDate();
	const mes = meses[fechaActual.getMonth()];
	const año = fechaActual.getFullYear();

	return `${dia} de ${mes} de ${año}`;
}

function calculateHoursRemaining(deadline) {
	const fechaLimite = new Date(deadline);
	const ahora = new Date();

	// Calcula la diferencia en horas
	const diferenciaHoras = Math.floor((fechaLimite - ahora) / (1000 * 60 * 60));

	return `${diferenciaHoras} horas`;
}

// Función para calcular el porcentaje

function calcularPorcentaje(evaluados, total) {
      return ((evaluados / total) * 100).toFixed(2);
    }
	function calcularPorcentajePendientes(evaluados, total) {
      return (((total - evaluados) / total) * 100).toFixed(2)

    }
</script>
   
   
   