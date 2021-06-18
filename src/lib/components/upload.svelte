

<script  >
 let files


 function handlesubmit(){
  const request = new XMLHttpRequest();

    request.open('POST', 'http://localhost:1337/upload');

    request.send(files[0].name);
 }

    
 
	 

 
 
 
</script>
<input type="file" bind:files>

{#if files && files[0]}
	 <button on:click={handlesubmit}>Submit</button>
{/if}