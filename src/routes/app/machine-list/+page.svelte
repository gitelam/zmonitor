<script>
  // @ts-nocheck

  import { goto } from "$app/navigation";
  import Navbar from "../../../lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";
  import LinePlot from "../../../lib/charts/test/LinePlot.svelte";
  import * as d3 from "d3";

  let b = 0;
  let num = 0;
  let dec = 0;

  let times = [1, 2, 3, 4, 5, 6];

  //interval to make the number change every 2 seconds
  setInterval(() => {
    num = Math.floor(Math.random() * 100);
    dec = Math.floor(Math.random() * 100);
  }, 2400);

  let system_info = {
    OS: "Windows 10 10.0.19045",
    "Node Name": "DESKTOP-KT5HJPV",
    Machine: "AMD64",
    "Processor (CPU)": "Intel(R) Core(TM) i7-3720QM CPU @ 2.60GHz",
    "mac-address": "60-67-20-5C-D2-5C",
    "conection-interface": "Wi-Fi",
    "Boot Time": "2024/3/17 15:3:28",
  };

  let data = d3.ticks(0, 0, 0).map(Math.sin);

  //set interval for live chart
  setInterval(() => {
    data = data.slice(-200).concat(0.5);
  }, 500);

  function get_system_info() {
    system_info = {
      OS: choice([
        "Windows 10 10.0.19045",
        "Windows 11 10.0.19045",
        "Windows 12 10.0.19045",
      ]),
      "Node Name": choice(["DESKTOP-JKJKHJPV", "DESKTOP-KT5H", "DESKTOP-JPV"]),
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

  /**
   * @param {string} modalName
   */
  function openModal(modalName) {
    const modal = document.getElementById(modalName);
    // @ts-ignore
    modal.showModal();
  }
</script>

<Navbar currentPage={"machines"} />

<div class="flex justify-start w-screen h-screen text-white">
  <div class=" border-zinc-600 border-1 border-r w-96">
    <div class="mt-20">
      <div>
        <div class="px-6 pt-3">
          <div class="flex justify-between">
            <h2>Machines</h2>
            <div class="flex">
              <button
                on:click={() => goto("/app/test")}
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
          {#each times as time}
            <!-- svelte-ignore a11y-no-static-element-interactions -->
            <!-- svelte-ignore a11y-mouse-events-have-key-events -->
            <button
              on:click={get_system_info}
              class="w-full pl-6 focus:bg-slate-700 focus:border-1 focus:border-blue-700 p-2 flex items-center hover:bg-zinc-950 active:bg-zinc-500"
            >
              
              <div class="icon hover:text-red">
                <Icon icon="mdi:circle" width="12" height="12" color="lime" />
              </div>

              <div class="flex flex-col w-full items-start mx-4">
                <div class="overflow-x-auto max-w-52">
                  <p class="text-white truncate">DESKTOP-HBKSKL2</p>
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

  <div class="mt-16 w-full">
    <div class="content flex w-full flex-col h-full">
      <div class="flex h-full">
        <div class="p-7 w-5/12 metrics items-center">
          <div class=" space-y-6">
            <div class="flex flex-col">
              <div>PC INFO</div>
              <div class="">
                <h2 class="text-4xl truncate">DESKTOP-KT5HJPV</h2>
              </div>
            </div>
            <div>
              <Icon
                icon="material-symbols-light:desktop-mac-outline-sharp"
                width="124"
                height="124"
              />
            </div>
            <div>
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

        <div
          class="w-5/12 flex flex-col space-y-6 text-slate-300 border-r px-4 border-zinc-600"
        >
          <div class="py-7 flex items-center justify-between">
            <h2 class="text-white">Alerts</h2>
            <div class=" flex">
              <button
                on:click={() => openModal("dialog")}
                class="flex justify-center align-middle items-center text-blue-300 hover:text-blue-600 active:text-purple-500"
              >
                <div class="text-md">create</div>
                <Icon
                  icon="material-symbols-light:add"
                  width="32"
                  height="32"
                />
              </button>
            </div>
          </div>

          <button class="rounded-md hover:bg-zinc-700 p-2">
            <div class="alarm-item flex items-center">
              <div class="flex flex-col justify-center hover:text-red">
                <Icon
                  icon="material-symbols-light:memory-alt-outline"
                  width="32"
                  height="32"
                />
                <div>RAM</div>
              </div>
              <div class="flex flex-col w-full items-start mx-4">
                <div class="overflow-x-auto max-w-52">
                  <p class="text-white truncate">Memory warning</p>
                </div>

                <div class=" text-gray-400">trigger value: 20 mb/s</div>
                <div class=" text-gray-400">current value: 10 mb/s</div>
              </div>
            </div>
          </button>

          <button class="rounded-md hover:bg-zinc-700 p-2">
            <div class="alarm-item flex items-center">
             
              <div class="flex flex-col justify-center hover:text-red">
                <Icon
                  icon="material-symbols-light:memory-sharp"
                  width="32"
                  height="32"
                />
                <div>CPU</div>
              </div>
              
              <div class="flex flex-col w-full items-start mx-4">
                <div class="overflow-x-auto max-w-52">
                  <p class="text-white truncate">CPU trothling warning</p>
                </div>

                <div class=" text-gray-400">trigger value: 20 mb/s</div>
                <div class=" text-gray-400">current value: 10 mb/s</div>
              </div>

            </div>
          </button>
        </div>

        <div class="w-full h-full bg-zinc-800 p-4 space-y-4">
          <div class="flex metric">
            <div class="w-4/12 rounded-l-md bg-zinc-950 p-2">
              <div class="flex h-full flex-col">
                

                <div class="flex items-center">
                  <Icon
                  icon="material-symbols-light:memory-alt-outline"
                  width="32"
                  height="32"
                />
                <div>RAM</div>
                </div>
                <div class="text-zinc-400">
                  <div>using: 3992 MB</div>
                <div>free: 6992 MB</div>
                <div>total: 9992 MB</div>
                </div>
                
              </div>
            </div>
            
            <div class="w-full rounded-r-md bg-zinc-900 p-2">
              <LinePlot {data} height="200" width="450" line_color="yellow" />
            </div>

          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<dialog
  id="dialog"
  class="text-white bg-zinc-900 rounded-md p-6 space-y-6 w-96"
>
  <div class="flex justify-between items-center">
    <div class="flex flex-col text-xl">New alert</div>

    <button
      onclick="dialog.close()"
      class="hover:text-blue-500 text-blue-300 active:text-purple-500"
    >
      <Icon
        icon="material-symbols-light:cancel-outline"
        width="32"
        height="32"
      />
    </button>
  </div>

  <div class="flex w-full items-center justify-center">DESKTOP-HBKSKL2</div>

  <form class="flex flex-col justify-start">
    <div class="flex w-full flex-col space-y-4">
      <div class="flex flex-col">
        <label for="alert_name">Alert name</label>
        <input
          placeholder="Example: Memory warning"
          id="alert_name"
          class="bg-zinc-800 rounded-md outline-none p-2"
          type="text"
        />
      </div>

      <div class="flex flex-col">
        <label for="cars">Choose metric</label>
        <select
          id="cars"
          name="cars"
          class="bg-zinc-800 rounded-md outline-none p-2"
        >
          <option value="volvo">RAM</option>
          <option value="saab">CPU</option>
          <option value="fiat">DATA SEND</option>
          <option value="audi">DATA RECEIVED</option>
        </select>
      </div>

      <div class="flex flex-col">
        <label for="trigger ">Set trigger (MB, MGZ)</label>
        <input
          class="bg-zinc-800 mt-1 rounded-md outline-none p-2"
          type="number"
          bind:value={b}
          min="0"
          max="999999"
        />
        <input class="p-2" type="range" bind:value={b} min="0" max="999999" />
      </div>

      <div class="flex flex-col">
        <label for="cars">Alert when...</label>
        <select
          id="cars"
          name="cars"
          class="bg-zinc-800 rounded-md outline-none p-2"
        >
          <option value="moreThan">RAM value > trigger</option>
          <option value="lessThan">RAM value &lt trigger</option>
          <option value="moreOrEqualsThan">RAM value >= trigger</option>
          <option value="lessOrEqualsThan">RAM value &lt= trigger</option>
        </select>
      </div>
    </div>

    <div class=" space-y-4 mt-6">
      <button
        onclick="dialog.close()"
        class="w-full rounded-md bg-green-800 hover:bg-green-600 active:bg-green-900 p-2"
      >
        accept
      </button>

      <button
        onclick="dialog.close()"
        class="w-full rounded-md bg-red-800 hover:bg-red-600 active:bg-red-900 p-2"
      >
        cancel
      </button>
    </div>
  </form>
</dialog>
