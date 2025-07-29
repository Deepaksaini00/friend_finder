<script>
  import { MessageCircleCode ,Send } from "lucide-svelte";

  /** @type {import('./$types').PageData} */
  export let data; // layout.server + page.server
</script>

<div class="flex flex-row justify-center items-center h-full">
  <div class="flex flex-col items-center justify-center gap-2">
    <MessageCircleCode size={80}/>
     <span class="text-lg"> Send Message </span> 
    <p class="text-sm"> Say hi to start chat </p>
  </div>
</div>

