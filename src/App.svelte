<script>
import Three from "./three.svelte";
let songSave = null;
let checked = false
let getNothing = false
let errorMessage = ''
function song(event){
	event.preventDefault();
		if (songSave) {
			console.log(songSave);
			checked = true;
			console.log(checked);
		} else {
			getNothing =true
			errorMessage = "Veuillez remplir le champ."
			console.log(getNothing)
		}
}
</script>



{#if !checked}

<div class="container">
	<div class="row">
		<div class="col-12" id="getSong">
			<form on:submit|preventDefault={song}>
				<label for="formFileLg" class="form-label">Mettez une musique</label>
				<input class="form-control form-control-lg" id="formFileLg" type="file" bind:value={songSave}>
				{#if getNothing}
				<p class="text-danger">{errorMessage}</p>
				{/if}
				<button type="submit" class="my-5">Envoyer</button>
				
			</form>
		</div>
	</div>
</div>
	{:else if checked}
	<div class="container">
		<div class="row">
			<div id="getSong">
				<h1 class="text-light">Votre Musique : {songSave}</h1>
				<Three />
			</div>
		</div>
	</div>
	
{/if}
