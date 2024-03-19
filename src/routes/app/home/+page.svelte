p<script>
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

  //axios get method
  const get_data = async () => {
    try {
      const response = await axios.get(
        "http://localhost:8000/unsolved_tickets"
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

<div class="internal-body flex place-content-center w-full h-full">
  <div class="flex board w-full mx-8 mt-24">
    
    
    
    <div class="w-full h-auto p-4 mr-8 bg-zinc-800 rounded-xl">
      <h1 class="text-white text-lg font-bold">system monitor</h1>

      <div class="flex space-x-4">
        
        <div class="flex w-full ">
        
          <div class="flex-col space-y-2 w-full">

            <div class="flex  py-4 space-x-4 ">
              <div class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl">
                this is a chart
              </div>
              <div class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl">
                this is a chart
              </div>
            </div>
  
            <div  class="flex py-4 space-x-4 ">
              <div class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl">
                this is a chart
              </div>
              <div class="p-8 w-full h-52 bg-zinc-950 text-white rounded-2xl">
                this is a chart
              </div>
            </div>

          </div>

        </div>
        


        <div class="p-4 w-8/12 bg-zinc-600 rounded-2xl">
         <div class="flex justify-between items-center">
          <h2 class="text-white font-bold">
            Users in net
         </h2>
         <a href="#" class="font-bold rounded-xl p-2 text-blue-300 hover:bg-zinc-600">
          {"see all >"}
         </a>
         </div>

         <div class="list">
          
          <div class="p-4 item-list rounded-2xl bg-zinc-800 flex ">

            <div class="icon mr-2">
              <Icon icon="mdi:circle" width="24" height="24" color="lime" />
            </div>


              <div class="flex w-full flex-col space-y-4">
                
                <div>
                  <div class="flex w-full ">
    
                    <div class="w-full">
                      <p class="text-white">DESKTOP-HBKSKL2</p>
                    </div>
      
                    <div class="flex w-full justify-between">
                        <div class="ip">
                          <p class="text-white">ipv4</p>
                        </div>
                    </div>
  
                  </div>
  
                  <div class="flex w-full ">
                    <div class="w-full">
                      <p class="text-white">d9:2b:19:72:8f:e8</p>
                    </div>
      
                    <div class="flex w-full justify-between">
                        <div class="ip">
                          <p class="text-white">172.43.32.02.1</p>
                        </div>
                    </div>
                  </div>

                </div>

                
                <div class="speed flex flex-col ">
                  <div class="up">
                    <p class="text-gray-400 font-light">
                      up: 1.2 mb/s
                    </p>
                  </div>
                  <div>
                    <p class="text-gray-400 font-light">
                      down: 2.3 mb/s
                    </p>
                  </div>
                </div>

              </div>
              
              


          </div>

         </div>

        </div>

      </div>

      


    </div>

    <div class="ticket-section flex">
      <!--do iterable lis with svelte with the unsolved_tickets set-->
      <div class="unsolved-tickets w-96 h-auto p-4 mr-4 bg-zinc-800 rounded-xl">
        <h2 class="text-white text-lg font-bold">new tickets</h2>
        <div class="mt-2 overflow-auto max-h-80">
          {#each Object.values(unsolved_tickets) as ticket, index}
            <a href="#">
              <div
                class={index == Object.values(unsolved_tickets).length - 1
                  ? "item-list flex items-center p-2 hover:bg-slate-800"
                  : "item-list flex items-center border-b p-2 hover:bg-slate-800"}
              >
                <p class="text-white m-3">
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

                <p class="text-white m-3">
                  <Icon
                    icon="material-symbols-light:keyboard-arrow-right"
                    width="38"
                    height="38"
                  />
                </p>
              </div>
            </a>
          {/each}
        </div>
      </div>

 


    </div>

    
  </div>
</div>
