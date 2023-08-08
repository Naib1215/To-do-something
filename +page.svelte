<svelte:head>
    <script src="https://cdn.tailwindcss.com"></script>
</svelte:head>
<script>
    let toDoList = [];
    let textInput = "";

    function addToDo(){
        toDoList = [...toDoList, {content: textInput, editing: false, checked: false}]
    }

    function setEditing(i, isEditing){
        toDoList[i].editing = isEditing;
    }
    function deleteTodo(i){
        toDoList.splice(i, 1);
        toDoList = toDoList;
    }
</script>
<div class = "font-mono">
    <h1 class = "mt-10 text-[50px] text-center">Movies To Watch!</h1>
    <p class = "pl-20 text-[30px] font-bold">Movies:</p>
    <div class = "place-content-center flex">
        <input class = "text-[20px] p-2 bg-red-400 border-black border-2 h-10 w-[300px]" type="text" bind:value={textInput}>
        <button on:click = {addToDo} class = "hover:border-2 hover:border-l-0 hover:border-black active:bg-black active:text-red-400 hover:bg-red-400 hover:text-black bg-black text-[20px] font-bold h-10 w-[100px] text-red-400">ADD</button>
    </div>
</div>
{#each toDoList as toDo, i}
    <div class = "font-mono flex items-baseline w-[700px] m-auto mt-5">
        {#if toDo.editing}
            <input class = "text-[20px] bg-red-400 border-black border-2" type="text" bind:value={toDo.content}>

        {:else} 
        <input type="checkbox" bind:checked={toDo.checked}>
        <h4 class = "grow m-2 text-[22px]">{toDo.content}</h4>
        {/if}
        <div class = "flex">
            {#if toDo.editing}
                <button on:click = {() => setEditing(i, false)} class = "mr-1 hover:bg-black hover:text-red-400 active:bg-red-400 active:text-black mt-3 ml-3 mb-3 bg-red-400 text-[20px] font-bold pr-4 pl-4 pt-2 pb-2 rounded-[7px]">Save</button>
            {:else}
            <button on:click = {() => setEditing(i, true)} class = "mr-1 hover:bg-black hover:text-red-400 active:bg-red-400 active:text-black mt-3 ml-3 mb-3 bg-red-400 text-[20px] font-bold pr-4 pl-4 pt-2 pb-2 rounded-[7px]">Edit</button>
            {/if}
                <button on:click = {() => deleteTodo(i)} class = "active:bg-black active:text-red-400 hover:bg-red-400 hover:text-black mt-3 mr-3 mb-3 bg-black text-red-400 text-[20px] font-bold pr-4 pl-4 pt-2 pb-2 rounded-[7px]">Delete</button>
        </div>
    </div>
{/each}
