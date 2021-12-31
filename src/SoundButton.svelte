<script>
	export let path = "";
    // ;// = {"name":"","url":"https://www.myinstants.com/media/sounds/owenwowson5.mp3"};
    export let title = "";
	import TrackHeading from './TrackHeading.svelte';
 	import Controls from './Controls.svelte';
import { onMount } from 'svelte';
	
     $: loading = false;
	// Get Audio track
	let trackIndex = 0;
	// $: console.log(trackIndex)
	let audioFile =new Audio(path);
    audioFile.preload = "auto"
	let trackTitle = title;
	
	const loadTrack = () => {
		audioFile = new Audio(path);
		audioFile.onloadedmetadata = () => {
 			updateTime();
		}
        
		trackTitle = title;
	}
	 
	
	  
	 
	let trackTimer;
	
	function updateTime() {
		 
		
		if (audioFile.ended) {
			toggleTimeRunning();
		}
	}
	
	const toggleTimeRunning = () => {
		if (audioFile.ended) {
			isPlaying = false;
			clearInterval(trackTimer);
			console.log(`Ended = ${audioFile.ended}`);	
		} else {
			trackTimer = setInterval(updateTime, 100);
		}
	}
	

	// Controls
	let isPlaying = false;
	$: console.log(`isPlaying = ${isPlaying}`)
	
	const playPauseAudio = () => {
		if (audioFile.paused) {
			toggleTimeRunning()
			audioFile.play();
			isPlaying = true;
		} else {
			toggleTimeRunning()
			audioFile.pause();
			isPlaying = false;
		}	 	
	}
	 
	
	// Playlist
	const handleTrack = (e) => {
		if (!isPlaying) {
			trackIndex = Number(e.target.dataset.trackId);
			loadTrack();
			playPauseAudio(); // auto play
		} else {
			isPlaying = false;
			audioFile.pause();
 			loadTrack();
			playPauseAudio(); // auto play
		}
	}
    onMount(()=>{
        loadTrack()
    })
</script>


<main>
	<section id="player-cont">
		
		<TrackHeading {trackTitle} />

		
		<Controls {isPlaying} 
							on:playPause={playPauseAudio} />
		
	</section>
	
</main>


<style>
	

	#player-cont {
		width: 96px;
		height: 170px;
		padding: .7rem 1.5rem 0;
		box-shadow: 0 0 5px black;
		background: #222;
		color: #bbb;
		border-radius: 5px 5px 0 0;
	}		
</style>