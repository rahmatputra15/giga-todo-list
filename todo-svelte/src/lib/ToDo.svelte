<script>
  import logo from "../assets/svelte.svg";

  const text = "SVELTE TO-DO LIST";
  let new_task = "";
  let alert = false;
  let todos = [];

  const addTodo = () => {
    if (new_task.trim() !== "") {
      todos = [...todos, new_task];
      new_task = "";
      alert = false;
    } else {
      alert = true;
    }
  };

  const removeTodo = (index) => {
    todos = todos.filter((_, i) => i !== index);
    // todos.splice(index, 1);
    // todos = [...todos];
  };
</script>

<div class="max-w-md w-full p-4 bg-white rounded-2xl shadow-lg text-center">
  <img src={logo} alt="Logo Svelte" class="w-16 h-16 m-auto my-3" />
  <h1 class="text-xl font-bold mb-4">{text}</h1>
  <div class="flex flex-col items-center gap-2 mb-4">
    <input
      type="text"
      placeholder="Tambah tugas..."
      bind:value={new_task}
      on:keyup={(e) => e.key === "Enter" && addTodo()}
      class="w-full px-3 py-2 border rounded-lg focus:outline-none {alert
        ? 'border-red-500 focus:ring-1 focus:ring-red-500'
        : 'border-gray-300 focus:ring-1 focus:ring-blue-500'}"
    />
    {#if alert}
      <small class="text-red-500">Tugas tidak boleh kosong</small>
    {/if}
    <button
      class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg w-full"
      on:click={addTodo}>Tambah</button
    >
  </div>
  <div class="flex flex-col items-center">
    {#each todos as todo, index}
      <div
        class="flex justify-between items-center w-full p-3 mb-2 shadow-md border rounded-lg"
      >
        <span class="ps-2 text-start">{todo}</span>
        <button
          class="text-red-500"
          aria-label="Delete"
          on:click={() => removeTodo(index)}
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M12 9.75 14.25 12m0 0 2.25 2.25M14.25 12l2.25-2.25M14.25 12 12 14.25m-2.58 4.92-6.374-6.375a1.125 1.125 0 0 1 0-1.59L9.42 4.83c.21-.211.497-.33.795-.33H19.5a2.25 2.25 0 0 1 2.25 2.25v10.5a2.25 2.25 0 0 1-2.25 2.25h-9.284c-.298 0-.585-.119-.795-.33Z"
            />
          </svg>
        </button>
      </div>
    {/each}
  </div>
</div>

<style>
</style>
