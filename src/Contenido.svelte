<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Profesores  from "./Profesores.svelte";
  import Asignaturas   from "./Asignaturas.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/profesores" component={profesores} />
  <Route path="/asignaturas" component={asignaturas} />
</main>
