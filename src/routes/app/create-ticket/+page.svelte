
<script>
    import Icon from "@iconify/svelte";
    import Navbar from "../../../lib/app/Navbar.svelte";

    let page_name = 'ticket';

</script>


<Navbar currentPage={page_name} />


<div class="flex w-full h-full mt-32 justify-start mx-8">

<div class="p-4 bg-zinc-800 rounded-xl text-white">
    
    <h1 class="text-white font-semibold text-m mb-2">
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
           
            <div class="flex">
                <div class="flex flex-col">   
                    <label for="emisor" class="text-white text-m font-light my-2">your name</label>
                    <input id="emisor" class="rounded-xl w-11/12 p-2 bg-zinc-900" type="text">
                </div>
    
    
                <div class="flex flex-col">   
                    <label for="emisor" class="text-white text-m font-light my-2">departament</label>
                    <input id="emisor" class="rounded-xl w-11/12 p-2 bg-zinc-900" type="text">
                </div>

                <div class="flex flex-col">   
                    <label for="emisor" class="text-white text-m font-light my-2">PC place or PC number</label>
                    <input id="emisor" class="rounded-xl w-96 p-2 bg-zinc-900" type="text">
                </div>
            </div>
                
                
            <div class="problem-description my-2 flex flex-col">
                <label for="emisor" class="text-white text-m font-light my-2">problem description</label>
                <textarea class="bg-zinc-900 rounded-xl p-2 h-96 resize-none" name="comment" form="ticket" placeholder="Enter your problem details here.."></textarea>
            </div>

            <div class="buttons flex justify-around mt-4">
                <button class="bg-red-600 text-white p-2 rounded-xl active:bg-red-900 border-none">Cancel</button>
                <button class="bg-blue-400 text-white p-2 rounded-xl active:bg-blue-900 border-none">Submit</button>
            </div>

        </form>
    </div>

    
</div>

</div>