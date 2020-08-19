<script>
    import Card from "./Card.svelte";
    import Button from "./Button.svelte";
    import {fly} from "svelte/transition";
    export let absolute = false; 
    export let opacity = .45;
    export let zIndex = "10";
    export let value = false;
    export let flightPath = {duration: 500, y:800};

    let bgOpacity;

    if (opacity >= 0 && opacity < .25){
        bgOpacity = "bg-opacity-25";
    }
    else if (opacity >= .25 && opacity < .50){
         bgOpacity = "bg-opacity-50";
    }
    else if (opacity >= .50 && opacity < 1){
        bgOpacity = "bg-opacity-75";
    }
    else if (opacity >= 1){
        bgOpacity = "bg-opacity-100";
    }
    else{
        console.log('overlay ERROR');
    }
    
    let abs_position = absolute ? "absolute modal-backdrop-abs top-0 left-0 h-full w-full" : "modal-backdrop-full relative";
    let overlay_template = `${abs_position} ${bgOpacity} bg-gray-800`;
    let slot_template = `top-auto left-auto z-50`;

    $: hidden = value ? " block" : " hidden"

</script>
<style>
    .abs{
        top: 0px;
    }
    .modal-backdrop-abs{
        
    }
    .modal-backdrop-full{
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        overflow-y: scroll;
        z-index: 100;
    }
    .slot-content{
       opacity: 10;
        position: absolute; 
        top: 16%;
        margin: 1rem;
        z-index: 100;
      
        
        
    }
    .closer{
      top: 2.6%;
      left: 8%;
      position: fixed;
      z-index: 1000;
    }
    
    @media (min-width: 800px){
      .closer{
        top: 10%;
        left: 48%;
      }
    }

    
</style> 

<div on:click={()=>{
        value = !value;
    }}
    class="{overlay_template + hidden}">
      
 
{#if value}
    <!-- <h4 class="text-gray-200 closer inline cursor-pointer">X</h4> -->
    <div class="closer">
      <Button btnText="X" textMode={true} rounded={true} elevation="sm" color="white" />
    </div>
    <div on:click={()=>{
        value = false;
    }} transition:fly="{flightPath}" class="{`${hidden} slot-content`}"> 
        <slot>
        </slot>
        
    </div>
{/if} 

</div>

