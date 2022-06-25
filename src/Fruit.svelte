<script>
  export let fruit;
  export let deleteFruit;
</script>

<div>
  <h5 style={`background-color: ${fruit.color};padding:10px;`}>
    {fruit.name}
    <button on:click={() => deleteFruit(fruit.id)}>X</button>
  </h5>
</div>

<style>
</style>
