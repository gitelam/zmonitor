<script>
  // @ts-nocheck
  import { goto } from "$app/navigation";
  import Navbar from "../../../lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";
  import LinePlot from "../../../lib/charts/test/LinePlot.svelte";
  import * as d3 from "d3";

  let user ={
    "name": "John Ipsum Dereee Dou",
    "email": "johnipsumdereedou@gmail.com",
    "role": "admin",
  };

  let userJson = JSON.parse(JSON.stringify(user));

  let isEdit = false;
  let readonly = "readonly";
  let disabled = "disabled";

  function edit(){
    isEdit = !isEdit;
    readonly = "";
    disabled = "";
  }

  function noEdit(){
    isEdit = false;
    readonly = "readonly";
    disabled = "disabled";
  }

  function cancel(){
    noEdit();
    userJson = JSON.parse(JSON.stringify(user));
    console.log(user)
    console.log(userJson)
  }

  function save(){
    noEdit();
    user = userJson;
    //send...
  }

  function goback(){
    history.back();
  }

</script>

<Navbar currentPage={"Users"} />

<div class="flex justify-start w-screen h-screen text-white">
  <div class=" border-zinc-600 border-1 border-r w-96">
    <div class="mt-20">
      <div>
        <div class="px-6 pt-3">
          <div class="flex justify-between">
            <h2>Users</h2>
            <div class="flex">
              <button
                on:click={() => goback()}
                class="flex space-x-1 text-blue-300 hover:text-blue-600 active:text-purple-500"
              >
                <Icon icon="mdi:arrow-back" width="24" height="24" />
                <div class="text-md">back</div>
              </button>
            </div>
          </div>

          <div class="flex items-center">
            <input
              class="w-full my-4 p-2 outline-none bg-zinc-900"
              type="text"
              placeholder="Search..."
            />
            <button
              class="p-2 bg-zinc-700 hover:bg-slate-700 active:bg-purple-500"
            >
              <Icon
                icon="material-symbols-light:search"
                width="24"
                height="24"
              />
            </button>
          </div>
        </div>

        <div class="list w-auto mt-4">
          <!--iterate only 3 times-->
            <!-- svelte-ignore a11y-no-static-element-interactions -->
            <!-- svelte-ignore a11y-mouse-events-have-key-events -->
            <button
              class="w-full pl-6 focus:bg-slate-700 focus:border-1 focus:border-blue-700 p-2 flex items-center hover:bg-zinc-950 active:bg-zinc-500"
            >
              <div class="icon text-zinc-400">
                <Icon icon="ph:user" width="24" height="24"  />
              </div>

              <div class="flex flex-col w-full items-start mx-4">
                <div class="overflow-x-auto max-w-52">
                  <p class="text-white truncate">John Ipsum Dereee Dou</p>
                </div>
              </div>

              <div class=" text-white">
                <Icon
                  icon="material-symbols-light:keyboard-arrow-right"
                  width="42"
                  height="42"
                />
              </div>
            </button>

        </div>
      </div>
    </div>
  </div>

  <div class="mt-16 w-full">
      <div class="flex h-full">
        <div class="p-7 w-5/12 metrics items-center  border-r border-zinc-600">
          <div class=" space-y-6">
            

            <div class="flex flex-col">
              

              <div class="flex justify-between">
                {#if isEdit}
                EDIT
                {/if}
                USER INFO
                
                <button on:click={edit} class={isEdit?"hidden":"text-blue-400 rounded-full hover:bg-slate-900 p-2"}   >
                  <Icon icon="material-symbols-light:edit-square-outline-sharp" width="32" height="32"  />
                </button>

              </div>

              <div class="flex">
                <input class={isEdit? "hidden":"outline-none text-4xl truncate bg-black"} {readonly} value="{userJson.name}" >
              </div>
              
            </div>

            <div class="space-y-4">

              {#each Object.entries(userJson) as [index, value]}

                  <div class="flex flex-col">

                      <div class="font-medium">
                        {index}
                      </div>

                      {#if index == "role"}
                      <div class="flex">
                        <form>
                            <select on:select={()=>{console.log(user)}} bind:value={userJson[index]} class="bg-black border rounded-md p-2 text-blue-300 outline-none" {disabled}>
                                <option value="admin">admin</option>
                                <option  value="moderator">moderator</option>
                            </select>
                        </form>
                      </div>
                      {:else}
                      <div class="font-light">
                        <input  bind:value={userJson[index]}  class={isEdit? "w-full p-2 outline-1 rounded-md bg-zinc-800" : "w-full decoration-none bg-black focus:none focus-none outline-none"} {readonly} type="text" >
                      </div>
                      {/if}
                    
                  </div>
              
                {/each}
                

            </div>



            <!-- <div class="py-7 flex items-center space-x-4">
              <h2 class="text-white">Role</h2>
              <div class="flex">
                  <form>
                      <select class="bg-black border rounded-md p-2 text-blue-300 outline-none" {disabled}>
                          <option value="admin">admin</option>
                          <option value="user">moderator</option>
                      </select>
                  </form>                
              </div>
            </div> -->


            {#if isEdit}

            <div class="flex justify-around">
              <div class="flex justify-end">
                <button on:click={cancel} class="bg-red-400 p-2 rounded-md text-white">Cancel</button>
              </div>
                <div class="flex justify-end">
                  <button on:click={save} class="bg-blue-400 p-2 rounded-md text-white">Save</button>
                </div>
            </div>
            
            {/if}

            
          </div>
        </div>

       
          

        
      </div>
  </div>
</div>
