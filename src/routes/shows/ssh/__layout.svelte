<script context="module">
  import Show from "$lib/Show.ts"
  export async function load() {
    return { 
      stuff: {  show: new Show("Self Hosted") } 
    }
  }

  
</script>  

<slot></slot>
