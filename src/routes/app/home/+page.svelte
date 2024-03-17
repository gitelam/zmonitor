<script>
  import Navbar from "../../../lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";

  //axios import
  import axios from "axios";

  //svelte onmount import
  import { onMount } from "svelte";

  // svelte onmount method
  onMount(() => {
    get_data();
  });

  let num = 0;
  let dec = 0;

  //interval to make the number change every 2 seconds
  setInterval(() => {
    num = Math.floor(Math.random() * 100);
    dec = Math.floor(Math.random() * 100);
  }, 500);

  //unsolved tickets
  let unsolved_tickets = {};

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
  <div class="board w-full mx-8 mt-24">
    <div class="w-full h-96 p-4 mr-8 bg-zinc-800 rounded-xl">
      <h1 class="text-white text-lg font-bold">system monitor</h1>
      <div class="charts">
        <p class="text-white">
          download speed: <span id="randomNumber">{num}.{dec}{num}</span>
          kbps
        </p>
      </div>
    </div>

    <div class="ticket-section mt-4 flex">
      <!--do iterable lis with svelte with the unsolved_tickets set-->
      <div class="unsolved-tickets w-96 h-96 p-4 mr-4 bg-zinc-800 rounded-xl">
        <h1 class="text-white text-lg font-bold">unsolved tickets</h1>
        <div class="mt-2 overflow-auto max-h-92">
          {#each Object.values(unsolved_tickets) as ticket}
            <a href="#">
              <div
                class="{ticket.id == 7 ? 'item-list flex items-center border-b p-2 hover:bg-slate-800' : 'item-list flex items-center border-b p-2 hover:bg-slate-800'}"
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

      <!-- <div class="unsolved-tickets w-96 h-96 p-4 mr-4 bg-zinc-800 rounded-xl">
        <h1 class="text-white text-lg font-bold">recent tickets</h1>

        <div class="mt-2">
          <a href="#">
            <div
              class="item-list flex items-center border-b p-2 hover:bg-slate-800"
            >
              <p class="text-white m-3">
                <Icon
                  icon="material-symbols-light:warning-outline-rounded"
                  width="38"
                  height="38"
                />
              </p>

              <div class="w-full">
                <p class="text-white mx-2 font-bold">0001 - LB1S SISTEMAS</p>
                <p class="text-white mx-2 text-sm font-light">feb 23, 2023</p>
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
        </div>
      </div> -->

      <div class="standby-tickets mr-4 h-96 p-4 bg-zinc-800 rounded-xl">
        <h1 class="text-white text-lg font-bold">stanby tickets</h1>

        <div class="mt-2">
          <a href="#">
            <div
              class="item-list flex items-center border-b p-2 hover:bg-slate-800"
            >
              <p class="text-white m-3">
                <Icon
                  icon="material-symbols-light:browse-gallery-outline"
                  width="38"
                  height="38"
                />
              </p>

              <div class="w-full">
                <p class="text-white mx-2 font-bold">0001 - LB1S SISTEMAS</p>
                <p class="text-white mx-2 text-sm font-light">feb 23, 2023</p>
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
        </div>
      </div>

      <div class="standby-tickets h-96 p-4 bg-zinc-800 rounded-xl">
        <h1 class="text-white text-lg font-bold">solved tickets</h1>

        <div class="mt-2">
          <a href="#">
            <div
              class="item-list flex items-center border-b p-2 hover:bg-slate-800"
            >
              <p class="text-white m-3">
                <Icon
                  icon="material-symbols-light:check"
                  width="38"
                  height="38"
                />
              </p>

              <div class="w-full">
                <p class="text-white mx-2 font-bold">0001 - LB1S SISTEMAS</p>
                <p class="text-white mx-2 text-sm font-light">feb 23, 2023</p>
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
        </div>
      </div>
    </div>
  </div>
</div>
