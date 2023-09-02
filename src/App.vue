<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <Autocomplete
    auto-select
    :default-value="val"
    :key="updated"
    :search="langFilter"
    submit-on-enter
    submit-on-tab
    v-on:blur="handleBlur($event)"
    v-on:submit="handleSubmit($event)"
    v-on:isvalid="handleIsValid($event)"
    v-on:matchcount="handleMatched($event)" />
</template>

<script setup>
import Autocomplete from './components/autocomplete-vue/Autocomplete.vue'
import './assets/style.css';

const languageList = [
  {
      "Id": "03855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Aboriginal"
  },
  {
      "Id": "05855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Acadian"
  },
  {
      "Id": "07855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Acehnese"
  },
  {
      "Id": "09855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Acholi"
  },
  {
      "Id": "0b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Afrikaans"
  },
  {
      "Id": "0d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ainu"
  },
  {
      "Id": "0f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Akan"
  },
  {
      "Id": "11855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Akoli"
  },
  {
      "Id": "13855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Albanian"
  },
  {
      "Id": "15855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Altai"
  },
  {
      "Id": "17855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "American Indian"
  },
  {
      "Id": "19855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Amerind"
  },
  {
      "Id": "1b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Amharic"
  },
  {
      "Id": "1d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Amoy"
  },
  {
      "Id": "1f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Angal"
  },
  {
      "Id": "21855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Annam Muong"
  },
  {
      "Id": "23855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Annamese"
  },
  {
      "Id": "25855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Aphasic"
  },
  {
      "Id": "86283794-3eda-de11-afe3-00155d0a121f",
      "Name": "Arabic"
  },
  {
      "Id": "29855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Aramaic"
  },
  {
      "Id": "2b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Armenian"
  },
  {
      "Id": "2d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Aromunian"
  },
  {
      "Id": "2f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ashanti"
  },
  {
      "Id": "31855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Assamese"
  },
  {
      "Id": "33855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Assyrian"
  },
  {
      "Id": "35855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ateso"
  },
  {
      "Id": "37855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Auslan"
  },
  {
      "Id": "39855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Azerbaijani"
  },
  {
      "Id": "3b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Azeri"
  },
  {
      "Id": "3d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bahasa"
  },
  {
      "Id": "3f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bahasa Indonesia"
  },
  {
      "Id": "41855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bahasa Malaysia"
  },
  {
      "Id": "43855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bahnar"
  },
  {
      "Id": "45855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bai"
  },
  {
      "Id": "47855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bali Sasak"
  },
  {
      "Id": "49855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Balinese"
  },
  {
      "Id": "4b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Balochi"
  },
  {
      "Id": "4d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Balti"
  },
  {
      "Id": "4f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Baluchi"
  },
  {
      "Id": "51855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bambara"
  },
  {
      "Id": "53855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bantu"
  },
  {
      "Id": "55855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bari"
  },
  {
      "Id": "57855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bashkir"
  },
  {
      "Id": "59855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Basque"
  },
  {
      "Id": "5b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Batak"
  },
  {
      "Id": "5d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bau"
  },
  {
      "Id": "5f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Beach La Mar"
  },
  {
      "Id": "61855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Belorussian"
  },
  {
      "Id": "63855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bemba"
  },
  {
      "Id": "65855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bengali"
  },
  {
      "Id": "67855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Berber"
  },
  {
      "Id": "69855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bete"
  },
  {
      "Id": "6b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bhili"
  },
  {
      "Id": "6d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bhojpuri"
  },
  {
      "Id": "6f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bhotia"
  },
  {
      "Id": "71855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bichelamar"
  },
  {
      "Id": "73855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bicolano"
  },
  {
      "Id": "75855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bihari"
  },
  {
      "Id": "77855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bikol"
  },
  {
      "Id": "79855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bini"
  },
  {
      "Id": "7b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bisaya"
  },
  {
      "Id": "7d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bisayan"
  },
  {
      "Id": "7f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bislama"
  },
  {
      "Id": "81855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bobangi"
  },
  {
      "Id": "83855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bokmal"
  },
  {
      "Id": "85855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bontok"
  },
  {
      "Id": "87855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bosnian"
  },
  {
      "Id": "89855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Botswanian"
  },
  {
      "Id": "8b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Brahui"
  },
  {
      "Id": "8d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Breton"
  },
  {
      "Id": "8f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bru"
  },
  {
      "Id": "91855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Buginese"
  },
  {
      "Id": "93855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Bulgarian"
  },
  {
      "Id": "95855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Burmese"
  },
  {
      "Id": "97855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Burushaski"
  },
  {
      "Id": "99855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Buyi"
  },
  {
      "Id": "9b855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Byelorussian"
  },
  {
      "Id": "9d855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cambodian"
  },
  {
      "Id": "9f855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cantonese"
  },
  {
      "Id": "a1855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cape Dutch"
  },
  {
      "Id": "a3855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Castilian"
  },
  {
      "Id": "a5855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Catalan"
  },
  {
      "Id": "a7855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cebuan"
  },
  {
      "Id": "a9855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ceylonese"
  },
  {
      "Id": "ab855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chabacano"
  },
  {
      "Id": "ad855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chaldean"
  },
  {
      "Id": "af855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cham"
  },
  {
      "Id": "b1855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chamba"
  },
  {
      "Id": "b3855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chang Chow"
  },
  {
      "Id": "b5855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chavacano"
  },
  {
      "Id": "b7855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chechen"
  },
  {
      "Id": "b9855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cheremis"
  },
  {
      "Id": "bb855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chewa"
  },
  {
      "Id": "bd855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chichewa"
  },
  {
      "Id": "bf855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chikaranga"
  },
  {
      "Id": "c1855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chimbu"
  },
  {
      "Id": "1248d306-748f-e211-96e1-00155d0a0f05",
      "Name": "Chin"
  },
  {
      "Id": "c3855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chinchchou"
  },
  {
      "Id": "c5855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chinese"
  },
  {
      "Id": "c7855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chokwe"
  },
  {
      "Id": "c9855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Chuvash"
  },
  {
      "Id": "cb855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cook Island"
  },
  {
      "Id": "cd855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cornish"
  },
  {
      "Id": "cf855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Creole"
  },
  {
      "Id": "d1855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Crioulo"
  },
  {
      "Id": "d3855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Croatian"
  },
  {
      "Id": "d5855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Cymric"
  },
  {
      "Id": "d7855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Da Njong Ka"
  },
  {
      "Id": "d9855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Dahomey"
  },
  {
      "Id": "db855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Daie"
  },
  {
      "Id": "dd855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Danish"
  },
  {
      "Id": "df855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Dari"
  },
  {
      "Id": "e1855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Deaf"
  },
  {
      "Id": "e3855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Dinka"
  },
  {
      "Id": "e5855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Divehi"
  },
  {
      "Id": "e7855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Duala"
  },
  {
      "Id": "e9855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Dutch"
  },
  {
      "Id": "eb855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Dyula"
  },
  {
      "Id": "ed855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Dzonkha"
  },
  {
      "Id": "ef855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Eesti Keel"
  },
  {
      "Id": "f1855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Efik"
  },
  {
      "Id": "f3855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "English"
  },
  {
      "Id": "15865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "English"
  },
  {
      "Id": "f5855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Erse"
  },
  {
      "Id": "f7855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Estonian"
  },
  {
      "Id": "f9855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Euskara"
  },
  {
      "Id": "fb855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ewe"
  },
  {
      "Id": "fd855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Faeroese"
  },
  {
      "Id": "ff855436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Fang"
  },
  {
      "Id": "01865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Fante"
  },
  {
      "Id": "03865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Faroese"
  },
  {
      "Id": "05865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Farsi"
  },
  {
      "Id": "07865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Fijian"
  },
  {
      "Id": "09865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Filipino"
  },
  {
      "Id": "0b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Finnish"
  },
  {
      "Id": "0d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Flemish"
  },
  {
      "Id": "0f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Fon"
  },
  {
      "Id": "11865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Foo Chow"
  },
  {
      "Id": "13865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Formosan"
  },
  {
      "Id": "17865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Friesian"
  },
  {
      "Id": "19865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Friulian"
  },
  {
      "Id": "1b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Fuchow"
  },
  {
      "Id": "1d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Fulani"
  },
  {
      "Id": "d48b015d-b4c0-e111-bdd5-00155d0a0f05",
      "Name": "FUR"
  },
  {
      "Id": "1f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ga"
  },
  {
      "Id": "21865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gaddang"
  },
  {
      "Id": "23865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gaeilge"
  },
  {
      "Id": "25865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gaelic, Ireland"
  },
  {
      "Id": "27865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gaelic, Scotland"
  },
  {
      "Id": "29865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Galician"
  },
  {
      "Id": "2b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Galla"
  },
  {
      "Id": "2d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ganda"
  },
  {
      "Id": "2f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Garhwali"
  },
  {
      "Id": "31865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Georgian"
  },
  {
      "Id": "da05d627-e0ed-de11-bc94-00155d0a121f",
      "Name": "German"
  },
  {
      "Id": "35865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ghanaian"
  },
  {
      "Id": "37865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gilbertese"
  },
  {
      "Id": "39865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gondi"
  },
  {
      "Id": "3b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gorantolo"
  },
  {
      "Id": "3d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Greek"
  },
  {
      "Id": "3f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Greenlandic"
  },
  {
      "Id": "41865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Guarani"
  },
  {
      "Id": "43865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Guinean"
  },
  {
      "Id": "45865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gujarati"
  },
  {
      "Id": "47865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gurage"
  },
  {
      "Id": "49865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gurkhali"
  },
  {
      "Id": "4b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gurma"
  },
  {
      "Id": "4d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gusii"
  },
  {
      "Id": "4f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gutob"
  },
  {
      "Id": "51865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Guyanese"
  },
  {
      "Id": "53865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Gypsy"
  },
  {
      "Id": "55865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hainanese"
  },
  {
      "Id": "57865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Haitian"
  },
  {
      "Id": "59865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Haka"
  },
  {
      "Id": "5b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hakah"
  },
  {
      "Id": "5d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Halang"
  },
  {
      "Id": "5f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Halia"
  },
  {
      "Id": "61865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Harari"
  },
  {
      "Id": "63865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hausa"
  },
  {
      "Id": "65865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hawaiian"
  },
  {
      "Id": "c8c3c11f-6eb5-e311-ab03-00155d0a0f05",
      "Name": "Hazaragi"
  },
  {
      "Id": "67865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hebrew"
  },
  {
      "Id": "69865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hiligaynon"
  },
  {
      "Id": "6b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hindi"
  },
  {
      "Id": "6d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hmong"
  },
  {
      "Id": "6f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hokka"
  },
  {
      "Id": "71865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hokkien"
  },
  {
      "Id": "73865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hre"
  },
  {
      "Id": "75865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hrvatski"
  },
  {
      "Id": "77865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Huli"
  },
  {
      "Id": "79865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hunan"
  },
  {
      "Id": "7b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Hungarian"
  },
  {
      "Id": "7d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "I Kiribati"
  },
  {
      "Id": "7f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Iban"
  },
  {
      "Id": "81865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ibo"
  },
  {
      "Id": "83865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Icelandic"
  },
  {
      "Id": "85865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Idisch"
  },
  {
      "Id": "87865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ifugao"
  },
  {
      "Id": "89865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Igbo"
  },
  {
      "Id": "8b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Igorot"
  },
  {
      "Id": "8d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ikiribati"
  },
  {
      "Id": "8f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ilocano"
  },
  {
      "Id": "91865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ilongo"
  },
  {
      "Id": "93865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Indigenous"
  },
  {
      "Id": "95865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Indonesian"
  },
  {
      "Id": "97865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ingush"
  },
  {
      "Id": "99865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Interlingua"
  },
  {
      "Id": "9b865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Iranian"
  },
  {
      "Id": "9d865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Irish"
  },
  {
      "Id": "9f865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Irish Gaelic"
  },
  {
      "Id": "a1865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Istro Romanian"
  },
  {
      "Id": "a3865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Italian"
  },
  {
      "Id": "a5865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Jamaican"
  },
  {
      "Id": "d805d627-e0ed-de11-bc94-00155d0a121f",
      "Name": "Japanese"
  },
  {
      "Id": "a9865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Jarai"
  },
  {
      "Id": "ab865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Javanese"
  },
  {
      "Id": "ad865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Jeh"
  },
  {
      "Id": "af865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Jinga"
  },
  {
      "Id": "b1865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Judezmo"
  },
  {
      "Id": "b3865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Jui"
  },
  {
      "Id": "b5865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kabyle"
  },
  {
      "Id": "b7865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kadazan"
  },
  {
      "Id": "b9865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kalami"
  },
  {
      "Id": "bb865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kalinga"
  },
  {
      "Id": "bd865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kam Tai"
  },
  {
      "Id": "bf865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kamba"
  },
  {
      "Id": "c1865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kampuchean"
  },
  {
      "Id": "c3865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kan"
  },
  {
      "Id": "c5865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kanarese"
  },
  {
      "Id": "c7865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kankanaey"
  },
  {
      "Id": "c9865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kannada"
  },
  {
      "Id": "cb865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kanuri"
  },
  {
      "Id": "cd865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kapampangan"
  },
  {
      "Id": "cf865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Karelian"
  },
  {
      "Id": "d1865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Karen"
  },
  {
      "Id": "d3865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kashmiri"
  },
  {
      "Id": "d5865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kate"
  },
  {
      "Id": "d7865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Katheravousa"
  },
  {
      "Id": "d9865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Katu"
  },
  {
      "Id": "db865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kazakh"
  },
  {
      "Id": "dd865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kenyan"
  },
  {
      "Id": "df865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khalkha"
  },
  {
      "Id": "e1865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khandeshi"
  },
  {
      "Id": "e3865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kharia"
  },
  {
      "Id": "e5865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khasi"
  },
  {
      "Id": "e7865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khmer"
  },
  {
      "Id": "e9865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khmu"
  },
  {
      "Id": "eb865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khoisan"
  },
  {
      "Id": "ed865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Khorcin"
  },
  {
      "Id": "ef865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kia"
  },
  {
      "Id": "f1865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kikamba"
  },
  {
      "Id": "f3865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kikongo"
  },
  {
      "Id": "f5865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kikuyu"
  },
  {
      "Id": "f7865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kinya Rwanda"
  },
  {
      "Id": "f9865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kirgiz"
  },
  {
      "Id": "fb865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kiribati"
  },
  {
      "Id": "fd865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kirundi"
  },
  {
      "Id": "ff865436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kishaka"
  },
  {
      "Id": "01875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kissi"
  },
  {
      "Id": "03875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kiswahili"
  },
  {
      "Id": "05875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kiwai"
  },
  {
      "Id": "07875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Koda"
  },
  {
      "Id": "09875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Koho"
  },
  {
      "Id": "0b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kolami"
  },
  {
      "Id": "0d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kongo"
  },
  {
      "Id": "0f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Konkani"
  },
  {
      "Id": "11875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Korean"
  },
  {
      "Id": "13875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Koya"
  },
  {
      "Id": "15875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kreole"
  },
  {
      "Id": "17875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Krio"
  },
  {
      "Id": "19875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kui"
  },
  {
      "Id": "1b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kumauni"
  },
  {
      "Id": "1d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kurdish"
  },
  {
      "Id": "1f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Kurukh"
  },
  {
      "Id": "21875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ladin"
  },
  {
      "Id": "23875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ladino"
  },
  {
      "Id": "25875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Laghu"
  },
  {
      "Id": "27875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lampung"
  },
  {
      "Id": "29875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Landsmal"
  },
  {
      "Id": "2b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lango"
  },
  {
      "Id": "2d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Laos"
  },
  {
      "Id": "2f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lapp"
  },
  {
      "Id": "31875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Latvian"
  },
  {
      "Id": "33875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lettish"
  },
  {
      "Id": "35875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Letzeburgesch"
  },
  {
      "Id": "37875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Li"
  },
  {
      "Id": "39875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Liberian"
  },
  {
      "Id": "3b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lingala"
  },
  {
      "Id": "3d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lisu"
  },
  {
      "Id": "3f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lithuanian"
  },
  {
      "Id": "41875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Little Russian"
  },
  {
      "Id": "43875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Losengo"
  },
  {
      "Id": "45875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Luba"
  },
  {
      "Id": "47875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ludic"
  },
  {
      "Id": "49875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Luganda"
  },
  {
      "Id": "4b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Luhya"
  },
  {
      "Id": "4d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Luo"
  },
  {
      "Id": "4f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lusatian"
  },
  {
      "Id": "51875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Luxembourgish"
  },
  {
      "Id": "53875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Lwo"
  },
  {
      "Id": "55875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Macedonian"
  },
  {
      "Id": "57875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Macedo-Romanian"
  },
  {
      "Id": "59875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Madi"
  },
  {
      "Id": "5b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Madurese"
  },
  {
      "Id": "5d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Magindanao"
  },
  {
      "Id": "5f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Magyar"
  },
  {
      "Id": "61875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Maithili"
  },
  {
      "Id": "63875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Makaton"
  },
  {
      "Id": "65875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Makedonski"
  },
  {
      "Id": "67875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Makonde"
  },
  {
      "Id": "69875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malagasay"
  },
  {
      "Id": "6b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malagasy"
  },
  {
      "Id": "6d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malawian"
  },
  {
      "Id": "6f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malayalam"
  },
  {
      "Id": "71875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malaysian"
  },
  {
      "Id": "73875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Maldivian"
  },
  {
      "Id": "75875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Maltese"
  },
  {
      "Id": "77875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malto"
  },
  {
      "Id": "79875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Malvi"
  },
  {
      "Id": "7b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Manchu"
  },
  {
      "Id": "7d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mandarin"
  },
  {
      "Id": "7f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Manipuri"
  },
  {
      "Id": "81875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mano"
  },
  {
      "Id": "83875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Manx"
  },
  {
      "Id": "85875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Maori"
  },
  {
      "Id": "87875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Marano"
  },
  {
      "Id": "89875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Marathi"
  },
  {
      "Id": "8b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Marova"
  },
  {
      "Id": "8d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Marshallese"
  },
  {
      "Id": "c989a4af-36fd-e611-8100-00155d03cc3a",
      "Name": "Martu"
  },
  {
      "Id": "8f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Masai"
  },
  {
      "Id": "91875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mashona"
  },
  {
      "Id": "93875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mauritian Creole"
  },
  {
      "Id": "95875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Melanesian"
  },
  {
      "Id": "97875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mende"
  },
  {
      "Id": "99875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mendi"
  },
  {
      "Id": "9b875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Meo"
  },
  {
      "Id": "9d875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mewari"
  },
  {
      "Id": "9f875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Miao"
  },
  {
      "Id": "a1875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Micronesian"
  },
  {
      "Id": "a3875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mien"
  },
  {
      "Id": "a5875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Minangkabau"
  },
  {
      "Id": "a7875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mnong"
  },
  {
      "Id": "a9875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Moldavian"
  },
  {
      "Id": "ab875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mon"
  },
  {
      "Id": "ad875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mongol"
  },
  {
      "Id": "af875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Montenegrin"
  },
  {
      "Id": "b1875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "More"
  },
  {
      "Id": "b3875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mossi"
  },
  {
      "Id": "b5875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Motu"
  },
  {
      "Id": "b7875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Munda"
  },
  {
      "Id": "b9875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mundari"
  },
  {
      "Id": "bb875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Muong"
  },
  {
      "Id": "bd875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Mute"
  },
  {
      "Id": "bf875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nauruan"
  },
  {
      "Id": "c1875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ndebele"
  },
  {
      "Id": "c3875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Neo Melanesian"
  },
  {
      "Id": "c5875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nepalese"
  },
  {
      "Id": "c7875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nepali"
  },
  {
      "Id": "c9875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "New Caledonian Pidgin French"
  },
  {
      "Id": "cb875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "New Zealand Maori"
  },
  {
      "Id": "cd875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ngalum"
  },
  {
      "Id": "cf875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nguni"
  },
  {
      "Id": "d1875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nilotic"
  },
  {
      "Id": "d3875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nipon"
  },
  {
      "Id": "d5875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Niue"
  },
  {
      "Id": "d7875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Niuean"
  },
  {
      "Id": "d9875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Non Verbal"
  },
  {
      "Id": "db875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nor"
  },
  {
      "Id": "dd875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Norfolk English"
  },
  {
      "Id": "df875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Norsk"
  },
  {
      "Id": "e1875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Norwegian"
  },
  {
      "Id": "e3875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nubian"
  },
  {
      "Id": "e5875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nuer"
  },
  {
      "Id": "e7875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "NULL"
  },
  {
      "Id": "e9875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nuristani"
  },
  {
      "Id": "eb875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nyamwesi"
  },
  {
      "Id": "ed875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nyang"
  },
  {
      "Id": "ef875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Nynorsk"
  },
  {
      "Id": "f1875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Occitan"
  },
  {
      "Id": "f3875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Oriya"
  },
  {
      "Id": "f5875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Orokaiva"
  },
  {
      "Id": "f7875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Oromo"
  },
  {
      "Id": "f9875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ossetic"
  },
  {
      "Id": "4a6f44e7-1445-ed11-bba3-00224818a733",
      "Name": "Other"
  },
  {
      "Id": "fb875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pacoh"
  },
  {
      "Id": "fd875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Paiwan"
  },
  {
      "Id": "ff875436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pakhto"
  },
  {
      "Id": "01885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Palauan"
  },
  {
      "Id": "03885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Palaung"
  },
  {
      "Id": "05885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pampangan"
  },
  {
      "Id": "07885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pangasinan"
  },
  {
      "Id": "09885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Panjabi"
  },
  {
      "Id": "0b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pao An"
  },
  {
      "Id": "0d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Papiamento"
  },
  {
      "Id": "0f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Papuan"
  },
  {
      "Id": "11885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pashto"
  },
  {
      "Id": "13885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pedi"
  },
  {
      "Id": "15885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Peguan"
  },
  {
      "Id": "ba0edb3e-d719-df11-a8ca-00155d038e14",
      "Name": "Persian"
  },
  {
      "Id": "19885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Philippino"
  },
  {
      "Id": "1b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pho"
  },
  {
      "Id": "1d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pidgeon"
  },
  {
      "Id": "1f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pijin"
  },
  {
      "Id": "21885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pisa"
  },
  {
      "Id": "23885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pitcairnese"
  },
  {
      "Id": "27885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Polish"
  },
  {
      "Id": "29885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Polski"
  },
  {
      "Id": "2b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Polynesian"
  },
  {
      "Id": "fc49d844-d719-df11-a8ca-00155d038e14",
      "Name": "Portuguese"
  },
  {
      "Id": "2f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Punjabi"
  },
  {
      "Id": "31885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Pushto"
  },
  {
      "Id": "33885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Putonghua"
  },
  {
      "Id": "35885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Puyi"
  },
  {
      "Id": "37885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Quechua"
  },
  {
      "Id": "39885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rade"
  },
  {
      "Id": "3b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rajasthani"
  },
  {
      "Id": "3d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rarotongan"
  },
  {
      "Id": "3f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ratuman"
  },
  {
      "Id": "41885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rawang"
  },
  {
      "Id": "43885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rengao"
  },
  {
      "Id": "45885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rhaetian"
  },
  {
      "Id": "47885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Riff"
  },
  {
      "Id": "49885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Riksmal"
  },
  {
      "Id": "4b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Romanian"
  },
  {
      "Id": "4d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Romansch"
  },
  {
      "Id": "4f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Romany"
  },
  {
      "Id": "51885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ronga"
  },
  {
      "Id": "53885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Roro"
  },
  {
      "Id": "55885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rotuman"
  },
  {
      "Id": "57885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Roviania"
  },
  {
      "Id": "59885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rumanian"
  },
  {
      "Id": "5b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Rundi"
  },
  {
      "Id": "5d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Russian"
  },
  {
      "Id": "5f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ruthenian"
  },
  {
      "Id": "61885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Saami"
  },
  {
      "Id": "63885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Samarleyte"
  },
  {
      "Id": "65885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Samoan"
  },
  {
      "Id": "67885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sango"
  },
  {
      "Id": "69885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sanskrit"
  },
  {
      "Id": "6b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Santa"
  },
  {
      "Id": "6d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Scottish Gaelic"
  },
  {
      "Id": "6f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sechyelles Creole"
  },
  {
      "Id": "71885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sedang"
  },
  {
      "Id": "73885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Senegalese"
  },
  {
      "Id": "75885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Serbian"
  },
  {
      "Id": "77885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Serer"
  },
  {
      "Id": "79885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sesothoian"
  },
  {
      "Id": "7b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Setswana"
  },
  {
      "Id": "7d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shanghai"
  },
  {
      "Id": "7f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shanghainese"
  },
  {
      "Id": "81885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shilan"
  },
  {
      "Id": "83885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shilluk"
  },
  {
      "Id": "85885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shluh"
  },
  {
      "Id": "87885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shona"
  },
  {
      "Id": "89885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Shqip"
  },
  {
      "Id": "8b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Siamese"
  },
  {
      "Id": "8d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sidamo"
  },
  {
      "Id": "8f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sign Language"
  },
  {
      "Id": "91885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Signed English"
  },
  {
      "Id": "93885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sikaiana"
  },
  {
      "Id": "95885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sikkamese"
  },
  {
      "Id": "97885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sinanese"
  },
  {
      "Id": "99885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sindhi"
  },
  {
      "Id": "9b885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Singalese"
  },
  {
      "Id": "9d885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sinhala"
  },
  {
      "Id": "9f885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sinhalais"
  },
  {
      "Id": "a1885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sinhalese"
  },
  {
      "Id": "a3885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sinitic"
  },
  {
      "Id": "a5885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Siswati"
  },
  {
      "Id": "a7885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Slavic"
  },
  {
      "Id": "a9885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Slavonic"
  },
  {
      "Id": "ab885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Slovak"
  },
  {
      "Id": "ad885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Slovene"
  },
  {
      "Id": "af885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Slovenian"
  },
  {
      "Id": "b1885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Solomon Islands Pidgeon"
  },
  {
      "Id": "b3885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Somali"
  },
  {
      "Id": "b5885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Songhai"
  },
  {
      "Id": "b7885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sorbian"
  },
  {
      "Id": "b9885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sotho"
  },
  {
      "Id": "3bd3f8c7-aaee-de11-bc94-00155d0a121f",
      "Name": "Spanish"
  },
  {
      "Id": "bd885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Srpski"
  },
  {
      "Id": "bf885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Stieng"
  },
  {
      "Id": "c1885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Sudanese"
  },
  {
      "Id": "c3885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Suisse"
  },
  {
      "Id": "c5885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Suomi"
  },
  {
      "Id": "c7885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Svensk"
  },
  {
      "Id": "c9885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Swahili"
  },
  {
      "Id": "cb885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Swazi"
  },
  {
      "Id": "cd885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Swedish"
  },
  {
      "Id": "cf885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Swiss French"
  },
  {
      "Id": "d1885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tadjik"
  },
  {
      "Id": "d3885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tagalog"
  },
  {
      "Id": "d5885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tahitian"
  },
  {
      "Id": "d7885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tai"
  },
  {
      "Id": "d9885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Taiwanese"
  },
  {
      "Id": "db885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tajik"
  },
  {
      "Id": "dd885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tamil"
  },
  {
      "Id": "df885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tanzanian"
  },
  {
      "Id": "e1885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tartar"
  },
  {
      "Id": "e3885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tatar"
  },
  {
      "Id": "e5885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Telugu"
  },
  {
      "Id": "e7885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Temne"
  },
  {
      "Id": "e9885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Teo Chew"
  },
  {
      "Id": "eb885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Teochew"
  },
  {
      "Id": "ed885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Teso"
  },
  {
      "Id": "ef885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tetum"
  },
  {
      "Id": "f1885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Thai"
  },
  {
      "Id": "f3885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tho"
  },
  {
      "Id": "f5885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tibetan"
  },
  {
      "Id": "f7885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tie Chiw"
  },
  {
      "Id": "6296ca46-25fe-e211-8134-00155d0a0f05",
      "Name": "Tigrina"
  },
  {
      "Id": "f9885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tigrinya"
  },
  {
      "Id": "fb885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Timorese"
  },
  {
      "Id": "fd885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tiv"
  },
  {
      "Id": "ff885436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "To Chu"
  },
  {
      "Id": "01895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Toaripi"
  },
  {
      "Id": "03895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tochew"
  },
  {
      "Id": "05895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Toda"
  },
  {
      "Id": "07895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tok Pisin"
  },
  {
      "Id": "09895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tokelau"
  },
  {
      "Id": "0b895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tokelauan"
  },
  {
      "Id": "0d895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tongan"
  },
  {
      "Id": "0f895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Triprui"
  },
  {
      "Id": "11895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tsakonian"
  },
  {
      "Id": "13895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tsonga"
  },
  {
      "Id": "15895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tswana"
  },
  {
      "Id": "17895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tulu"
  },
  {
      "Id": "19895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tungus"
  },
  {
      "Id": "1b895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tupi"
  },
  {
      "Id": "1d895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Turkish"
  },
  {
      "Id": "1f895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Turkmen"
  },
  {
      "Id": "21895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Tuvaluan"
  },
  {
      "Id": "23895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Twi"
  },
  {
      "Id": "25895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ugandan"
  },
  {
      "Id": "27895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Uighur"
  },
  {
      "Id": "29895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Ukrainian"
  },
  {
      "Id": "2b895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Urdu"
  },
  {
      "Id": "2d895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Urdu Hindustani"
  },
  {
      "Id": "2f895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Uzbek"
  },
  {
      "Id": "31895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Vietnamese"
  },
  {
      "Id": "33895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Visayan"
  },
  {
      "Id": "35895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Vlach"
  },
  {
      "Id": "37895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Walamo"
  },
  {
      "Id": "39895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Walloon"
  },
  {
      "Id": "3b895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Waray"
  },
  {
      "Id": "3d895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Welsh"
  },
  {
      "Id": "3f895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Wen Tcheou"
  },
  {
      "Id": "41895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Wendish"
  },
  {
      "Id": "43895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Wolof"
  },
  {
      "Id": "45895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Wu"
  },
  {
      "Id": "47895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Xhosa"
  },
  {
      "Id": "49895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Yao"
  },
  {
      "Id": "4b895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Yiddish"
  },
  {
      "Id": "4d895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Yoruba"
  },
  {
      "Id": "4f895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Yue"
  },
  {
      "Id": "51895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Zambian"
  },
  {
      "Id": "53895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Zande"
  },
  {
      "Id": "55895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Zealand"
  },
  {
      "Id": "57895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Zimbabwean"
  },
  {
      "Id": "59895436-b2ec-e011-84f9-00155d0a0f06",
      "Name": "Zulu"
  }
];

let val = '';
let isValid = '';
let count = '';
let updated = Date.now();

const getLangFilter = (langList) => (input) => {
  const str = input.trim().toLowerCase();
  return langList.filter((lang) => lang.Name.toLowerCase().includes(str))
    .map((lang) => lang.Name);
};

const langFilter = getLangFilter(languageList);

const handleBlur = (event) => {
  console.group('handleBlur()');
  console.log('event:', event);
  console.log('event.target:', event.target);
  console.log('event.target.value:', event.target.value);
  console.log('isValid:', isValid);
  console.log('count:', count);
  console.log('val (before):', val);

  if (isValid === true) {
    val = event.target.value;
  } else {
    val = '';
    updated = Date.now();
  }


    console.log('val (after):', val);
  console.groupEnd();
}
const handleSubmit = (event) => {
  console.group('handleSubmit()');
  console.log('event:', event);
  val = event;
  console.groupEnd();
}
const handleIsValid = (event) => {
  console.group('handleIsValid()');
  console.log('event:', event);
  console.log('isValid (before):', isValid);
  console.log('count:', count);
  console.log('val:', val);
  isValid = event;
  console.log('isValid (after):', isValid);
  console.groupEnd();
}
const handleMatched = (event) => {
  console.group('handleMatched()');
  console.log('event:', event);
  console.log('isValid:', isValid);
  console.log('count (before):', count);
  console.log('val:', val);
  count = event;
  console.log('count (after):', count);
  console.groupEnd();
}

</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
