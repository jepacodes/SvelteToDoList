<svelte:head>
    <link rel="stylesheet" href="https://unpkg.com/@picocss/pico@latest/css/pico.min.css">
</svelte:head>


<script>
    let toDoList = []; //array of priority list

    let newTask="";
    let currentDate = new Date().toLocaleDateString(undefined, { 
        weekday: 'long', 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric' 
    });
    function addtodo() {
        toDoList = [...toDoList, {content: newTask, editing: false, checked: false}]
    }

    function setEditing(i, isEditing) {
        toDoList[i].editing = isEditing;
    }
    function deletetoDo(i) {
        toDoList.splice(i,1); 
        toDoList=toDoList;
    }

</script>

<div style="margin: 0 auto; padding: 20px; width 700px; align-items: center">
    <h2 style="text-align: center;">{currentDate}'s Priority List</h2>
    <p style ="text-align: center;">Where do you want to dedicate your time today?</p>
    <div style="display: block; text-align: center">
        <input type="text; width:200px; height: 50px; box-sizing: border-box; text-align: center" bind:value={newTask}>
        <button style="width: 200px; height: 50px" on:click={addtodo}>Let's Do That</button>
    </div>
</div>

{#each toDoList as toDo,i}
<div style= "display: flex; align-tems: center; width: 700px; margin: 0 auto; text-align: center">
    {#if toDo.editing}
        <input type="text" bind:value={toDo.content}>
    {:else}
    <input type="checkbox" bind:checked={toDo.checked}>
    <h4 style="flex-grow: 1; height: 50px">{toDo.content}</h4>
    {/if}
    <div style="display: flex; height: 50px">
        {#if toDo.editing}
            <button on:click={() => setEditing(i,false)}>Save</button>
        {:else}
            <button on:click={() => setEditing(i,true)}>Edit</button>
        {/if}
        <button on:click={() => deletetoDo(i)}>Remove</button>
    </div>
</div>
{/each}