<script>
  let todos = [];
  let todo = { id: "", text: "", completed: false };

  const addTodo = () => {
    if (!todo.texto.trim()) {
      todo.texto = "";
      return;
    }
    todo.id = Date.now();
    todos = [...todos, todo];
    todo = { id: "", text: "", completed: false };
  };

  const delTodo = id => {
	todos = todos.filter((item) => item.id !== id);
	todo = { id: "", text: "", completed: false };
  };

const editTodo = id => {
	todos = todos.map((item) => 
	item.id === id ?
	{...item, completed: !item.completed} :
	item
	);
};

</script>

<div class="container">
  <h1 class="display-5 my-3">CRUD</h1>

  <form on:submit|preventDefault={addTodo}>
    <input
      type="text"
      placeholder="Add Todo"
      class="from-control shadow border-0"
      bind:value={todo.texto}
    />
  </form>

  {#each todos as item}
    <div class="shadow my-3 p-3">
      <p
	  class={item.completed ? "text-decoration-line-through" : ""}
	  >{item.texto}</p>
      <button class="btn btn-sm btn-warning" on:click={editTodo(item.id)}>
        <span>
			<i class="bi bi-check-circle-fill"></i>
          Edit
        </span>
      </button>
      <button class="btn btn-sm btn-danger" on:click={delTodo(item.id)}>
        <span>
          <i class="bi bi-trash-fill" />
          Delete
        </span>
      </button>
    </div>
  {/each}
</div>
