<script>
  import Tailwindcss from "./Tailwindcss.svelte";
  import Button from "./components/Button.svelte";
  import Card from "./components/Card.svelte";
  import Overlay from "./components/Overlay.svelte";
  import Carousel from "./components/Carousel.svelte";
  import Chip from "./components/Chip.svelte";
  import {fly} from "svelte/transition";
  import ContactForm from "./components/ContactForm.svelte";
  import Icon from 'svelte-awesome';
  import {onMount} from "svelte";
  import { beer, refresh, comment, codeFork, camera, ban, github, linkedin } from 'svelte-awesome/icons';
  import { faThumbsUp, faThumbsDown} from '@fortawesome/free-regular-svg-icons';

  

  export let name;



  let canvas;
  let particles;
  let mouse;
  onMount(()=>{
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    mouse = {
      x : null,
      y : null,
      radius : (canvas.height/80) * (canvas.height/80)
    };
  })

  function handleMouseMove(event){
    mouse.x = event.x;
    mouse.y = event.y;
    console.log("mouse.x", mouse.x, "mouse.y", mouse.y);
  }

  

  // const ctx = canvas.getContext('2d');
  // canvas.width = window.innerWidth;
  // canvas.height = window.innerHeight;

  
  let hello = "Hello!";
  let preMain = "My name's Gurhar and I am a frontend web developer."
  let mainText = "Lets make awesome stuff!";

  let showProjects = false;
  let showContactForm = false;
  let showBio = false;
  

  let fadeStage = "opacity-0";
  let delayType = "opacity-0";

  setTimeout(()=>{
    delayType = "opacity-1 fadeIn";
  }, 2000);

  setTimeout(()=>{
    fadeStage = "fadeIn";
  }, 4000);
  
  $: if (showBio) {
    preMain = "";
    hello = "";
    mainText = "";
  }

  function sendMessage(){
    setTimeout(()=>{
      console.log("message sent");
      showContactForm = !showContactForm;
      console.log("show", showContactForm);
    }, 700);

  }

  
  
</script>

<style>

  h1 {
    text-transform: uppercase;
    font-size: 5em;
    font-weight: 80;
  }

  p {
    font-size: 1.4em;
    font-weight: 200;
  }

  @media (max-width: 800px){
    h1{
      font-size: 2em;
    }
    p{
      font-size: 1.2em;
    }
    
  }
  .canvas{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #eee;
    z-index: -1000;
  }
  .typewriter {
    overflow: hidden; /* Ensures the content is not revealed until the animation */
    margin: 0 auto; /* Gives that scrolling effect as the typing happens */
    white-space: nowrap; 
    animation: typing 6s steps(300, end), blink-caret .6s step-end infinite;
  }
  
  
  .fadeIn {
    animation: fade-in 3s;
  }

  .scaleIn{
    animation: scale-in .4s ease-out;
  }

  .backgroundImage{
    position: absolute;
    z-index: -1;
    /* position: fixed; */
    top: 0%;
    
    /* transform: translate(-50%, -50%); */
    
    /* background-image: url("https://i.pinimg.com/564x/cb/38/23/cb38236bac66bad44373a6f3f93feba1.jpg"); */
    /* -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover; */
    /* height: 100%; */
    /* background-repeat: no-repeat;
    background-position: center; */
   
  }

  @keyframes scale-in {
    from{
      transform: scale(.2);
      opacity: .5;
    }
    to{
      transform: scale(1);
      opacity: 1;
    }
  }

  @keyframes typing {
    from {
      width: 0;
    }
    to {
      width: 100%;
    }
  }

  @keyframes fade-in{
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>


<canvas  class="canvas" bind:this={canvas} ></canvas>
<Tailwindcss />


<div on:mousemove={handleMouseMove} class="main-container text-blue-700 text-center h-full">
  
  <!-- <div class="backgroundImage">
    <img src="https://imgprx.livejournal.net/3708e8eec0cbca5f20bcf468c1a111ecb1711dc3/M-6EpnphedBDC6oBKeP1w2Pzc0Z54SZMg6j1-VCZAlZYkIrYy4ZLAtvWAuC2GGhqm_5ewkrqx9ErrfWmszlfNDpuDbtqTgM9WwHoTJkA6tU" />
  </div> -->

  

  <h1 class="{fadeStage}">Gurhar Webdev</h1>

  
  
  
  <img class="rounded-full text-center scaleIn inline-block sm:w-2/12 w-4/12 border-2 border-blue-700" src="https://i.pinimg.com/564x/be/aa/74/beaa7485babacdd56d578ae6a0af200b.jpg" alt="photo"/>
  
  

  
  <p class="scaleIn mt-20">
    {hello}
    </p>
  <p class={` ${delayType}`}> {preMain} </p>

  <p class={` ${fadeStage}`}> {mainText} </p>

  {#if showBio}
    <div class="md:mx-20 mx-10" transition:fly={{duration: 600, x: -900}}>
      <p>This is my bio. I love to build sleak web and mobile apps that are fun to interact with.
      Blah blah blah. Responsive design blah blah.</p>
    </div>
  {/if}




  <div class="absolute bottom-0 w-full">

    

    <div class={`my-4 flex flex-wrap justify-center ${fadeStage}`}> 

    <Button
      on:click={()=>{
        showContactForm = true;
      }}
      class="mx-2"
      textMode={true}
      rounded={true}
      elevation="sm"
      color="primary"
      btnText="Contact"
    />

    <Button
      on:click={()=>{
        showProjects = true;
      }}
      class="mx-2"
      textMode={true}
      rounded={true}
      color="primary"

      elevation="sm"
      btnText="Projects/work"
    />

 
      <Button
        on:click={()=>{
          showBio = !showBio;
        }}
        class="mx-2"
        textMode={true}
        rounded={true}
        color="primary"

        elevation="sm"
        btnText="about me"
      />
    

    <a href="https://docs.google.com/document/d/e/2PACX-1vTBr0Tqo8sNXf0weWmEHpP1kBmPw_G0-3VnlrYULcL3dDb5-PTh8Ix_66jcNm7YMARe2XxpfGsaDsDk/pub" target="_blank">
      <Button
      
      class="mx-2"
      textMode={true}
      rounded={true}
      color="primary"

      elevation="sm"
      btnText="Resume"
    />
    </a>
    
    

    <!-- <Button
      class="mx-2"
      textMode={true}
      rounded={true}
      color="primary"

      elevation="sm"
      btnText="Skills"
    /> -->
  
  
    
  
    

  </div>

  <hr class={`border-blue-500 width-8/10 ${fadeStage}`}>

  <div class={`my-4 flex flex-wrap justify-center ${fadeStage}`}>

      <a href="https://github.com/gurhar1133" target="_blank">
    <Button
      textMode={true}
      elevation="none"
      iconData={github}
      color="primary"
      fab={true}
    />
  </a>
    
    
  <a href="https://www.linkedin.com/in/gurhar-khalsa-61a9ba158/" target="_blank"> 
    <Button 
      textMode={true}
      elevation="none"
      iconData={linkedin}
      color="primary" 
      fab={true}
    />
  </a>

  </div>

{#if showProjects}
  <Overlay bind:value={showProjects}>
    
    <Carousel>
      <Card title="Landing Page"
              hasImage={true}
              imgSrc="https://scontent-lax3-1.xx.fbcdn.net/v/t1.0-9/117374653_10213507909210630_3006732944279027220_n.jpg?_nc_cat=101&_nc_sid=730e14&_nc_ohc=9TPTCNP-aYQAX9S7S5L&_nc_ht=scontent-lax3-1.xx&oh=e2827622e6ea99aa49d8b419f5e01857&oe=5F6081D4"
              description="A nice little landing page with fun animations. Made with svelte and tailwindCSS" >

        <a href="https://github.com/gurhar1133/landing" target="_blank">
          <Chip text="code" type="code"/>
        </a>
        <a href="https://emailtest-c548a.web.app/" target="_blank">
          <Chip text="link" type="link"/>
        </a>

      </Card>


      <Card title="Svelte Components"
            hasImage={true}
            imgSrc="https://www.tempoautomation.com/wp-content/uploads/2018/05/shutterstock_175375409-673x381.jpg"
            description="Material UI inspired components for web and native mobile applications. Svelte, svelte-native and tailwindCSS">
        
        <a href="https://github.com/gurhar1133/component_practice" target="_blank">
          <Chip text="boilerplate" type="code"/>
        </a>
        
        <a href="https://github.com/gurhar1133/native_components" target="_blank">
          <Chip text="boilerplate (native)" type="code"/>
        </a>
        
        <a href="https://github.com/gurhar1133/componentExample" target="_blank">
          <Chip text="finished" type="code" />
        </a>
        
        <a href="https://github.com/gurhar1133/nativeComponentExample" target="_blank">
          <Chip text="finished (native)" type="code"/>
        </a>

        

      </Card>

      <Card title="Cellular Automata"
            hasImage={true}
            imgSrc="https://scontent-lax3-1.xx.fbcdn.net/v/t1.0-9/95509574_10212799532781662_987953060602970112_n.jpg?_nc_cat=105&_nc_sid=cdbe9c&_nc_ohc=tmJc3c-rsowAX-Hef8v&_nc_ht=scontent-lax3-1.xx&oh=6880adb38a8dad8b501a57563de6ef95&oe=5F605CBF"
            description="Some animations of 1D and 2D cellular automata. Made with vanilla JS and a little bootstrap and jQuery">

      <a href="https://github.com/gurhar1133/JSAutomata" target="_blank">
        <Chip text="code" type="code"/>
      </a>    
        

      <a href="https://codepen.io/g-rhar-khalsa/full/MWaoJrP" target="_blank">
        <Chip text="link" type="link"/>
      </a>
        
      </Card>

      

      <Card title="This Site"
            hasImage={true}
            imgSrc="data:image/jpeg;base64,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"
            description="This website. Made with svelte and tailwindCSS">
        
        <a href="https://github.com/gurhar1133/thisSite" target="_blank">
          <Chip text="code" type="code"/>
        </a>
        
      </Card>

    </Carousel>
    
  </Overlay>
{/if}

{#if showContactForm}
  <Overlay flightPath="{{duration: 700, x: 1000}}" bind:value={showContactForm} >
    <ContactForm on:sent={sendMessage}/>
  </Overlay>
  
{/if}
  
  </div>
  

</div>




