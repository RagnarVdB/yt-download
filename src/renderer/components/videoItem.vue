<template>
  <div
    id="item"
    tabindex="-1"
    @focus="$emit('current', video)"
    v-bind:class="{ selected: video.id === current }"
  >
    <div id="title">
      <p>{{ video.title }}</p>
    </div>
    <div id="progress">
      <div :style="{width: video.progress + '%'}" v-bind:class="{ indeterminate: video.progress === 'indeterminate' }" />
    </div>
    <p id="ext">
      {{ video.settings.ext }}
    </p>
    <p
      v-if="video.settings.type === 'video'"
      id="quality"
    >
      {{ video.settings.quality }}
    </p>
    <button @click="$emit('del-video', video.id)">  
      <img src="static/delete.svg">
    </button>
  </div>
</template>

<script>
export default {
  name: 'VideoItem',
  props: ['video', 'current']
}
</script>

<style scoped>
  #item{
    width: 97%;
    height: 60px;
    margin-top: 5px;
    background-color: black;
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-bottom: 10px;
  }
  #item:hover, #item:focus, .selected{
    outline: 2px solid rgb(148, 148, 148);
  }
  #item > p{
    margin-left: 15px;
    font-size: 0.9rem;
    width: 80px;
  }
  #title{
    width: 300px;
    overflow: hidden;
    text-overflow: ellipsis;
    max-height: 39px;
    margin-left: 20px;
  }
  #title p{
    font-size: 0.85rem;
  }
  #progress{
    width: 100%;
    height: 25px;
    background-color: var(--main);
    border-radius: 13px;
    margin-left: 15px;
    overflow: hidden;
  }
  #progress > div{
    background-color: #3869DC;
    height: 100%;
    border-radius: 13px;
  }
  /* Enable class when progress is indeterminate */
  #progress > .indeterminate {
    width: 100% !important ;
    animation: indeterminateAnimation 2s infinite linear;
    transform-origin: 0% 50%;
  }

  @keyframes indeterminateAnimation {
    0% {
      transform:  translateX(0) scaleX(0);
    }
    40% {
      transform:  translateX(0) scaleX(0.4);
    }
    100% {
      transform:  translateX(100%);
    }
  }


  #quality, #ext{
    margin-right: 15px;
    width: 60px;
  }
  #item button{
    margin-right: 15px;
    background: none;
    border: none;
  }

  #item button img{
    width: 18px;
  }
</style>