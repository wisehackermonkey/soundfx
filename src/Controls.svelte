<script>
	import { createEventDispatcher } from 'svelte';
	
	let dispatch = createEventDispatcher();
	
	const icons = {
		play: "https://www.myinstants.com/media/images/transparent_button_normal.png.pagespeed.ce._PQuVSQuHh.png",
		pause: "https://www.myinstants.com/media/images/transparent_button_pressed.png.pagespeed.ce.aQzxIVJ9pw.png"
	}
	
  export let isPlaying;
	
</script>


<div id="btn-cont">
	<button id="play" on:click={() => dispatch('playPause')}>
		<img src={isPlaying ? icons.pause : icons.play} 
				 alt="play"/>
	</button>
</div>

<style>
	
	
	button {
/* 		width: 37px; */
		border: none;
		font-size: 2.3rem;
		padding: 0;
		cursor: pointer;
		margin: 0;
		background-color: transparent;
	}
	
	button:active {
		background-color: transparent;
	}
	
	button img {
		width: 100%;
	}
</style>