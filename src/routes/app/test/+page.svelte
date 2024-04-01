<script lang="js">
  import LinePlot from "../../../lib/charts/test/LinePlot.svelte";
  import * as d3 from "d3";

  let data = d3.ticks().map(Math.sin);

  //set interval for live chart
  setInterval(() => {
    data = data.slice(-50).concat(Math.sin(Math.random() * 2));
  }, 500);

  /**
   * @param {any} event
   */
  function onMousemove(event) {
    const [x, y] = d3.pointer(event);
    data = data.slice(-200).concat(Math.atan2(x, y));
  }

  import Navbar from "../../../lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";

  import { goto } from "$app/navigation";

  //axios import
  import axios from "axios";

  //svelte onmount import
  import { onMount } from "svelte";

  //svelte onmount method
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
  }, 2400);

  //unsolved tickets
  /**
   * @type {{ [s: string]: any; } | ArrayLike<any>}
   */
  let unsolved_tickets = [];

  let system_info = {
    OS: "Windows 10 10.0.19045",
    "Node Name": "DESKTOP-KT5HJPV",
    Machine: "AMD64",
    "Processor (CPU)": "Intel(R) Core(TM) i7-3720QM CPU @ 2.60GHz",
    "mac-address": "60-67-20-5C-D2-5C",
    "conection-interface": "Wi-Fi",
    "Boot Time": "2024/3/17 15:3:28",
  };

  function get_system_info() {
    system_info = {
      OS: choice([
        "Windows 10 10.0.19045",
        "Windows 11 10.0.19045",
        "Windows 12 10.0.19045",
      ]),
      "Node Name": choice([
        "DESKTOP-KT5HJPV",
        "DESKTOP-KT5HJPV",
        "DESKTOP-KT5HJPV",
      ]),
      Machine: choice(["AMD64", "AMD64", "AMD64"]),
      "Processor (CPU)": choice([
        "Intel(R) Core(TM) i7-3210QM CPU @ 2.60GHz",
        "Intel(R) Core(TM) i7-3720QM CPU @ 2.65GHz",
        "Intel(R) Core(TM) i7-4940HQ CPU @ 2.61GHz",
      ]),
      "mac-address": choice([
        "60-67-20-5C-D2-5C",
        "601-1-10-4C-D2-5C",
        "80-23-13-KK-DD-5C",
      ]),
      "conection-interface": choice(["Wi-Fi", "Ethernet 4", "Ethernet 1"]),
      "Boot Time": choice([
        "2024/3/23 15:3:28",
        "2024/1/12 13:3:22",
        "2024/2/21 15:3:28",
      ]),
    };
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

<Navbar currentPage={"dashboard"} />

<div class="flex mt-18 justify-start w-screen h-screen text-white">
  <!--sidebar-->
  <div class=" border-zinc-600 border-1 border-r w-96">
    <div class="mt-20">
      <div class="">
        <div class="px-6 pt-3">
          <div class="flex justify-between">
            <h2>Online machines</h2>
            <button
              on:click={() => goto("/app/machine-list")}
              class="text-blue-300 hover:text-blue-600 active:text-purple-500"
            >
              manage
            </button>
          </div>
        </div>

        <div class="list w-auto mt-4">
          <!--iterate only 3 times-->
          {#each times as time}
            <!-- svelte-ignore a11y-no-static-element-interactions -->
            <!-- svelte-ignore a11y-mouse-events-have-key-events -->
            <button
              on:click={get_system_info}
              class="w-full pl-6 focus:bg-slate-700 focus:border-1 focus:border-blue-700 p-2 flex items-center hover:bg-slate-800 active:bg-zinc-500"
            >
              <div class="icon hover:text-red">
                <Icon icon="mdi:circle" width="12" height="12" color="lime" />
              </div>

              <div class="flex flex-col w-full items-start mx-4">
                <div class="overflow-x-auto max-w-52">
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
  <!--end sidebar-->

  <div class="flex flex-col w-full">
    <!--here start charts-->
    <div class="flex">
      <div
        class="bg-zinc-950 h-full w-full border-r border-b border-zinc-600 pt-20"
      >
        <div class="mx-6 pt-3">
          <div class="flex justify-between">
            <h2>System monitor</h2>
            <button
              class="text-blue-300 hover:text-blue-600 active:text-purple-500"
            >
              view all
            </button>
          </div>
        </div>

        <!-- svelte-ignore a11y-no-static-element-interactions -->
        <div class="flex flex-col h-full mt-4 mx-6 ">
          <div class="flex ">
            <LinePlot {data} type="show_data"/>
            <LinePlot {data} type="show_data"/>
            <LinePlot {data} type="show_data"/>
          </div>
          <div class="flex ">
            <LinePlot {data} type="show_data"/>
            <LinePlot {data} type="show_data" path_fill_color={"yellow"} />
            <LinePlot {data} type="show_data"/>
          </div>
        </div>
      </div>
      <div class="bg-zinc-950 h-full w-full border-b border-zinc-600 pt-20">
        <div class="px-6 pt-3">
          <div class="flex justify-between">
            <h2>Recent activity</h2>
            <button
              class="text-blue-300 hover:text-blue-600 active:text-purple-500"
            >
              view all
            </button>
          </div>
        </div>
        <div class="h-full mt-4">
          {#if Object.values(unsolved_tickets).length == 0}
            <div
              class="flex h-full flex-col items-center justify-center align-middle space-y-4"
            >
              <Icon
                icon="material-symbols-light:contract-delete-outline"
                width="48"
                height="48"
                color="gray"
              />
              <p class="text-zinc-400">Nothing yet...</p>
            </div>
          {:else}
            {#each Object.values(unsolved_tickets) as ticket, index}
              <a class=" " href="#">
                <div class="item-list flex items-center p-2 hover:bg-slate-800">
                  <p class="text-white">
                    <Icon
                      icon="material-symbols-light:warning-outline-rounded"
                      width="32"
                      height="32"
                    />
                  </p>
                  <div class="w-full">
                    <div class="flex flex-col w-full items-start mx-4">
                      <div class="overflow-x-auto max-w-52">
                        <p class="text-white truncate">
                          {ticket.id} - {ticket.section}
                          {ticket.place}
                        </p>
                      </div>

                      <div class="text-m">
                        <div class=" text-gray-400">
                          {new Date(ticket.date_creation).toDateString()}
                        </div>

                        <div class=" text-gray-400">
                          {new Date(ticket.date_creation).toLocaleTimeString()}
                        </div>
                      </div>
                    </div>
                  </div>

                  <p class="text-white">
                    <Icon
                      icon="material-symbols-light:keyboard-arrow-right"
                      width="38"
                      height="38"
                    />
                  </p>
                </div>
              </a>
            {/each}
          {/if}
        </div>
      </div>
    </div>

    <!--here end charts-->

    <!--here start system info and recent tickets-->
    <div class="flex h-full">
      <div class="bg-zinc-950 w-full overflow-auto">
        <div class="px-6 pt-3">
          <div class="flex justify-between">
            <h2>System info</h2>
            <!-- <button
              class="text-blue-300 hover:text-blue-600 active:text-purple-500"
            >
              view all
            </button> -->
          </div>

          <div class="flex flex-col space-y-4 my-4">
            <div class="flex space-x-8 rounded-b-xl text-white">
              {#each Object.entries(system_info) as [index, value]}
                <div>
                  <div class="flex flex-col">
                    <div class="font-medium">
                      {index}
                    </div>

                    <div class="font-light">
                      {value}
                    </div>
                  </div>
                </div>
              {/each}
            </div>

            <div class="flex space-x-8 rounded-b-xl text-white">
              
              {#each Object.entries(system_info) as [index, value]}
                <div>
                  <div class="flex flex-col">
                    <div class="font-medium">
                      {index}
                    </div>

                    <div class="font-light">
                      {value}
                    </div>
                  </div>
                </div>
              {/each}


            </div>
          </div>
        </div>
      </div>
      <!--system info end-->
    </div>
    <!--here end system info and recent tickets-->
  </div>
</div>
