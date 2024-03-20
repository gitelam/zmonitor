<script>
  import Navbar from "$lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";


</script>

<div class="flex justify-center w-full h-full mt-32 justify-start mx-8">
  <img src="../images/logo.svg" class="h-12 m-0 p-0" alt="Flowbite Logo" />
</div>

<div class="flex justify-center w-full h-full mt-10 justify-start mx-8">
  <div class="p-8 w-96 bg-zinc-800 rounded-xl text-white">
    <h1
      class="text-white text-xl font-semibold text-m mb-2 flex justify-center"
    >
      Sing in
    </h1>

    <div class="form my-2 w-full m-full bg-zinc-800">
      <form name="ticket" class="flex flex-col">
        <div class="problem-description my-2 flex flex-col flex justify-center">
          <label for="emisor" class="text-white text-m font-light my-2"
            >Email or Username
          </label>
          <input
            type="Email"
            id="emisor"
            name="emisor"
            class="p-2 rounded-xl bg-zinc-900 text-white outline-cyan-500"
            placeholder="Ingrese username..."
          />
        </div>

        <div class="problem-description my-2 flex flex-col flex justify-center">
          <label for="emisor" class="text-white text-m font-light my-2"
            >Contraseña
          </label>
          <input
            type="password"
            id="emisor"
            name="emisor"
            class="p-2 rounded-xl bg-zinc-900 text-white outline-cyan-500"
            placeholder="Contraseña..."
          />
          <label
            class="text-right text-violet-400 mr-2 underline cursor-pointer"
            >Has olvidado la Contraseña</label
          >
        </div>

        <div class="buttons flex justify-around mt-4">
          <button
            class="bg-blue-400 text-white p-4 rounded-xl active:bg-blue-900 border-none"
            >Continuar</button
          >
        </div>
      </form>
    </div>
  </div>
</div>
