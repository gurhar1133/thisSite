<script>
    import Textfield from "./Textfield.svelte";
    import Button from "./Button.svelte";
    import {slide} from "svelte/transition";
    import {createEventDispatcher} from "svelte";

    const dispatch = createEventDispatcher();

    let closeLetter = false;

    $: if (closeLetter) {
    
    }
</script>
<style>
    .contact{
        text-align: center;
        margin-left: -1rem;
        
        
    }
    .message{
        border: 2px solid rgb(65, 133, 228);
        border-top-right-radius: 20px;
        border-bottom-left-radius: 20px;
    }
    .message:focus{
        outline: none;
        background-color: #eee;
    }
    @media (max-width: 800px ){
        .contact{
            margin-top: -4rem;
        }
    }
</style>

<div class="border-1 border-gray-400 contact rounded text-center bg-white w-screen p-8 pt-0 pb-0">
    
    {#if !closeLetter}
    <div class="bg-blue-600 p-2 rounded-b-lg shadow-md">
    <p class="text-white"> Send me a message and lets make something great!</p>
    </div>

    {:else if  closeLetter}
        <div in:slide={{duration: 800}} class="bg-blue-600 w-full h-48 fixed rounded-b-lg shadow-md">
        
        </div>
    {/if}

    <hr>
    <br>
    Email: <Textfield />
    <br>
    Name: <Textfield />
    <br><br>
    Message:
    <textarea class="message shadow-md" cols="37" rows="8"></textarea>
    <br>
    <Button on:click={()=>{ 
        closeLetter = true;
        dispatch("sent");
    }} rounded={true} btnText="confirm" color="primary"/>
   {#if  closeLetter}
        <div in:slide={{duration: 800}} class="bg-blue-600 w-full h-56 absolute bottom-0 rounded-t-lg shadow-md">
            
        </div>
    {/if}
</div>