<style>
.container {
   display: flex;
   flex-wrap: nowrap;
   overflow-x: scroll;
   overflow-y: scroll;
   -webkit-overflow-scrolling: touch;
   -ms-overflow-style: -ms-autohiding-scrollbar; 
 }
 /* @media (max-width: 800px){
   .container{
     display: inline-block;
     margin-top: -4rem;
   }
 } */
 @media (max-width: 750px){
   .container{
     display: inline-block;
     margin-top: -4rem;
   }
 }
</style>
<div class="container">
    <slot> </slot>
</div>