<script>
    import { goto } from "$app/navigation";
    import { fade, slide } from "svelte/transition";
    let isMenuOpen = false;
    let isSidebarOpen = false;
    let loading = false;
  
    let profilePicture = `https://scontent.ftij3-2.fna.fbcdn.net/v/t39.30808-6/311693255_2099624763574076_8587080800396754404_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=efb6e6&_nc_eui2=AeE-oFIUGaD6Iyzvjqffa4IQ5gaAvgJA8JLmBoC-AkDwku2ZmAOlt179B_TAHV6abq5d-F9_3s-uN2Q2Wj8dbgAI&_nc_ohc=IfDfbbq7K5QAX8vJyLw&_nc_ht=scontent.ftij3-2.fna&oh=00_AfBLQYHoiojzEWPoGYVamYpE33uchArC-jUL0leQXUrp5w&oe=6582DF3E`;
  
    let userJson = `{
      "name": "Diego",
      "lastName": "Beltran",
      "secondLastName": "Lopez",
      "career": "Ing. Sistemas",
      "picture": "/images/dummy.jpg",
      "dateBirth": "1998-10-10",
      "controlNum": "20212390",
      "email": "20212390@tectijuana.edu.mx"
    }
    `;
  
    let user = JSON.parse(userJson);
  
    console.log(user);
  
    let completeName = `${user.name} ${user.lastName} ${user.secondLastName}`;
  
    /**
   * @param {string} modalName
   */
    function showModal(modalName) {
      const modal = document.getElementById(modalName);
      // @ts-ignore
      modal.showModal();
    }
  
    function toggleMenu() {
      isMenuOpen = !isMenuOpen;
    }
  
    function closeMenu() {
      isMenuOpen = false;
    }
  
    function toggleSidebar() {
      isSidebarOpen = !isSidebarOpen;
    }
  
    function closeSidebar() {
      isSidebarOpen = false;
    }
  
    function logOut() {
      loading = true;
      //localStorage.removeItem("token");
      setTimeout(() => {
        loading = false;
        goto("/auth/login");
      }, 1000);
    }
  </script>
  
  <!-- <aside
    class="{isSidebarOpen
      ? 'translate-x-0'
      : '-translate-x-full'} fixed top-0 left-0 h-full w-60 bg-gray-200 text-white transition-transform duration-300 ease-in-out"
  > -->
    <!-- Sidebar content goes here -->
    <!-- <div class="p-4">
      <div class="flex items-center justify-self-center">
        <button
          on:click={toggleSidebar}
          class="p-2 focus:outline-none focus:ring focus:border-blue-300 mr-2"
        >
          <svg
            width="50px"
            height="50px"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            class="w-5 h-5"
          >
            <path
              d="M20.7457 3.32851C20.3552 2.93798 19.722 2.93798 19.3315 3.32851L12.0371 10.6229L4.74275 3.32851C4.35223 2.93798 3.71906 2.93798 3.32854 3.32851C2.93801 3.71903 2.93801 4.3522 3.32854 4.74272L10.6229 12.0371L3.32856 19.3314C2.93803 19.722 2.93803 20.3551 3.32856 20.7457C3.71908 21.1362 4.35225 21.1362 4.74277 20.7457L12.0371 13.4513L19.3315 20.7457C19.722 21.1362 20.3552 21.1362 20.7457 20.7457C21.1362 20.3551 21.1362 19.722 20.7457 19.3315L13.4513 12.0371L20.7457 4.74272C21.1362 4.3522 21.1362 3.71903 20.7457 3.32851Z"
              fill="#0F0F0F"
            />
          </svg>
        </button>
        <img src="/images/logo_ITT.png" alt="logo" class="h-12 w-12" />
        <span class="text-xl font-bold text-gray-900">Asiscan ITT</span>
      </div>
      <div class="mt-10">
        <a
          class="flex items-center justify-self-start hover:bg-white hover:text-gray-900 rounded-md py-3 px-2"
          href="/app/home"
        >
          <i class="fa-solid fa-house text-gray-900"></i>
          <span class="text-xl font-bold text-gray-900 ml-3">Inicio</span>
        </a>
        <a
          class="flex items-center justify-self-start hover:bg-white hover:text-gray-900 rounded-md py-3 px-2"
          href="/"
        >
          <i class="fa-solid fa-house text-gray-900"></i>
          <span class="text-xl font-bold text-gray-900 ml-3">Reportes</span>
        </a>
        <a
          class="flex items-center justify-self-start hover:bg-white hover:text-gray-900 rounded-md py-3 px-2"
          href="/"
        >
          <i class="fa-solid fa-house text-gray-900"></i>
          <span class="text-xl font-bold text-gray-900 ml-3">Inbox</span>
        </a>
        <a
          class="flex items-center justify-self-start hover:bg-white hover:text-gray-900 rounded-md py-3 px-2"
          href="/"
        >
          <i class="fa-solid fa-house text-gray-900"></i>
          <span class="text-xl font-bold text-gray-900 ml-3">Media</span>
        </a>
        <a
          class="flex items-center justify-self-start hover:bg-white hover:text-gray-900 rounded-md py-3 px-2"
          href="/"
        >
          <i class="fa-solid fa-house text-gray-900"></i>
          <span class="text-xl font-bold text-gray-900 ml-3">Calendar</span>
        </a>
      </div>
    </div>
  </aside> -->


  <nav class=" dark:bg-black fixed w-full z-20 top-0 start-0 border-b dark:border-zinc-600">
   
    <div class="flex justify-between mx-auto p-4">
        <a href="https://flowbite.com/" class="flex items-center space-x-3 rtl:space-x-reverse">
            <img src="../images/logo.svg" class="h-92 m-0 p-0" alt="Flowbite Logo">
            
            <span class="self-center text-xl font-light whitespace-nowrap dark:text-white">
                summary
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
            <div class="w-full flex justify-end bg-zinc-800 rounded-full ">
                <div class="mx-4 flex items-center text-white text-sm ">
                    username
                </div>
                <div class="flex items-center bg-slate-800 rounded-full">
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