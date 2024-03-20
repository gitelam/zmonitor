<script>

    import Icon from "@iconify/svelte";
    import Navbar from "../../../lib/app/Navbar.svelte";
    import axios from 'axios';


let data = {
    emisor: "",
    section: "",
    place: "",
    description: "",
    date_creation: new Date().toISOString()
}


//clear data with vacuum string method
const clear_data = () => {
    data.emisor = "";
    data.section = "";
    data.place = "";
    data.description = "";
}

const validar_espacios = () => {
    if(data.emisor.replaceAll(" ","")==="" ||  data.emisor===("")){
        alert("Campo nombre no valido");
        throw new Error("Campo Nombre no valido");
    }else if(data.section.replaceAll(" ","")==="" ||  data.section===("")){
        alert("Campo nombre no valido");
        throw new Error("Campo nombre no valido");
    }else if(data.place.replaceAll(" ","")==="" ||  data.place===("")){
        alert("Campo departamento no valido");
        throw new Error("Campo departamento no valido");
    }else if(data.description.replaceAll(" ","")==="" ||  data.description===("")){
        alert("Campo descripción no valido");
        throw new Error("Campo descripción no valido");
    }else if(data.description.length<50){
        alert("Campo descripción muy corto");
        throw new Error("Campo descripción muy corto");
    }
}

//axios post method
const create_ticket = async () => {
    validar_espacios();
    /*if(data.emisor == "" || data.section == "" || data.place == "" || data.description == ""){
        alert("please fill all the fields");
        return;
    }*/

    try {

        const response = await axios.post('http://localhost:8000/create_ticket', data);
        console.log(response);
        
        if(response.status == 201){
            clear_data();
            alert("ticket created successfully");
        }

    } catch (error) {
        console.error(error);
    }
};

</script>

<Navbar currentPage={"tickets"} />

<div class="flex w-full h-full mt-24 justify-start px-8">

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
        <form name="ticket"  class="flex flex-col">
            
            <div class="flex">
                
                <div class="flex flex-col">   
                    <label for="name" class="text-white text-m font-light my-2">your name</label>
                    <input id="name" class="rounded-xl w-11/12 p-2 bg-zinc-900" type="text" placeholder="name..." bind:value={data.emisor} >
                </div>
    
                <div class="flex flex-col">   
                    <label for="departament" class="text-white text-m font-light my-2" >departament</label>
                    <input id="departament" class="rounded-xl w-11/12 p-2 bg-zinc-900" type="text" placeholder="work area..." bind:value={data.section}>
                </div>

                <div class="flex flex-col">   
                    <label for="pc_place" class="text-white text-m font-light my-2">PC place or PC number</label>
                    <input id="pc_place" class="rounded-xl w-96 p-2 bg-zinc-900" type="text" placeholder="how to found the pc..." bind:value={data.place}>
                </div>

            </div>
                
            <div class="problem-description my-2 flex flex-col">
                <label for="problem" class="text-white text-m font-light my-2">problem description</label>
                <textarea id="problem" class="bg-zinc-900 rounded-xl p-2 h-52 resize-none" name="comment" form="ticket" placeholder="enter your problem details here.." bind:value={data.description}></textarea>
            </div>

            <div class="buttons flex justify-between mt-4 mx-2">
                <button class="bg-red-500 text-white p-2 rounded-xl active:bg-red-900 border-none hover:bg-red-600 w-32">Cancel</button>
                <button on:click={create_ticket} class="bg-blue-400 text-white p-2 rounded-xl active:bg-blue-900 border-none hover:bg-blue-500 w-32">Submit</button>
            </div>

        </form>
    </div>

    
</div>

</div>