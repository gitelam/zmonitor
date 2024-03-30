<script>
  import { goto } from "$app/navigation";

  import Navbar from "../../../lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";

  //axios import
  import axios from "axios";

  //svelte onmount import
  import { onMount } from "svelte";

  // svelte onmount method
  onMount(async () => {
    await get_data();
  });

  let num = 0;
  let dec = 0;

  let times = [1, 2, 3, 4, 5, 6];

  //interval to make the number change every 2 seconds
  setInterval(() => {
    num = Math.floor(Math.random() * 100);
    dec = Math.floor(Math.random() * 100);
  }, 500);

  //unsolved tickets
  /**
   * @type {{ [s: string]: any; } | ArrayLike<any>}
   */
  let unsolved_tickets = [];


  let system_info = {
    "System": "Windows 10 10.0.19045",
    "Node Name": "DESKTOP-KT5HJPV",
    "Machine": "AMD64",
    "Processor (CPU)": "Intel(R) Core(TM) i7-3720QM CPU @ 2.60GHz",
    "mac-address": "60-67-20-5C-D2-5C",
    "conection-interface": "Wi-Fi",
    "Boot Time": "2024/3/17 15:3:28"
  }


  function get_system_info(){
    system_info={
      "System": choice(["Windows 10 10.0.19045", "Windows 11 10.0.19045", "Windows 12 10.0.19045"]),
      "Node Name": choice(["DESKTOP-KT5HJPV", "DESKTOP-KT5HJPV", "DESKTOP-KT5HJPV"]),
      "Machine": choice(["AMD64", "AMD64", "AMD64"]),
      "Processor (CPU)": choice(["Intel(R) Core(TM) i7-3210QM CPU @ 2.60GHz", "Intel(R) Core(TM) i7-3720QM CPU @ 2.65GHz", "Intel(R) Core(TM) i7-4940HQ CPU @ 2.61GHz"]),
      "mac-address": choice(["60-67-20-5C-D2-5C", "601-1-10-4C-D2-5C", "80-23-13-KK-DD-5C"]),
      "conection-interface": choice(["Wi-Fi", "Ethernet 4", "Ethernet 1"]),
      "Boot Time": choice(["2024/3/23 15:3:28", "2024/1/12 13:3:22", "2024/2/21 15:3:28"])
    }
  }

  //random choice function with params
  /**
   * @param {string | any[]} arr
   */
  function choice(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
  }



  //axios get method
  const get_data = async () => {
    try {
      const response = await axios.get(
        "http://localhost:8000/first_unsolved_tickets"
      );

      //save the response in the unsolved tickets set
      unsolved_tickets = response.data;

      console.log(unsolved_tickets);

      console.log(response);
    } catch (error) {
      console.error(error);
    }
  };




</script>

<Navbar currentPage={"summary"} />

<div class="internal-body flex place-content-center mt-20 mx-4">
  <div class="flex flex-col board w-full">
    <div class="flex upperboard gap-3">
      <div class="flex w-full flex-col">
        <div class="w-full h-auto p-4 mr-8 bg-zinc-800 rounded-xl">
          <h1 class="text-white text-lg font-bold">system monitor</h1>

          <div class="flex space-x-4">
            <div class="flex w-full">
              <div class="flex-col space-y-2 w-full">
                <div class="flex py-4 space-x-4">
                  <div
                    class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl"
                  >
                    this is a chart
                  </div>
                  <div
                    class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl"
                  >
                    this is a chart
                  </div>
                </div>

                <div class="flex py-4 space-x-4">
                  <div
                    class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl"
                  >
                    this is a chart
                  </div>
                  <div
                    class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl"
                  >
                    this is a chart
                  </div>
                </div>
              </div>
            </div>

            <div class="p-4 w-8/12 bg-zinc-600 rounded-2xl space-y-4">
              <div class="flex justify-between items-center px-4">
                <h2 class="text-white font-bold">Online machines</h2>

                <div class="flex space-x-4">
                  <div
                    class="px-4 flex justify-center items-center rounded-xl bg-zinc-700 text-zinc-300"
                  >
                    99+
                  </div>
                  <a
                    on:click={() => {
                      goto("/app/machine-list");
                    }}
                    href="#"
                    class="flex justify-center items-center font-bold rounded-xl text-blue-300 hover:bg-gray-500 active:bg-blue-500"
                  >
                    <div class="ml-2">see all</div>
                    <Icon
                      icon="material-symbols-light:keyboard-arrow-right"
                      width="42"
                      height="42"
                    />
                  </a>
                </div>
              </div>

              <div class="flex flex-col gap-2 list">

                <!--iterate only 3 times-->
                {#each times as time}
                  
                  <!-- svelte-ignore a11y-no-static-element-interactions -->
                  <!-- svelte-ignore a11y-mouse-events-have-key-events -->
                  <button on:click={get_system_info} class="w-full justify-between focus:bg-slate-700 focus:ring focus:ring-gray-300 p-2 flex items-center item-list rounded-2xl bg-zinc-800  hover:bg-zinc-950  active:bg-zinc-500  space-x-5">
                    <div class="icon  hover:text-red">
                      <Icon
                        icon="mdi:circle"
                        width="12"
                        height="12"
                        color="lime"
                      />
                    </div>
                    
                    <div class="flex w-full justify-between items-center">
                      <div class="overflow-x-auto max-w-44">
                        <p class="text-white truncate">DESKTOP-HBKSKL2</p>
                      </div>

                      <div class=" text-gray-400">
                         up: {num}2.{dec} mb/s 
                      </div>

                      <div class=" text-gray-400">
                        down: {dec}4.{num} mb/s  
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
                  
                {/each}               



              </div>
            </div>
          </div>
        </div>

        <div class="px-4">
          <div class="flex flex-col rounded-b-xl p-4 text-white bg-zinc-600">
            <div class="">

             
              <div class="flex space-x-8">

              {#each Object.entries(system_info) as [index, value]}

                <div class="flex flex-col">
                  
                  <div class="font-medium">
                    {index}
                  </div>
    
                  <div class="font-light">
                    {value}
                  </div>

                </div>

              {/each}

            </div>


            </div>
          </div>
        </div>

      </div>

      <div class="ticket-section">
        <!--do iterable lis with svelte with the unsolved_tickets set-->
        <div class="unsolved-tickets w-96 p-4 bg-zinc-800 rounded-xl">
          
          <h2 class="text-white text-lg font-bold">new tickets</h2>

          {#if Object.values(unsolved_tickets).length == 0}
              <div
                class="flex h-full flex-col items-center justify-center align-middle space-y-4"
              >
                <Icon
                  icon="mdi:archive-cancel-outline"
                  width="48"
                  height="48"
                  color="gray"
                />
                <p class="text-zinc-400 font-bold">Nothing yet...</p>
              </div>
          {:else}
              {#each Object.values(unsolved_tickets) as ticket, index}
                <a href="#">
                  <div
                    class={index == Object.values(unsolved_tickets).length - 1
                      ? "item-list flex items-center p-2 hover:bg-slate-800"
                      : "item-list flex items-center border-b border-zinc-500 p-2 hover:bg-slate-800"}
                  >
                    <p class="text-white">
                      <Icon
                        icon="material-symbols-light:warning-outline-rounded"
                        width="38"
                        height="38"
                      />
                    </p>
                    <div class="w-full">
                      <p
                        class="text-white
                    mx-2 font-bold"
                      >
                        {ticket.id} - {ticket.section}
                        {ticket.place}
                      </p>
                      <p
                        class="text-white
                    mx-2 text-sm font-light"
                      >
                        {new Date(ticket.date_creation).toDateString()}
                      </p>
                      <p
                        class="text-white
                    mx-2 text-sm font-light"
                      >
                        {new Date(ticket.date_creation).toLocaleTimeString()}
                      </p>
                    </div>

                    <p class="text-white ">
                      <Icon
                        icon="material-symbols-light:keyboard-arrow-right"
                        width="38"
                        height="38"
                      />
                    </p>

                  </div>
                </a>
                
              {/each}

              <button class="flex w-full h-full justify-center align-middle items-center rounded-xl text-blue-400 hover:bg-zinc-700">
                          see all tickets 99+
                          <Icon
                          icon="mdi:keyboard-arrow-right"
                          width="24"
                          height="24"
                        />
              </button>
            
          {/if}
          
        </div>
      </div>
    </div>
  </div>
</div>
