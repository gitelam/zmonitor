<script>
    import Navbar from "$lib/app/Navbar.svelte";
    import Icon from "@iconify/svelte";
</script>

<Navbar currentPage="TestAnto" />


<div class="flex justify-center w-full h-full mt-32 justify-start mx-8">

    <div class="p-4 bg-zinc-800 rounded-xl text-white">
        
        <h1 class="text-white font-semibold text-m mb-2 ">
            Create a ticket
        </h1>
    
        <div class="caution-info flex bg-gray-700 rounded-xl p-2 items-center">
            <Icon icon="material-symbols:info-outline-rounded" width="24" height="24" />
            <p class="text-white text-sm mx-2">
                Caution: this generate a ticket in the system for a problem, please be sure to fill all the fields and be detailed.
            </p>
        </div>
        
        <div class="form my-2 w-full">
            <form name="ticket" class="flex flex-col">
               
               <div class="p-8">
                <div class="flex gap-20 content-start ">
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">Nombre</label>
                        <label  class="text-neutral-400 text-sm">Antonio PC</label>
                    </div>
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">Hora</label>
                        <label  class="text-neutral-400 text-sm">9:10 </label>
                    </div>
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">Departamento</label>
                        <label  class="text-neutral-400 text-sm">ISCI</label>
                    </div>
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">IP</label>
                        <label  class="text-neutral-400 text-sm">172.43.32.02.1</label>
                    </div>
        
                </div>

                <div class="flex gap-20 content-start mt-8">
                    <div class="flex flex-col ">   
                        <label class="text-white text-m font-light my-2">Fecha</label>
                        <label  class="text-neutral-400 text-sm">12-04-2024</label>
                    </div>
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">Remitente</label>
                        <label  class="text-neutral-400 text-sm">Vasquez  Antonio</label>
                    </div>
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">Numero de maquina</label>
                        <label  class="text-neutral-400 text-sm">32</label>
                    </div>
                    <div class="flex flex-col">   
                        <label class="text-white text-m font-light my-2">Lugar de PC</label>
                        <label  class="text-neutral-400 text-sm">Laboratorio 12 </label>
                    </div>
        
                </div>

               </div>
                    
                <div class="problem-description my-2 flex flex-col flex justify-center">
                    <label for="emisor" class="text-white text-m font-light my-2">Problema</label>
                    <textarea class="bg-zinc-900 rounded-xl p-2 h-96 resize-none" name="comment" form="ticket" ></textarea>
                </div>
    
                <div class="buttons flex justify-around mt-4">
                    <button class="bg-red-600 text-white p-2 rounded-xl active:bg-red-900 border-none">Cancel</button>
                    <button class="bg-blue-400 text-white p-2 rounded-xl active:bg-blue-900 border-none">Submit</button>
                </div>
    
            </form>
        </div>
    
        
    </div>
    
    </div>