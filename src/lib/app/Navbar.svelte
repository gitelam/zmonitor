<script>
  //import icon from iconify
  import Icon from "@iconify/svelte";

  import Dialog from "./Dialog.svelte";

  /**
   * @type {any}
   */
  export let currentPage;

  /**
   * @type {any}
   */

  let notifications = 1;

  let isDropdownOpen = false; // default state (dropdown close)

  // @ts-ignore
  const handleDropdownClick = () => {
    isDropdownOpen = !isDropdownOpen; // togle state on click
    notifications = 0;
  };

  // @ts-ignore
  const handleDropdownFocusLoss = ({ relatedTarget, currentTarget }) => {
    // use "focusout" event to ensure that we can close the dropdown when clicking outside or when we leave the dropdown with the "Tab" button
    if (
      relatedTarget instanceof HTMLElement &&
      currentTarget.contains(relatedTarget)
    )
      return; // check if the new focus target doesn't present in the dropdown tree (exclude ul\li padding area because relatedTarget, in this case, will be null)
    isDropdownOpen = false;
  };
</script>

<nav
  class=" dark:bg-black fixed w-full z-20 top-0 start-0 border-b dark:border-zinc-600"
>
  <div class="flex justify-between mx-4 p-4">
    <a href="/" class="flex items-center space-x-3 rtl:space-x-reverse">
      <img src="../images/logo.svg" class="h-8 m-0 p-0" alt="Flowbite Logo" />

      <span
        class="self-center text-xl font-light whitespace-nowrap dark:text-white"
      >
        {currentPage}
      </span>
    </a>

    {#if currentPage == "summary"}
      <!-- <div class="flex justify-end w-full">
                <button on:click={()=>dialog.showModal()} class="flex text-white  font-medium space-x-2 bg-blue-300 rounded-2xl p-1">
                
                    <Icon icon="mdi:bell" width="24" height="24" />
                
                    <div class="border-l px-2">
                        notifications
                    </div>

                </button>
            </div>

            <Dialog bind:dialog on:close={()=>console.log('closed')}>
                <div>
                    i am the dialog
                </div>
            </Dialog> -->

      <div class="flex justify-end w-full space-y-8">
        <div
          class="flex dropdown items-center"
          on:focusout={handleDropdownFocusLoss}
        >
          <!-- {#if notifications == 1}
                    
                    <div class="flex items-center px-2 outline outline-red-500 rounded-xl border-solid border-1 border-red-200">
                        <div class="">
                            <Icon icon="mdi:circle" width="12" height="12" color="red" />
                        </div>
                        <button class="btn m-1 " on:click={handleDropdownClick} >
                       
                            {#if isDropdownOpen}
                                <Icon icon="mdi:bell" width="24" height="24" color="white"/>
                            {:else}
                                <Icon icon="mdi:bell" width="24" height="24" color="grey"/>
                            {/if}
    
                        </button>     

                    </div>
                    {/if} -->

          <div class="flex items-center px-2 rounded-xl">
            <div class="">
              <Icon icon="mdi:circle" width="12" height="12" color="red" />
            </div>
            <button class="btn mx-1" on:click={handleDropdownClick}>
              {#if isDropdownOpen}
                <div class="relative z-10 border-zinc-500 bg-black">
                  <Icon icon="mdi:bell" width="24" height="24" color="white" />
                </div>
              {:else}
                <Icon icon="mdi:bell" width="24" height="24" color="grey" />
              {/if}
            </button>
          </div>
        </div>

        <div
          class="absolute dropdown-content menu rounded-box -top-5"
          style:visibility={isDropdownOpen ? "visible" : "hidden"}
        >
          <div
            class="w-full h-full p-2 bg-black rounded-xl text-white outline-1 outline-double outline-zinc-500"
          >
            <div class=" space-y-4">
              <h2 class="font-bold">Notifications</h2>

              <div class="list">
                <a href="#">
                  <div class="item-list space-x-4 hover:bg-zinc-700 rounded-xl">
                    <div
                      class="flex body border-zinc-600 p-2 justify-center items-center h-full space-x-4"
                    >
                      <div class="flex">
                        <Icon icon="mdi:check-all" width="24" height="24" />
                      </div>

                      <div class="space-y-2">
                        <p class="font-bold">01 - Lab PC 2039</p>
                        <div>
                          checked by John on
                          <div class="italic">Sat Mar 16 2024 9:46:28 PM</div>
                        </div>
                      </div>

                      <div class="space-y-2">
                        <p class="font-bold"></p>
                        <Icon
                          icon="mdi:keyboard-arrow-right"
                          width="24"
                          height="24"
                        />
                      </div>
                    </div>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    {/if}

    <div class="flex md:order-2 space-x-3 md:space-x-0 rtl:space-x-reverse">
      <form class="w-80 h-0 mx-8 p-0">
        <label
          for="default-search"
          class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white"
          >Search</label
        >
        <div class="relative">
          <div
            class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
          >
            <svg
              class="w-4 h-4 text-gray-500 dark:text-gray-400"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 20 20"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
              />
            </svg>
          </div>
          <input
            type="search"
            id="default-search"
            class="block w-full p-2 ps-10 text-sm text-gray-900 rounded-full bg-gray-800 focus:ring-blue-500 focus:border-blue-500 dark:bg-zinc-800 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Search Mockups, Logos..."
            required
          />
        </div>
      </form>

      <a href="#">
        <div
          class="w-full flex justify-end bg-zinc-800 rounded-full hover:bg-blue-400 active:bg-blue-800"
        >
          <div class="mx-4 flex items-center text-white text-m">admin</div>
          <div class="flex items-center bg-gray-600 rounded-full">
            <p class="p-2 text-white text-sm font-light">img</p>
          </div>
        </div>
      </a>

      <button
        data-collapse-toggle="navbar-sticky"
        type="button"
        class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
        aria-controls="navbar-sticky"
        aria-expanded="false"
      >
        <span class="sr-only">Open main menu</span>
        <svg
          class="w-5 h-5"
          aria-hidden="true"
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 17 14"
        >
          <path
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M1 1h15M1 7h15M1 13h15"
          />
        </svg>
      </button>
    </div>
  </div>
</nav>
