<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Profesor                from "./Profesor.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let profesor = {};

  onMount(async () => {
    const response = await fetch(URL.profesores);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.modelo))
    : $jsonData;

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>Profesores</h1>
<Buscar bind:busqueda />

<div class="container">
  <Profesor bind:profesor>
    <div style="text-align: right">
      <Boton documento={profesor} tipo="insertar" coleccion="profesores" />
    </div>
  </Profesor>
</div>

<div class="container">
  {#each datos as profesor}
    <Profesor {profesor}>
      <div style="text-align: right">
        <Boton documento={profesor} tipo="modificar" coleccion="profesores" />
        <Boton documento={profesor} tipo="eliminar"  coleccion="profesores" />
      </div>
    </Profesor>
  {/each}
</div>
