<template>
  
  <section class="h-full bg-slate-800">
  
  <div class="h-16 flex border">
    <p class="flex text-center items-center text-white">Editing Section</p>
  </div>
  
  <div class="h-auto flex justify-center items-center border">
    <div class="h-72 w-2/5 rounded-xl bg-gray-300 flex" id="videoselect">
      <video class="h-36" id="video01" ></video>
      <video class="h-36" id="video02"></video>
    </div>
  </div>
  
  <div class="p-2 border-1 flex justify-center">
    <button class="bg-yellow-300 p-3 flex items-center h-12" id="play">Play</button>
  </div>
 
  <div class="border-2 flex h-full" id="container">
    <!-- <div class="w-full">
      <div class="border-2 w-full" id="waveform01"></div>
      <div class="border-2 w-full" id="waveform02"></div>  
    </div> -->
  </div>
  <div class="h-8 border"></div>
  </section>
</template>

<script setup>
import WaveSurfer from 'wavesurfer.js';
import WaveSurferMultitrack from 'wavesurfer-multitrack';

var c_btn = ref(0)

onMounted(() => {
  const multitrack = WaveSurferMultitrack.create(
    [
      {
        id:0,
      },
      {
      id: 1,
      draggable: true,
      startPosition: 0, // start time relative to the entire multitrack
      url: '/Jazz-01-Piano_120.mp4',
      envelope: true,
      volume: 1,
      fadeInEnd: 2,
      fadeOutStart: 72,
      options: {
        waveColor: 'hsl(46, 87%, 49%)',
        progressColor: 'hsl(46, 87%, 20%)',
      },
      barRadius: 4,
      barWidth: 4,
    },
    {
      id: 2,
      draggable: true,
      startPosition: 0,
      // startCue: 1,
      // endCue: 75,
      // fadeInEnd: 2,
      // fadeOutStart: 72,
      // envelope: [
      //   { time: 11.2, volume: 0.5 },
      //   { time: 13.5, volume: 0.8 },
      // ],
      volume: 0.8,
      options: {
        waveColor: 'hsl(161, 87%, 49%)',
        progressColor: 'hsl(161, 87%, 20%)',
      },
      url: '/Jazz-03-Saxophone_120.mp4',
      barRadius: 4,
      barWidth: 4,
    },
    {
      id:3,
    }
  ],
  {
    media: document.getElementById('videoselect'), 
    container: document.querySelector('#container'), // required!
    minPxPerSec: 60, // zoom level
    rightButtonDrag: false, // set to true to drag with right mouse button
    cursorWidth: 2,
    cursorColor: '#D72F21',
    trackBackground: 'bg-slate-700',
    trackBorderColor: '#7C7C7C',
    dragBounds: true,
    // envelopeOptions: {
    //   lineColor: 'rgba(255, 0, 0, 0.7)',
    //   lineWidth: 4,
    //   dragPointSize: 8,
    //   dragPointFill: 'rgba(255, 255, 255, 0.8)',
    //   dragPointStroke: 'rgba(255, 255, 255, 0.3)',
    // },
  })

    const button = document.querySelector('#play')
      button.disabled = true
      multitrack.once('canplay', () => {
      button.disabled = false
      button.onclick = () => {
        multitrack.isPlaying() ? multitrack.pause() : multitrack.play()
        button.textContent = multitrack.isPlaying() ? 'Pause' : 'Play'
      }
    })
})
</script>

<style scoped>
</style>
