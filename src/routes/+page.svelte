<script>
	import Navbar from '$lib/Navbar.svelte';
	import Home from '$lib/Home.svelte';
	import Info from '$lib/Info.svelte';
	import Work from '$lib/Work.svelte';
	import Team from '$lib/Team.svelte';
	import Project from '$lib/Project.svelte';
	import Services from '$lib/Services.svelte';
	import Vision from '$lib/Vision.svelte';
	import About from '$lib/About.svelte';
	import Contact from '$lib/Contact.svelte';
</script>
<title>Descon</title>
<div class="w-full h-full bg-primary-900">
	<Navbar />

	<Home />
	<Info />
	<Work />

	<Team />

	<Project />
	<Services />
	<Vision />

	<About />
	<Contact />
</div>

<!-- ? Tailwind css -->

<!-- * Conditonal claseses in tailwind css -->

<!-- 
 <script>
  let toggle = true;
</script>

<button on:click={() =>
toggle = !toggle
  
  }>
  click me
</button>

<div 
class={`${toggle ? 'bg-green-900' : 'bg-red-900'} text-white`}


>
  this is my kindom
</div> -->

<!-- 
 <script>
let check ='';

 </script>

<input type="text" bind:value={check}>
<div class={check.length >= 6 ? "bg-green-900":"bg-red-600" }>writename</div> -->

<!-- 

 
🔸 Common Mistakes to Avoid
❌ Passing variables to a function and modifying only the parameter (doesn’t change original)
❌ Forgetting to directly update reactive variables (let x = y won't trigger reactivity)
❌ Putting logic directly in class="" without using class={} in Svelte/JSX  -->

<!-- ! in TailwindCss -->

<!-- 
<div class="  text-amber-700! text-red-800 text-9xl ">
  This text will be red, not gray.
</div> -->

<!-- ? For migration -->

<!-- 

npx @tailwindcss/upgrade

npx @tailwindcss/upgrade --force 

-->

<!-- * new things -->

<!-- 
<div class="columns-1 p-11 gap-2xl sm:columns-5">
  <img class="aspect-auto " src="./front.jpg" alt="" />
  <img class="aspect-square " src="./logo.png" alt="" />
  <img class="aspect-square " src="./front.jpg" alt="" />

  <img class="aspect-square " src="./front.jpg" alt="" />
  <img class="aspect-square " src="./logo.png" alt="" />
  <img class="aspect-square " src="./front.jpg" alt="" />
  <img class="aspect-3/2 " src="./front.jpg" alt="" />
  <img class="aspect-square " src="./logo.png" alt="" />
  <img class="aspect-square " src="./front.jpg" alt="" />
</div> -->

<!-- break after/before/inside -->

<!-- 
<div class="columns-2">
  <p>Well, let me tell you something, </p>
  <p >Sure, go ahead, laugh</p>
  <p class="break-after-column ">Maybe we can live without</p>
  <p>Look. If you think this is</p>
</div> -->

<!-- <div class="columns-2">
  <p>Well, let me tell you something, </p>
  <p class="break-inside-avoid-column">Sure, go ahead, laugh</p>
  <p>Maybe we can live without</p>
  <p>Look. If you think this is</p>
</div> -->

<!-- <div class="flex items-center p-24">
  <img src="./front.jpg"  alt="" class="w-24 rounded-full"/>
  <div class="px-3  cursor-pointer text-primary-500   font-heading place-content-center h-full  border-primary-300 border-l ">
    <strong>Andrew Alfred</strong>
    <span>Technical advisor</span>
  </div>
</div> -->

<!-- ! Svelte -->

<!-- ? runes -->

<!-- 
<script>
  let counts = [1, 5, 10, 1339, 2048];
</script>

{#each counts as count}
  <div class="px-3  cursor-pointer text-primary-500   font-heading place-content-center h-full  border-primary-300 border-l ">
    Count: {count}, Doubled: {count * 4}
  </div>
{/each}

 -->

<!-- $state -->

<!-- <script>
	let count = $state(0);
</script>

<button  onclick={() => count++} >
	clicks: {count}
</button> -->

<!-- 
<script>


	const todos = $state([
		{
			done: false,
			text: 'add more todos'
		},
		{
			ok: true
		}
	]);



	function toggleOk() {
		todos[1].ok = !todos[1].ok;
	}


</script>

<button onclick={toggleOk}>
	click
</button>

<div class="px-3  cursor-pointer text-primary-500   font-heading place-content-center h-full  border-primary-300 border-l ">
	{todos[1].ok ? 'true' : 'false'}
</div>

 -->
