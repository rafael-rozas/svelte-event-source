# svelte-event-source
wrapper for event source in svelte component


## use
```
<script>
 import EvtSource from './EventSource.svelte';
 
 const handleUpdate = (e) => {
  const data = e.detail
  //your code
 }
 
</script>

<EvtSource events={['update']} url="/sse" on:update={handleUpdate} />


```
