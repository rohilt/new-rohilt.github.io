<script>
	import { blur, fade, fly, slide } from 'svelte/transition'
	export let name;
	let pageId = 0;
	let doneTransition = true;
	let showMenu = window.screen.availWidth >= 1024;
	let canMovePastHome = false;
	let showModal = false;
	const handleNextPage = () => {
		console.log("asdf")
		if (canMovePastHome && pageId === 0) {
			pageId++;
			doneTransition = false;
		}
	}
</script>

<div transition:fade class="page min-h-screen max-h-full flex flex-col select-none">
<nav transition:slide class="flex sticky top-0 items-center justify-between flex-wrap bg-white p-4 shadow z-10 bg-card-bg">
	<span class="w-1/6 text-black ml-3 mr-6 font-semibold font-display text-5xl select-none">R/T</span>
	<div class="block lg:hidden select-none">
		<button on:click={() => showMenu = !showMenu} class="flex items-center px-3 py-2 text-black-200 border-black-400 lg:hover:text-gray-500">
		<svg class="fill-current h-5 w-5" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
		</button>
	</div>
	{#if showMenu}
	<div transition:slide class="w-5/6 block flex-grow lg:flex lg:items-center lg:w-auto select-none">
		<div class="font-display lg:flex lg:justify-center text-sm lg:flex-grow">
		<a href="javascript:void(0)" on:click={() => {pageId = 0; doneTransition = false}} class="block mt-4 lg:inline-block lg:mt-0 text-2xl text-black-200 mr-8 lg:hover:font-semibold">
			Home
			{#if pageId === 0}
				<img transition:fade class="hidden lg:block object-contain h-2 w-10 mx-auto" src='underline2.svg' alt='R/T'/>
			{/if}
		</a>
		<a href="javascript:void(0)" on:click={() => {pageId = 1; doneTransition = false}} class="block mt-4 lg:inline-block lg:mt-0 text-2xl text-black-200 mr-8 lg:hover:font-semibold">
			About Me
			{#if pageId === 1}
				<img transition:fade class="hidden lg:block object-contain h-2 w-10 mx-auto" src='underline2.svg' alt='R/T'/>
			{/if}
		</a>
		<a href="javascript:void(0)" on:click={() => {pageId = 2; doneTransition = false}} class="block mt-4 lg:inline-block lg:mt-0 text-2xl text-black-200 mr-8 lg:hover:font-semibold">
			Experience
			{#if pageId === 2}
				<img transition:fade class="hidden lg:block object-contain h-2 w-10 mx-auto" src='underline2.svg' alt='R/T'/>
			{/if}
		</a>
		<a href="javascript:void(0)" on:click={() => {pageId = 3; doneTransition = false}} class="block mt-4 lg:inline-block lg:mt-0 text-2xl text-black-200 mr-8 lg:hover:font-semibold">
			Projects
			{#if pageId === 3}
				<img transition:fade class="hidden lg:block object-contain h-2 w-10 mx-auto" src='underline2.svg' alt='R/T'/>
			{/if}
		</a>
		</div>
	</div>
	<div transition:slide class="w-1/2 lg:w-1/6 justify-begin lg:justify-end flex self-end lg:self-auto mt-6 lg:mt-0 lg:items-center select-none">
	<!-- <a href="#" class="inline-block text-sm px-4 py-2 leading-none border rounded text-black border-black hover:border-transparent hover:text-black-500 hover:bg-white mt-4 lg:mt-0">Download</a> -->
		<a target="_blank" href="https://www.linkedin.com/in/rohiltuli/"><img class="object-contain h-16 w-16 p-4" src="linkedin2.png" alt="LinkedIn"/></a>
		<a target="_blank" href="https://github.com/rohilt"><img class="object-contain h-16 w-16 p-4" src="github2.png" alt="GitHub"/></a>
	</div>
	{/if}
</nav>

{#if showModal}
	<div transition:fade on:click={() => showModal = false} class="z-10 hidden w-full h-full flex flex-row bg-card-bg bg-opacity-75 lg:block fixed" />
	<div transition:fade class="flex-col lg:max-w-screen-md lg:mx-auto lg:my-40 fixed inset-0 w-auto h-auto flex bg-card-bg z-30 overflow-auto shadow-2xl rounded">
		<div class="flex content-right self-end h-10 w-10 pl-2 pr-4 pt-4 pb-2"><img src="close-line.png" alt="Close"/></div>
		<div class="font-display text-center text-xl">Details</div>
	</div>
{/if}

{#if pageId === 0 && doneTransition}
<style>
	.page {
		background-color: #fffefe;
		background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='4' height='4' viewBox='0 0 4 4'%3E%3Cpath fill='%23e5ddd5' fill-opacity='0.26' d='M1 3h1v1H1V3zm2-2h1v1H3V1z'%3E%3C/path%3E%3C/svg%3E");
	}
</style>
<main on:click={handleNextPage} out:fade on:outroend={() => doneTransition = true} in:fade="{{delay: 500}}" class="flex-1 pb-0 pt-16 px-16 lg:px-20 lg:py-16 align-middle select-none">
	<h1 class="font-display text-5xl lg:text-6xl"> Hello. I'm Rohil. </h1>
	<h1 class="font-display text-5xl lg:text-6xl">Welcome to my website. </h1>
	<div on:introstart={() => canMovePastHome = false} on:introend={() => canMovePastHome = true} out:fade in:fade="{{delay: 5000}}" class="hidden lg:block font-body mt-10 text-xl uppercase tracking-wider animate-pulse text-gray-600">Click anywhere to continue</div>
	<div on:introstart={() => canMovePastHome = false} on:introend={() => canMovePastHome = true} in:fade="{{delay: 5000}}" class="lg:hidden font-body text-center mt-10 text-xl uppercase tracking-wider animate-pulse text-gray-600">Tap to continue</div>
</main>
<img out:blur in:blur="{{delay: 250}}" class="hidden lg:block pin-b sticky bottom-0" src="mountain.png" alt="mountain" />
<!-- <img out:fade in:fade="{{delay: 250}}" class="lg:hidden pin-b sticky bottom-0" src="mountain-cropped.png" alt="mountain" /> -->
{:else if pageId === 1 && doneTransition}
<style>
	.page {
		background-color: #fffefe;
		background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='4' height='4' viewBox='0 0 4 4'%3E%3Cpath fill='%23e5ddd5' fill-opacity='0.26' d='M1 3h1v1H1V3zm2-2h1v1H3V1z'%3E%3C/path%3E%3C/svg%3E");
		/* background-image: url("data:image/svg+xml,%3Csvg width='6' height='6' viewBox='0 0 6 6' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='%23e5ddd5' fill-opacity='0.25' fill-rule='evenodd'%3E%3Cpath d='M5 0h1L0 6V5zM6 5v1H5z'/%3E%3C/g%3E%3C/svg%3E"); */
		/* background-color: #ffffff; */
		background-repeat: repeat;
		/* background-image: url("data:image/svg+xml,%3Csvg width='36' height='36' viewBox='0 0 36 36' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M36 0H0v36h36V0zM15.126 2H2v13.126c.367.094.714.24 1.032.428L15.554 3.032c-.188-.318-.334-.665-.428-1.032zM18 4.874V18H4.874c-.094-.367-.24-.714-.428-1.032L16.968 4.446c.318.188.665.334 1.032.428zM22.874 2h11.712L20 16.586V4.874c1.406-.362 2.512-1.468 2.874-2.874zm10.252 18H20v13.126c.367.094.714.24 1.032.428l12.522-12.522c-.188-.318-.334-.665-.428-1.032zM36 22.874V36H22.874c-.094-.367-.24-.714-.428-1.032l12.522-12.522c.318.188.665.334 1.032.428zm0-7.748V3.414L21.414 18h11.712c.362-1.406 1.468-2.512 2.874-2.874zm-18 18V21.414L3.414 36h11.712c.362-1.406 1.468-2.512 2.874-2.874zM4.874 20h11.712L2 34.586V22.874c1.406-.362 2.512-1.468 2.874-2.874z' fill='%23dcdcdc' fill-opacity='0.19' fill-rule='evenodd'/%3E%3C/svg%3E"); */
	}
</style>
<main out:fade on:outroend={() => doneTransition = true} in:fade="{{delay: 500}}" class="flex-1 lg:flex lg:flex-col p-10 lg:p-20 lg:pr-0 align-middle">
	<div class="lg:w-1/2">
		<h1 class="font-display text-4xl lg:text-5xl"> A little bit about me. </h1>
		<div class="pt-4 font-body text-xl">
			I'm currently a junior at the University of Florida, where I'm studying computer science and mathematics, and I interned at American Express this past summer.  
			<!-- <br /> -->
			I have experience with several programming languages and frameworks, and I'm always looking to learn more. 
			Right now, I'm learning more about Svelte (which this webpage is built with!). 
			<br />
			<br />
			You can find more about my background and the projects I've worked on throughout this webpage. 
			<!-- <br /> -->
			Feel free to reach out to me through email or LinkedIn. 
			I'm currently a junior at the University of Florida, where I'm studying computer science and mathematics, and I interned at American Express this past summer.  
			<!-- <br /> -->
			I have experience with several programming languages and frameworks, and I'm always looking to learn more. 
			Right now, I'm learning more about Svelte (which this webpage is built with!). 
			<br />
			<br />
			You can find more about my background and the projects I've worked on throughout this webpage. 
			<!-- <br /> -->
			Feel free to reach out to me through email or LinkedIn. 
			I'm currently a junior at the University of Florida, where I'm studying computer science and mathematics, and I interned at American Express this past summer.  
			<!-- <br /> -->
			I have experience with several programming languages and frameworks, and I'm always looking to learn more. 
			Right now, I'm learning more about Svelte (which this webpage is built with!). 
			<br />
			<br />
			You can find more about my background and the projects I've worked on throughout this webpage. 
			<!-- <br /> -->
			Feel free to reach out to me through email or LinkedIn. 
			I'm currently a junior at the University of Florida, where I'm studying computer science and mathematics, and I interned at American Express this past summer.  
			<!-- <br /> -->
			I have experience with several programming languages and frameworks, and I'm always looking to learn more. 
			Right now, I'm learning more about Svelte (which this webpage is built with!). 
			<br />
			<br />
			You can find more about my background and the projects I've worked on throughout this webpage. 
			<!-- <br /> -->
			Feel free to reach out to me through email or LinkedIn. 
		</div>
	</div>
	<div class="mt-10 lg:mt-0 lg:w-1/2 lg:flex lg:items-center lg:justify-center lg:fixed lg:self-end">
		<div class="max-w-xs rounded overflow-hidden shadow-lg bg-card-bg">
			<img class="hidden lg:block w-full" src="personal.png" alt="Rohil Tuli">
			<div class="px-6 py-4">
			  <div class="font-display text-2xl mb-2 lg:text-center">Rohil Tuli</div>
			</div>
			<div class="flex flex-col lg:items-center px-6 pb-4">
				<a target="_blank" href="https://goo.gl/maps/wLs676jT36KNsCGe7" class="flex my-2 bg-gray-100 rounded px-3 py-1 text-sm font-semibold text-grey-darker mr-2">
					<img class="fill-current self-center w-4 h-4 mr-2" src="location.svg" />
					Student at Gainesville, FL
				</a>
				<a target="_blank" href="mailto:rohil.tuli@gmail.com" class="flex my-2 bg-gray-100 rounded px-3 py-1 text-sm font-semibold text-grey-darker mr-2">
					<img class="fill-current self-center w-4 h-4 mr-2" src="mail.svg" />
					rohil.tuli@gmail.com
				</a>
				<a target="_blank" href="mailto:rohil.tuli@gmail.com" class="flex my-2 bg-gray-100 rounded px-3 py-1 text-sm font-semibold text-grey-darker">
					<img class="fill-current self-center w-4 h-4 mr-2" src="resume.svg" />
					PDF of Resume
				</a>
			</div>
		</div>
	</div>
</main>
{:else if pageId === 2 && doneTransition}
<style>
	.page {
		background-color: #fffefe;
		background-repeat: repeat;
		background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100' viewBox='0 0 100 100'%3E%3Cg fill-rule='evenodd'%3E%3Cg fill='%23dfdfdf' fill-opacity='0.16'%3E%3Cpath opacity='.5' d='M96 95h4v1h-4v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4h-9v4h-1v-4H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15v-9H0v-1h15V0h1v15h9V0h1v15h9V0h1v15h9V0h1v15h9V0h1v15h9V0h1v15h9V0h1v15h9V0h1v15h9V0h1v15h4v1h-4v9h4v1h-4v9h4v1h-4v9h4v1h-4v9h4v1h-4v9h4v1h-4v9h4v1h-4v9h4v1h-4v9zm-1 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-9-10h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm9-10v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-9-10h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm9-10v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-9-10h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm9-10v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-10 0v-9h-9v9h9zm-9-10h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9zm10 0h9v-9h-9v9z'/%3E%3Cpath d='M6 5V0H5v5H0v1h5v94h1V6h94V5H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
	}
</style>
<main out:fade on:outroend={() => doneTransition = true} in:fade="{{delay: 500}}" class="flex-1 p-10 lg:p-20 align-middle">
	<h1 class="font-display text-4xl lg:text-5xl"> Where I've learned </h1>
	<div class="pt-4 grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4">
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">The University of Florida</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Land O Lakes High School</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
		</div>
	</div>
	<h1 class="font-display text-4xl lg:text-5xl mt-4"> What I've been doing </h1>
	<div class="pt-4 grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4">
		<div on:click={() => showModal = true} class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95 cursor-pointer">
			<div class="px-6 py-4">
				<div class="font-display text-2xl mb-2">American Express</div>
				<div class="font-display text-xl mb-2 text-gray-700">Technology Intern</div>
				<div class="font-body font-thin uppercase tracking-wider text-sm mb-2 text-gray-600">July 2020 to August 2020</div>
				<button class="bg-transparent hover:bg-blue-500 bg-opacity-50 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-black border-opacity-50 hover:border-transparent rounded-full">
					...
				</button>
			<!-- <p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p> -->
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-2xl mb-2">Embedded Systems Lab</div>
			<div class="font-display text-xl mb-2 text-gray-600">Undergraduate Researcher</div>
			<!-- <p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p> -->
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Mathnasium</div>
			<div class="font-display text-l mb-2 text-gray-600">Instructor</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">FRC Team 5276</div>
			<div class="font-display text-l mb-2 text-gray-600">Lead Programmer</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">LOLHS Mu Alpha Theta</div>
			<div class="font-display text-l mb-2 text-gray-600">Vice President & Tutor</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
		</div>
		<!-- Sci Oly? Pasco County library volunteer? Feeding America??? -->
	</div>
</main>
{:else if pageId === 3 && doneTransition}
<style>
	.page {
		background-color: #fffefe;
		background-repeat: repeat;
		background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 304 304' width='304' height='304'%3E%3Cpath fill='%23dfdfdf' fill-opacity='0.16' d='M44.1 224a5 5 0 1 1 0 2H0v-2h44.1zm160 48a5 5 0 1 1 0 2H82v-2h122.1zm57.8-46a5 5 0 1 1 0-2H304v2h-42.1zm0 16a5 5 0 1 1 0-2H304v2h-42.1zm6.2-114a5 5 0 1 1 0 2h-86.2a5 5 0 1 1 0-2h86.2zm-256-48a5 5 0 1 1 0 2H0v-2h12.1zm185.8 34a5 5 0 1 1 0-2h86.2a5 5 0 1 1 0 2h-86.2zM258 12.1a5 5 0 1 1-2 0V0h2v12.1zm-64 208a5 5 0 1 1-2 0v-54.2a5 5 0 1 1 2 0v54.2zm48-198.2V80h62v2h-64V21.9a5 5 0 1 1 2 0zm16 16V64h46v2h-48V37.9a5 5 0 1 1 2 0zm-128 96V208h16v12.1a5 5 0 1 1-2 0V210h-16v-76.1a5 5 0 1 1 2 0zm-5.9-21.9a5 5 0 1 1 0 2H114v48H85.9a5 5 0 1 1 0-2H112v-48h12.1zm-6.2 130a5 5 0 1 1 0-2H176v-74.1a5 5 0 1 1 2 0V242h-60.1zm-16-64a5 5 0 1 1 0-2H114v48h10.1a5 5 0 1 1 0 2H112v-48h-10.1zM66 284.1a5 5 0 1 1-2 0V274H50v30h-2v-32h18v12.1zM236.1 176a5 5 0 1 1 0 2H226v94h48v32h-2v-30h-48v-98h12.1zm25.8-30a5 5 0 1 1 0-2H274v44.1a5 5 0 1 1-2 0V146h-10.1zm-64 96a5 5 0 1 1 0-2H208v-80h16v-14h-42.1a5 5 0 1 1 0-2H226v18h-16v80h-12.1zm86.2-210a5 5 0 1 1 0 2H272V0h2v32h10.1zM98 101.9V146H53.9a5 5 0 1 1 0-2H96v-42.1a5 5 0 1 1 2 0zM53.9 34a5 5 0 1 1 0-2H80V0h2v34H53.9zm60.1 3.9V66H82v64H69.9a5 5 0 1 1 0-2H80V64h32V37.9a5 5 0 1 1 2 0zM101.9 82a5 5 0 1 1 0-2H128V37.9a5 5 0 1 1 2 0V82h-28.1zm16-64a5 5 0 1 1 0-2H146v44.1a5 5 0 1 1-2 0V18h-26.1zm102.2 270a5 5 0 1 1 0 2H98v14h-2v-16h124.1zM242 149.9V160h16v34h-16v62h48v48h-2v-46h-48v-66h16v-30h-16v-12.1a5 5 0 1 1 2 0zM53.9 18a5 5 0 1 1 0-2H64V2H48V0h18v18H53.9zm112 32a5 5 0 1 1 0-2H192V0h50v2h-48v48h-28.1zm-48-48a5 5 0 0 1-9.8-2h2.07a3 3 0 1 0 5.66 0H178v34h-18V21.9a5 5 0 1 1 2 0V32h14V2h-58.1zm0 96a5 5 0 1 1 0-2H137l32-32h39V21.9a5 5 0 1 1 2 0V66h-40.17l-32 32H117.9zm28.1 90.1a5 5 0 1 1-2 0v-76.51L175.59 80H224V21.9a5 5 0 1 1 2 0V82h-49.59L146 112.41v75.69zm16 32a5 5 0 1 1-2 0v-99.51L184.59 96H300.1a5 5 0 0 1 3.9-3.9v2.07a3 3 0 0 0 0 5.66v2.07a5 5 0 0 1-3.9-3.9H185.41L162 121.41v98.69zm-144-64a5 5 0 1 1-2 0v-3.51l48-48V48h32V0h2v50H66v55.41l-48 48v2.69zM50 53.9v43.51l-48 48V208h26.1a5 5 0 1 1 0 2H0v-65.41l48-48V53.9a5 5 0 1 1 2 0zm-16 16V89.41l-34 34v-2.82l32-32V69.9a5 5 0 1 1 2 0zM12.1 32a5 5 0 1 1 0 2H9.41L0 43.41V40.6L8.59 32h3.51zm265.8 18a5 5 0 1 1 0-2h18.69l7.41-7.41v2.82L297.41 50H277.9zm-16 160a5 5 0 1 1 0-2H288v-71.41l16-16v2.82l-14 14V210h-28.1zm-208 32a5 5 0 1 1 0-2H64v-22.59L40.59 194H21.9a5 5 0 1 1 0-2H41.41L66 216.59V242H53.9zm150.2 14a5 5 0 1 1 0 2H96v-56.6L56.6 162H37.9a5 5 0 1 1 0-2h19.5L98 200.6V256h106.1zm-150.2 2a5 5 0 1 1 0-2H80v-46.59L48.59 178H21.9a5 5 0 1 1 0-2H49.41L82 208.59V258H53.9zM34 39.8v1.61L9.41 66H0v-2h8.59L32 40.59V0h2v39.8zM2 300.1a5 5 0 0 1 3.9 3.9H3.83A3 3 0 0 0 0 302.17V256h18v48h-2v-46H2v42.1zM34 241v63h-2v-62H0v-2h34v1zM17 18H0v-2h16V0h2v18h-1zm273-2h14v2h-16V0h2v16zm-32 273v15h-2v-14h-14v14h-2v-16h18v1zM0 92.1A5.02 5.02 0 0 1 6 97a5 5 0 0 1-6 4.9v-2.07a3 3 0 1 0 0-5.66V92.1zM80 272h2v32h-2v-32zm37.9 32h-2.07a3 3 0 0 0-5.66 0h-2.07a5 5 0 0 1 9.8 0zM5.9 0A5.02 5.02 0 0 1 0 5.9V3.83A3 3 0 0 0 3.83 0H5.9zm294.2 0h2.07A3 3 0 0 0 304 3.83V5.9a5 5 0 0 1-3.9-5.9zm3.9 300.1v2.07a3 3 0 0 0-1.83 1.83h-2.07a5 5 0 0 1 3.9-3.9zM97 100a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-48 32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm32 48a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm32-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0-32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm32 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16-64a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 96a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-144a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-96 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm96 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16-64a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-32 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zM49 36a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-32 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm32 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zM33 68a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-48a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 240a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16-64a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16-32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm80-176a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm32 48a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0-32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm112 176a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm-16 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zM17 180a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0 16a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm0-32a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16 0a3 3 0 1 0 0-6 3 3 0 0 0 0 6zM17 84a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm32 64a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm16-16a3 3 0 1 0 0-6 3 3 0 0 0 0 6z'%3E%3C/path%3E%3C/svg%3E");
	}
</style>
<main out:fade on:outroend={() => doneTransition = true} in:fade="{{delay: 500}}" class="flex-1 p-10 lg:p-20 align-middle">
	<h1 class="font-display text-4xl lg:text-5xl"> Some of the projects I've worked on. </h1>
	<div class="pt-4 grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4">
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">UF NeuroNav</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">JavaScript</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">ReactJS</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">NodeJS</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">MongoDB</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">API Integrations</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Agile</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Pascal Interpreter</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Haskell</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Test Driven Development</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Type Inference Mechanism</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Prolog</span>
			<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Test Driven Development</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Stack-Sortable Permutations</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Combinatorics</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Haskell</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">LaTeX</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">0h h1 Puzzle Solver</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Python</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">API Integrations</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Help Deliver</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Hackathon</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">ReactJS</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">GoLang</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">MongoDB</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">HeadsUp</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Hackathon</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">React Native</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">Anonym</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Hackathon</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">ReactJS</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Blockchain</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">GatorWealth</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Hackathon</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Flutter</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Dart</span>
			</div>
		</div>
		<div class="max-w-sm rounded overflow-hidden shadow-xl bg-white bg-opacity-95">
			<div class="px-6 py-4">
			<div class="font-display text-xl mb-2">RideShare</div>
			<p class="text-gray-700 text-base">
				Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia, nulla! Maiores et perferendis eaque, exercitationem praesentium nihil.
			</p>
			</div>
			<div class="px-6 py-4">
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Hackathon</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Python</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">Flask</span>
				<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-1">SQL</span>
			</div>
		</div>
	</div>
</main>
{/if}
</div>