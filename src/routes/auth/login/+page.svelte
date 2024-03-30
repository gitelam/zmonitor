<script>
  import { goto } from "$app/navigation";
  import Navbar from "$lib/app/Navbar.svelte";
  import Icon from "@iconify/svelte";
  
  let log = {
    passw: "",
    correo: ""
  }

  const clear_log = () => {
    log.correo = "";
    log.passw = "";
  }

  function go_ticket(){
    
    window.location.href ="http://localhost:5173/app/create-ticket";
    
  }

  const validar_log = () => {
    //const emisorA = data.emisor.replaceAll(" ","");
    if(log.correo.replaceAll(" ","")==="" ||  log.correo===("")){
        alert("Campo correo no valido");
        throw new Error("Campo correo no valido");
    }else if(log.passw.replaceAll(" ","")==="" ||  log.passw===("")){
        alert("Campo contraseña no valido");
        throw new Error("Campo contraseña no valido");
    }else if(!(log.correo.endsWith("@gmail.com") || log.correo.endsWith("@tectijuana.edu.mx") || log.correo.endsWith("@tijuana.tecnm.mx"))){
        alert("Dominio de correo no valido");
        throw new Error("Dominio de correo no valido");
    }
  }

  const Iniciar_Sesion = () =>{
    validar_log();
    if((log.correo==="prueba@gmail.com" || log.correo==="prueba@tectijuana.edu.mx" || log.correo==="prueba@tijuana.tecnm.mx")
        && log.passw==="PasswPrueba"){
          go_ticket();
          console.log("Ingresó correctamente");
      }else{
        alert("Contraseña y/o usuario no valido");
        throw new Error("Contraseña y/o usuario no valido");
      }
  }
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
          <label for="Email" class="text-white text-m font-light my-2"
            >Email or Username
          </label>
          <input
            type="Email"
            id="Email"
            name="Email"
            class="p-2 rounded-xl bg-zinc-900 text-white outline-cyan-500"
            placeholder="Ingrese username..."
            bind:value={log.correo}
          />
        </div>

        <div class="problem-description my-2 flex flex-col flex justify-center">
          <label for="Pssw" class="text-white text-m font-light my-2"
            >Contraseña
          </label>
          <input
            type="password"
            id="Pssw"
            name="Pssw"
            class="p-2 rounded-xl bg-zinc-900 text-white outline-cyan-500"
            placeholder="Contraseña..."
            bind:value={log.passw}
          />
          <label
            class="text-right text-violet-400 mr-2 underline cursor-pointer"
            >Has olvidado la Contraseña</label
          >
        </div>

        <div class="buttons flex justify-around mt-4">
          <button
            class="bg-blue-400 text-white p-4 rounded-xl active:bg-blue-900 border-none"
            on:click={Iniciar_Sesion}
            >Continuar</button
          >
        </div>
      </form>
    </div>
  </div>
</div>