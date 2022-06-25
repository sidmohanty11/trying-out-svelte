<script>
  import Announcement from "./Announcement.svelte";
  import Fruit from "./Fruit.svelte";

  let name = "";
  let color = "";
  let fruitName = "";
  let src = "favicon.png";
  let count = 0;

  function increment() {
    count++;
  }

  // array of fruits with object as fruit item
  let fruits = [
    {
      id: 1,
      name: "apple",
      color: "red",
    },
    {
      id: 2,
      name: "banana",
      color: "yellow",
    },
    {
      id: 3,
      name: "orange",
      color: "orange",
    },
  ];

  $: totalFruits = fruits.length;

  function addFruit() {
    let fruit = {
      id: Math.floor(Math.random() * 100000),
      name: fruitName,
      color: color,
    };
    fruits.push(fruit);
    fruits = fruits;
  }

  // delete fruit by id
  function deleteFruit(id) {
    fruits = fruits.filter((fruit) => fruit.id !== id);
  }

  // reactive fullname
  $: fullname = `${name} ${count}`;
</script>

<main>
  <Announcement />
  <img {src} alt="favicon" />
  <h1>Hello {fullname}!</h1>
  <div>
    <h3>Counter: {count}</h3>
    <button on:click={increment}>Increment</button>
  </div>
  <input type="text" bind:value={name} placeholder="name" />
  <div>
    <h2>Fruits</h2>
    {#if totalFruits > 10}
      <p>There are too many fruits!</p>
    {:else}
      <input type="text" placeholder="fruitName" bind:value={fruitName} />
      <input type="text" placeholder="fruitColor" bind:value={color} />
      <button on:click={addFruit}>Add fruit</button>
    {/if}
    {#each fruits as fruit (fruit.id)}
      <Fruit {fruit} {deleteFruit} />
    {:else}
      <div>No fruits</div>
    {/each}
  </div>
</main>

<style>
  main {
    text-align: center;
  }
</style>
