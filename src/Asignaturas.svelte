<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Asignatura                from "./Asignatura.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let asignatura = {};

  onMount(async () => {
    const response = await fetch(URL.asignaturas);
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

<h1>Asignatura</h1>
<Buscar bind:busqueda />

<div class="container">
  <Asignatura bind:asignatura>
    <div style="text-align: right">
      <Boton documento={asignatura} tipo="insertar" coleccion="asignaturas" />
    </div>
  </Asignatura>
</div>

<div class="container">
  {#each datos as asignatura}
    <Asignatura {asignatura}>
      <div style="text-align: right">
        <Boton documento={asignatura} tipo="modificar" coleccion="asignaturas" />
        <Boton documento={asignatura} tipo="eliminar"  coleccion="asignaturas" />
      </div>
    </Asignatura>
  {/each}
</div>