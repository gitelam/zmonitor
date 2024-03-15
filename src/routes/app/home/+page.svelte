p<body class="bg-black">
</body>

<script>

    let num = 0;
    let dec = 0;

    //interval to make the number change every 2 seconds
    setInterval(() => {
        num = Math.floor(Math.random() * 100);
        dec = Math.floor(Math.random() * 100)
    }, 500);

</script>

<div class="internal-body flex place-content-center w-full h-full">
    <div class="board w-full mx-10 my-52 flex">
       
        <div class="w-full ml-4 h-96 p-4 bg-zinc-800 rounded-xl">
            <h1 class="text-white text-lg font-bold">System monitor</h1>
            <div class="charts">
                <p class="text-white">
                    Velocidad de descarga: <span id="randomNumber">{num}.{dec}</span> kbps
                </p>
            </div>
        </div>

        <div class="ticket-section ml-8 w-full flex justify-around">
            <div class="new-tickets w-96 h-96 p-4 bg-zinc-800 rounded-xl">
                <h1 class="text-white text-lg font-bold">new tickets</h1>
                
                <div class="mt-2">
                    
                    <!-- <p class="text-gray-500">here start my list</p> -->
                    
                    <div class="item-list flex items-center border-b p-2">
                        <p class="text-white m-3">icon</p>
                        <div>
                            <p class="text-white mx-2 font-bold">0001 - LB1S SISTEMAS</p>
                            <p class="text-white mx-2 text-sm font-light">feb 23, 2023</p>
                        </div>
                    </div>

                </div>

            </div>
            <div class="standby-tickets w-96 h-96 p-4 bg-zinc-800 rounded-xl">
                <h1 class="text-white text-lg font-bold">stanby tickets</h1>

                <div class="mt-2">
                    
                    <!-- <p class="text-gray-500">here start my list</p> -->
                    
                    <div class="item-list flex items-center border-b p-2">
                        <p class="text-white m-3">icon</p>
                        <div>
                            <p class="text-white mx-2 font-bold">0001 - LB1S SISTEMAS</p>
                            <p class="text-white mx-2 text-sm font-light">feb 23, 2023</p>
                        </div>
                    </div>

                </div>


            </div>
        </div>
    </div>
</div>
