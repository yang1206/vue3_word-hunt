<template>
  <div class="definitions">
    <p v-if="!props.searchWord" class="tip">Start by typing a word in search ...</p>
    <p v-if="props.searchWord && !result.length" class="tip">这个单词不存在</p>
    <div v-else class="definition" v-for="(definition, index) in result" :key="index">
      <!-- 音标读音 --> 
      <div class="phonetics">
        <span class="phonetic" @click="handleClick(index)">
          {{ definition?.phonetics[0]?.text }}
        </span>
        <i class="iconfont icon-yangshengqi" @click="handleClick(index)" ></i>
        <audio :src="definition?.phonetics[0]?.audio" ref="audio"></audio>
      </div>
     
      
      <div class="meanings">
        <div class="meaning" v-for="(meaning, index) in definition.meanings" :key="index">
          <span class="partOfSpeech">{{ meaning.partOfSpeech }}</span>
          <span class="word-meaning">
            {{ meaning.definitions.map(definition => definition.definition).join(' ') }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { watch, ref } from 'vue'
const props = defineProps({
  searchWord: String
})


//监听props里接收的值
watch(() => props.searchWord, debounce)

const result = ref([])

//使用图标替换原生播放器，监听audio标签，控制播放
const audio = ref()
const handleClick = (index)=>{
  console.log(audio)
  audio.value[index].currentTime = 0;
  audio.value[index].play();
}
let timeout;
let context = this
function debounce(newValue){
  clearTimeout(timeout);
  timeout = setTimeout(function(){
    getData(newValue).apply(context);
  },1000)
  
}
async function getData(newValue) {
  const url = `https://api.dictionaryapi.dev/api/v2/entries/en/${newValue}`
  result.value = []
  try {
    fetch(url)
      .then(response => response.json())
      .then(
        data => {
          result.value =  data
          
        }
      );
  } catch (err) {

  }
}

</script>

<style lang="scss" scoped>
::-webkit-scrollbar {
  width: 5px;
  //background: #282c34;
}

::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.6);
  border-radius: 20px;
}

.definitions {
  border: 10px solid #696969;
  border-radius: 10px;
  height: 60vh;
  padding: 15px;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  gap: 5px;

  .tip {
    font-size: 18px;
  }
  .definition {
    margin-bottom: 10px;
    .phonetics {
      margin-bottom: 10px;
      .phonetic {
        cursor: pointer;
        border-radius: 5px;

        margin-right: 10px;
        &:hover {
          opacity: 0.8;
        }
      }
      .iconfont {
        cursor: pointer;
        &:hover {
          opacity: 0.8;
        }
      }
    }
    &:last-child {
      .meanings {
        border-bottom: none;
      }
    }
    .meanings {
      display: flex;
      flex-direction: column;
      gap: 10px;
      padding-bottom: 10px;
      border-bottom: 1px solid #c5bcbc;

      div.meaning {
        .partOfSpeech {
          margin-right: 10px;
          background-color: #3b3e45;
          opacity: 0.8;
          display: inline-block;
          padding-block: 3px;
          padding-inline: 5px;
          font-size: 14px;
          border-radius: 5px;
          line-height: 25px;
        }
        .word-meaning {
          line-height: 25px;
        }
      }
    }
  }
}
</style>
