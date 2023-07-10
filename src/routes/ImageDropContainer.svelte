<script lang="ts">
let fileinput = [];

const onFileSelected =(e)=>{
		console.log(...e.target.files)
  let image = e.target.files[0];
            let reader = new FileReader();
            reader.readAsDataURL(image);
            reader.onload = e => {
                 avatar = e.target.result
            };
}
</script>

<div data-id="to-be-ranked-container">
    
    <label for='images'> Add Image: </label>
    <input accept="image/png, image/jpeg" bind:files id='images' multiple name='images' type='file' />
<div class="chan" on:click={()=>{fileinput.click();}}>Choose Image</div>
        <input style="display:none" type="file" accept=".jpg, .jpeg, .png" on:change={(e)=>onFileSelected(e)} bind:this={fileinput} >

    {#if files}
       {#each Array.from(files) as file}
       <p> {file.name} </p>
       {/each} 
    {/if}
</div>
