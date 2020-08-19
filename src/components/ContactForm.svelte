<script>
    import Textfield from "./Textfield.svelte";
    import Button from "./Button.svelte";
    import {createEventDispatcher} from "svelte";

    const dispatch = createEventDispatcher();
</script>
<style>
    .contact{
        text-align: center;
        margin-left: -1rem;
        
    }
    @media (max-width: 800px ){
        .contact{
            margin-top: -4rem;
        }
    }
</style>

<div class="border-1 border-gray-400 contact rounded text-center bg-white w-screen p-20">
    Send me a message. Let's make something great!
    <hr>
    <br>
    Email: <Textfield />
    <br>
    Name: <Textfield />
    <br>
    Message:
    <textarea></textarea>
    <br>
    <Button on:click={()=>{dispatch("sendForm")}} rounded={true} outline={true} btnText="send" color="primary"/>
</div>