<template>
  <div class="min-h-screen bg-gray-400">

    <div class="container py-6">
      
      <div class="bg-white p-4 shadow rounded">
        <h1 class="text-center font-semibold text-3xl mb-4">Quran App</h1>
        <div class="flex -mx-4 items-center mb-6">
          <div class="flex-1 px-4">
            <select @change="getSpecificSura" name="" id="" class="quran-input">
              <option value="">Select Sura</option>
              <option v-for="sura in suras" :value="sura.number">{{ sura.englishName }} - {{ sura.name }}</option>
            </select>
          </div>

          <div class="flex-1 px-4 text-center">
            <h3 class="font-bold mb-1 text-lg">{{ currentSura.name }} - {{ currentSura.englishName }}</h3>
            <p>{{ currentSura.englishNameTranslation }} | Ayahs - {{ currentSura.numberOfAyahs }}</p>
          </div>
          
        </div>

        <div v-if="loading" class="flex text-center">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 animate-spin">
            <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12a7.5 7.5 0 0015 0m-15 0a7.5 7.5 0 1115 0m-15 0H3m16.5 0H21m-1.5 0H12m-8.457 3.077l1.41-.513m14.095-5.13l1.41-.513M5.106 17.785l1.15-.964m11.49-9.642l1.149-.964M7.501 19.795l.75-1.3m7.5-12.99l.75-1.3m-6.063 16.658l.26-1.477m2.605-14.772l.26-1.477m0 17.726l-.26-1.477M10.698 4.614l-.26-1.477M16.5 19.794l-.75-1.299M7.5 4.205L12 12m6.894 5.785l-1.149-.964M6.256 7.178l-1.15-.964m15.352 8.864l-1.41-.513M4.954 9.435l-1.41-.514M12.002 12l-3.75 6.495" />
          </svg>
           loading ...

        </div>

        <div v-else class="text-4xl mt-8 text-slate-700 relative min-h-[20rem]">
          <div class="px-4">
            <p class="flex mb-8 text-right leading-[3rem]" v-if="currentSura.hasOwnProperty('ayahs')" v-for="(ayah, index) in  currentSura.ayahs" :key="ayah.index">









              <span class="flex-1 text-end mr-4"><span class=" font-arabic">{{ ayah.text }} </span> <br>
                <span class="text-lg font-bangla">{{ currentSurahBangla.ayahs[index].text }}</span> <br>
                <span class="float-right">
    <av-waveform :canv-height="0" :canv-width="0" :src="ayah.audio" symmetric="true"></av-waveform></span>
</span>

              <span class="text-xs self-baseline mr-4 w-10 h-10 flex text-right items-center justify-center border-4 border-lime-400 rounded-full">{{ ayah.numberInSurah }}</span>

            </p>

          </div>

            
          </div>

          
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default{
    name: 'App',
    data (){
      return {
        suras: [],
        currentSura: [],
        currentSurahBangla: [],
        loading: true
      }
    },
    mounted () {
      axios.get('https://api.alquran.cloud/v1/surah').then(response => {
        this.suras = response.data.data
      })

      this.querySpecificSura(1);

    },
    methods: {
      getSpecificSura(e){
        this.querySpecificSura(e.target.value);
      },
      querySpecificSura(suraNumber){
        this.loading = true;
        axios.get('https://api.alquran.cloud/v1/surah/' + suraNumber + '/editions/ar.alafasy,bn.bengali').then(response => {
          this.currentSura = response.data.data[0];
          this.currentSurahBangla = response.data.data[1];
          
          this.loading = false
        });
        //axios.get('https://api.alquran.cloud/v1/surah/'+suraNumber+'/editions/bn.bengali').then(response => {
          //this.currentSurahBangla = response.data.data[0];
          //this.loading = false
        //})
      }
    }
  };
</script>