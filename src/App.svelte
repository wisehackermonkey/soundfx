<script>
    import {soundfx} from "./soundfx.js"
 import SoundButton from "./SoundButton.svelte"
   let name = 'world';
   
   let formateFxURL =(fx_name)=>{
       return `https://www.myinstants.com/instant/${fx_name}/embed/`
   }
   let formateAudioUrl = (fx_name)=> `/sound/${fx_name}.mp3`
   let formateSoundObject = (obj)=>{
   obj.url = formateAudioUrl(obj.url )
return obj
}
</script>
<main>
<h1>Sound FX Board by oran</h1>

{#each soundfx as sound}
  <!-- 		 <iframe width="110" height="200" src={formateFxURL(sound.url)} frameborder="0" scrolling="no"></iframe> -->
    <!-- {console.log( formateAudioUrl(sound.url))}  -->
		<SoundButton title={sound.name}  path={formateAudioUrl(sound.url)}/>
{/each}
</main>