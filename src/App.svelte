<script>
	
	import { onMount } from "svelte";
	import { apiData, resp } from './app.js';
	function onSubmit(e) {
    const formData = new FormData(e.target);

    const data = {};
    for (let field of formData) {
      const [key, value] = field;
      data[key] = value;
    }
	switch (data.operator) {
		case ("+"):
			data.operator = "add";
			break;
		case ("-"):
			data.operator = "subtract";
			break;
		case ("*"):
			data.operator = "multiply";
			break;
		case ("/"):
			data.operator = "divide";
			break;
	}
	  (async () => {
	  var url = `http://localhost:3000/?first=${data.first}&condition=${data.operator}&second=${data.second}`;
	  console.log(url)
	  fetch(url)
	  .then(response => response.json())
	  .then(data => {
			console.log(data);
		apiData.set(data);
	  }).catch(error => {
		console.log(error);
		return [];
	  });
	})();
  }




	console.log('hi')

	function handleSubmit() {
		alert(`submitted ${pin}`);
	}


	</script>
	
	<main>
		<h1>Calculator thing</h1>

		<form on:submit|preventDefault={onSubmit}>
			<!-- ... -->
			<input  name="first" type="text" placeholder="first" required>
			<br>
			<input  name="operator" type="text" placeholder="operator" required>
			<br>
			<input  name="second" type="text" placeholder="second" required>
			<input type="submit">
		   </form>
		   
		<ul>
		{$resp}
		</ul>
	</main>
	
	<style>
	
	</style>

	