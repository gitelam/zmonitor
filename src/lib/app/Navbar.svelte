<script>

    /**
   * @type {any}
   */
     export let currentPage;

</script>


  <nav class=" dark:bg-black fixed w-full z-20 top-0 start-0 border-b dark:border-zinc-600">
   
    <div class="flex justify-between mx-4 p-4">
        
        <a href="/" class="flex items-center space-x-3 rtl:space-x-reverse">
            <img src="../images/logo.svg" class="h-8 m-0 p-0" alt="Flowbite Logo">
            
            <span class="self-center text-xl font-light whitespace-nowrap dark:text-white">
                {currentPage}
            </span>

        </a>
   
   
        <div class="flex md:order-2 space-x-3 md:space-x-0 rtl:space-x-reverse">
            
            <form class="w-80 h-0 mx-8 p-0">   
                <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Search</label>
                <div class="relative">
                    <div class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none">
                        <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"/>
                        </svg>
                    </div>
                    <input type="search" id="default-search" class="block w-full p-2 ps-10 text-sm text-gray-900  rounded-full bg-gray-800 focus:ring-blue-500 focus:border-blue-500 dark:bg-zinc-800 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search Mockups, Logos..." required />
                </div>
            </form>
            
        <a href="#">
            <div class="w-full flex justify-end bg-zinc-800 rounded-full hover:bg-blue-400 active:bg-blue-800">
                <div class="mx-4 flex items-center text-white text-m ">
                    admin
                </div>
                <div class="flex items-center bg-gray-600 rounded-full ">
                    <p class="p-2 text-white text-sm font-light">
                        img
                    </p>
                </div>
            </div>
        </a>
        
      <button data-collapse-toggle="navbar-sticky" type="button" class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600" aria-controls="navbar-sticky" aria-expanded="false">
          <span class="sr-only">Open main menu</span>
          <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15"/>
          </svg>
      </button>


    </div>
   
    </div>
  </nav>