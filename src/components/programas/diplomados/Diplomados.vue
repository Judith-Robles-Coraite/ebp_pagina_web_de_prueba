<template>
  <div class="bg-white py-2 px-4 md:px-8 lg:px-20 mx-auto">
    <h2 class="text-center text-2xl md:text-3xl font-bold mb-6 md:mb-3 text-[#0A8B37]">
      MAESTRIAS EN OFERTA
    </h2>
  </div>
  <div class="flex justify-between items-center bg-white py-2 px-4 md:px-4 lg:px-20">
    <!-- Imagen del programa -->
    <div class="w-1/3 flex justify-center items-center">
      <div class="bg-white shadow-md rounded overflow-hidden w-64 ">
      <img 
        :src="currentImage" 
        class="w-full h-full transition-opacity duration-700 ease-in-out"
        @mouseover="changeImage(currentProgram.image2)"
        @mouseleave="resetImage()"
        alt="Programa"
      />
        <div class="flex justify-center p-4 mt-auto">
          <button class="relative flex items-center justify-center bg-[#057a55] text-white py-3 px-16 sm:py-2 sm:px-4 rounded-full text-lg sm:text-sm transform transition-transform duration-200 hover:scale-110">
            <font-awesome-icon :icon="['fab', 'whatsapp']" class="text-2xl text-white mr-2" />
            <span class="transform transition duration-300 hover:scale-100">INSCRÍBETE AHORA</span>
          </button>
        </div>
      </div>
    </div>
    <!-- Información del programa -->
    <div class="w-2/3 bg-white border border-[#0A8B37] rounded-3xl px-0 shadow-lg p-6">
      <h2 class="text-green-800 text-2xl font-bold text-center">{{ currentProgram.title }}</h2>
      <p class="mt-2 text-white  bg-[#0A8B37] text-center">{{ currentProgram.description }}</p>

      <div class="grid grid-cols-2 gap-4 mt-4">
  <div v-for="(feature, index) in currentProgram.features" 
      :key="feature.title" 
      :class="index === 4 && currentProgram.features.length === 5 ? 'col-span-2 mx-auto' : ''"
      class="flex items-center space-x-2 px-6">
      
    <svg
    v-if="!(index === 4 && currentProgram.features.length === 5)"
      xmlns="http://www.w3.org/2000/svg"
      width="48px"  
      height="48px" 
      viewBox="0 -960 960 960"
      class="mr-4 transition-colors duration-100"
    >
      <defs>
        <linearGradient id="iconGradient" x1="0%" y1="0%" x2="100%">
          <stop offset="0%" stop-color="#203C61" />
          <stop offset="100%" stop-color="#0A8B37" />
        </linearGradient>
      </defs>
      <path
        :d="feature.icon"
        class="fill-[url(#iconGradient)] group-hover:fill-white transition-colors duration-200"
      />
    </svg>

    <div class="flex-1">
      <p class="font-bold text-center">{{ feature.text }}</p>
      <p class=" text-gray-500  text-center">{{ feature.description }}</p>
    </div>


      </div>
    </div>

    </div>
  </div>

  <!-- Botones del carrusel -->
  <div class="flex justify-center space-x-4 mt-6">
    <button 
      v-for="(program, index) in programs" 
      :key="index" 
      @click="setCurrentProgram(index)"
      :class="{'bg-[#0A8B37] text-white': currentProgramIndex === index, 'bg-gray-200 text-green-700': currentProgramIndex !== index}"
      class="px-4 py-2 rounded-full transition-colors duration-300"
    >
      {{ program.shortTitle }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentProgramIndex: 0,
      currentImage: "src/assets/ofertas_academicas/doc1.jpg", // Imagen actual que se muestra
      programs: [
        {
          title: "Maestría en Hematología y Hemoterapia",
          shortTitle: "Hematología",
          image1: "src/assets/ofertas_academicas/doc1.jpg",
          image2: "src/assets/ofertas_academicas/doc2.jpg",
          description: "Programa semipresencial con duración de 16 meses...",
          features: [
            { icon: 'm662-556 160-92-160-92-160 92 160 92Zm0 122 110-64v-84l-110 64-110-64v84l110 64ZM81-160v-104q41.67 0 70.83 30.33Q181-203.33 181-160H81Zm200 0q0-84.66-58-144.33Q165-364 81-364v-60q108.64 0 184.32 77.5Q341-269 341-160h-60Zm160 0q0-75-28-141.5t-77-116q-49-49.5-114.5-78T81-524v-60q87 0 163.5 33.5t133.5 91q57 57.5 90 135T501-160h-60Zm160 0q0-108-40.5-203.5t-111-167Q379-602 284.18-643T81-684v-56q0-24.75 17.63-42.38Q116.25-800 141-800h680q24.75 0 42.38 17.62Q881-764.75 881-740v520q0 24.75-17.62 42.37Q845.75-160 821-160H601Z', 
            text: "Modalidad y carga horaria", description: "Virtual - 800 Horas Académicas, equivalentes a 20 Créditos Internacionales." },
            { icon:  'M321-160q-24 0-42-18t-18-42v-100h124v-127q-38 3-76-10.5T241-500v-58h-50L60-689q36-34 86-55.5T248-766q30 0 68.5 9.5T385-726v-74h455v535q0 44-30.5 74.5T735-160H321Zm124-160h245v55q0 20 12.5 32.5T735-220q20 0 32.5-12.5T780-265v-475H445v57l241 241v43h-43L517-525l-17 20q-13 15-26 23t-29 15v147ZM218-618h83v89q17 11 33.5 16.5T368-507q25 0 51-13.5t38-27.5l17-20-69-69q-32-32-72-50.5T248-706q-27 0-49 6.5T154-682l64 64Z', 
            text: "Entrega de su Título", description: "Su Título será entregado en la sede de su Ciudad, nosotros nos hacemos cargo de su trámite en la Universidad." },
            { icon: 'M860-283v-282L479-360 40-600l439-240 441 240v317h-60ZM479-120 189-279v-210l290 159 290-159v210L479-120Z', 
            text: "Dirigido", description: "A profesionales de todas las áreas (Técnicos Superiores y Licenciados), Diploma para habilitación como docente." },
            { icon: 'M306-394q-17 0-28.5-11.5T266-434q0-17 11.5-28.5T306-474q17 0 28.5 11.5T346-434q0 17-11.5 28.5T306-394Zm177 0q-17 0-28.5-11.5T443-434q0-17 11.5-28.5T483-474q17 0 28.5 11.5T523-434q0 17-11.5 28.5T483-394Zm170 0q-17 0-28.5-11.5T613-434q0-17 11.5-28.5T653-474q17 0 28.5 11.5T693-434q0 17-11.5 28.5T653-394ZM180-80q-24 0-42-18t-18-42v-620q0-24 18-42t42-18h65v-60h65v60h340v-60h65v60h65q24 0 42 18t18 42v620q0 24-18 42t-42 18H180Zm0-60h600v-430H180v430Z', 
            text: "Duración", description: "5 meses Avance académico más desarrollo de monografía." },
            { icon: 'M212-241v-339h60v339h-60Zm242 0v-339h60v339h-60ZM80-121v-60h800v60H80Zm608-120v-339h60v339h-60ZM80-640v-53l400-228 400 228v53H80Z', 
            text: "Titulación", description: "Universidad Autónoma del Beni José Ballivian. Universidad pública y parte del Comité Ejecutivo de la Universidad Boliviana C.E.U.B." }
          ]
        },
        // Puedes agregar más programas aquí

        {
          title: "Maestría en Hematología y Hemoterapia",
          shortTitle: "Hematología",
          image1: "src/assets/ofertas_academicas/doc2.jpg",
          image2: "src/assets/ofertas_academicas/doc2.jpg",
          description: "Programa semipresencial con duración de 16 meses...",
          features: [
            { icon: `<svg ...></svg>`, text: "Modalidad Virtual" },
            { icon: `<svg ...></svg>`, text: "Entrega de Título" },
            { icon: `<svg ...></svg>`, text: "Dirigido a Enfermería" },
            { icon: `<svg ...></svg>`, text: "Universidad Autónoma" },
          ]
        },
      ]
    };
  },
  computed: {
    currentProgram() {
      return this.programs[this.currentProgramIndex];
    }
  },
  methods: {
    setCurrentProgram(index) {
      this.currentProgramIndex = index;
      this.currentImage = this.programs[index].image1;
    },
    changeImage(newImage) {
      this.currentImage = newImage;
    },
    resetImage() {
      setTimeout(() => {
        this.currentImage = this.currentProgram.image1;
      }, 100); // Pausa para suavizar el cambio
    }
  }
};
</script>

<style scoped>
/* Puedes agregar estilos personalizados, pero Tailwind cubre la mayoría */
</style>
