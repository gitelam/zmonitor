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

<div class="internal-body flex place-content-center ">
  <div class="flex flex-col board w-full mx-8 mt-20">
    


    <div class="flex upperboard gap-8">
      


      <div class="flex w-full flex-col">

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
             
              <div class="flex justify-between items-center mx-4 my-4">
               
                <h2 class="text-white font-bold">
                Users in net
               </h2>
               
               
               <div class="flex space-x-4">
                  <div class="px-4 flex justify-center items-center rounded-xl bg-zinc-700 text-zinc-300">
                    99+
                   </div>
                <a href="#" class="flex justify-center items-center font-bold rounded-xl text-blue-300 hover:bg-gray-500 active:bg-blue-500 ">
                  <div class="ml-2">
                    see all
                  </div>
                  <Icon
                          icon="material-symbols-light:keyboard-arrow-right"
                          width="42"
                          height="42"
                        />
                  </a>
               </div> 
              
             </div>
    
             <div class="list">
              
              <div class="p-4 item-list rounded-2xl bg-zinc-800 flex ">
    
                <div class="icon mr-2">
                  <Icon icon="mdi:circle" width="12" height="12" color="lime" />
                </div>
    
    
                  <div class="flex w-full flex-col space-y-4">
                    
                    <div class="flex">
                      <div class=" w-full ">
        
                        <div class="w-full">
                          <p class="text-white">DESKTOP-HBKSKL2</p>
                        </div>
          
                        <div class="flex w-full justify-between">
                            <div class="ip">
                              <p class="text-white">60-67-20-5C-D2-5C</p>
                            </div>
                        </div>
      
                      </div>
      
                      <div class=" w-full">

                        <div class="w-full">
                          <p class="text-white break-normal">ipv4</p>
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
        
        <div class="px-4">
          <div class="flex flex-col rounded-b-xl p-4 text-white bg-zinc-600">
      
          

          <div class="font-bold">
             System-info 
             <div class="font-light">
              DESKTOP-HBKSKL2
             </div>
          </div>
      
        </div>
        </div>

        
  
        <div class="flex flex-col">
  
        </div>
      </div>

      

  
      <div class="ticket-section flex">



       
                  <!--do iterable lis with svelte with the unsolved_tickets set-->
        <div class="unsolved-tickets w-auto h-auto p-4  bg-zinc-800 rounded-xl">
          <h2 class="text-white text-lg font-bold">new tickets</h2>



          {#if Object.values(unsolved_tickets).length==0}

          <div class="unsolved-tickets w-auto h-auto p-4 mr-4 bg-zinc-800 rounded-xl">
            <h2 class="text-white text-lg font-bold">new tickets</h2>
            <div class="h-full w-72">
             
  
              <div class="flex h-full flex-col items-center justify-center align-middle space-y-4">
  
                <Icon icon="mdi:archive-cancel-outline" width="48" height="48" color="gray"/>
                <p class="text-zinc-400 font-bold">Nothing yet...</p>
  
              </div>
  
            </div>
          </div>
  
          {:else}
  
          <div class="mt-2 w-96">
           
           
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
            
            

            <a href="#">
              <div class="flex h-full align-middle items-center mt-4">
                <div class="flex h-full w-full align-middle items-center justify-center rounded-xl text-blue-400 hover:bg-zinc-700">
                  <div class="flex flex-col">
                   <p>
                     see all tickets 
                   </p>
                   <div class="flex justify-center">99+
                    <Icon icon="mdi:keyboard-arrow-right" width="24" height="24" />
                   </div>
                  </div>
                 </div>
              </div>

             
            </a>

          </div>
          
          



        {/if}

        </div>



  
  
      </div>
    </div>
    

    




  </div>


</div>
