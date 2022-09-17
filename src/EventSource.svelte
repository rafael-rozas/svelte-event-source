<script>
  import { createEventDispatcher, onMount, onDestroy } from 'svelte';
  const dispacher = createEventDispatcher()
  export let url;
  export let events = [];
  export let evtInit= {withCredentials:true}
  let evtSource;

  onMount(()=>{
    
    if(!url) return;

    evtSource = new EventSource( url, evtInit );

    evtSource.onmessage = (e) => dispacher('message',e.data);

    evtSource.onerror = (e)=> dispacher('error',e);

    events.forEach( eventName => {
      evtSource.addEventListener(eventName,(e) => {
        if(e.data){
          try {
            dispacher(eventName,JSON.parse(e.data));
          } catch (error) {
            dispacher(eventName,e.data);
          }
        }
      })
    });

  });

  onDestroy(()=> {
    if(evtSource){
      evtSource.close()
    }
  })
</script>