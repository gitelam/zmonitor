<script>
  import {
    axisBottom as d3_axisBottom,
    axisLeft as d3_axisLeft,
    scaleLinear as d3_scaleLinear,
    select as d3_select,
  } from "d3";
  import * as d3 from "d3";

  /**
   * @type {string | any[]}
   */

  export let type = "";

  /**
   * @type {string | any[]}
   */
  export let data;
  export let width = 300;
  export let height = 150;
  export let marginTop = 10;
  export let marginRight = 10;
  export let marginBottom = 20;
  export let marginLeft = 30;



  export let data_name = "data_name";
  export let path_fill_color = "green";
  export let line_color = "green";
  export let y_up_domain = 5;
 

  /**
   * @type {any}
   */
  let gx;
  /**
   * @type {any}
   */
  let gy;

  $: x = d3.scaleLinear(
    [0, data.length - 1],
    [marginLeft, width - marginRight]
  );

  $: y = d3
    .scaleLinear(d3.extent(data), [height - marginBottom, marginTop]);

  $: line = d3.line((/** @type {any} */ d, /** @type {any} */ i) => x(i), y);

  $: d3.select(gx).call(d3.axisBottom(x));
  $: d3.select(gy).call(d3.axisLeft(y));


    // Cambiar a función area para rellenar el área debajo de la línea
    $: area = d3.area()
                .x((/** @type {any} */ d, /** @type {any} */ i) => x(i))
                .y0(height - marginBottom)
                .y1((/** @type {any} */ d) => y(d));

</script>

<div
  class="align-middle items-center justify-center border-zinc-600 border-1 text-white "
>
  <svg {width} {height} >

    <g opacity={0.6} bind:this={gx} transform="translate(0,{height - marginBottom})" />
    <g opacity={0.6} bind:this={gy} transform="translate({marginLeft},0)" />

    <path fill={path_fill_color} opacity="0.2" d={area(data)} />
    <path
      fill=none
      opacity={0.3}
      stroke={line_color}
      stroke-width="1"
      d={line(data)}
    />

    <!-- <g fill="purple" stroke="currentColor" stroke-width="0">
      {#each data as d, i}
        <circle cx={x(i)} cy={y(d)} r="1" />
      {/each}
    </g> -->

  </svg>

  {#if type == "show_data"}
    <div class="w-full flex flex-col mx-2 p-2">
      <div class="font-semibold">{data_name}</div>
        <div class="flex">
          <div class="truncate w-16">
            {data[data.length - 1]} 
          </div>
          <div>
            MB/s
          </div>
        </div>
    </div>
  {/if}

</div>