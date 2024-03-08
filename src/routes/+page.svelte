<script>
    import { tick } from 'svelte';
  
    let researchTopic = '';
    let showIdeas = false;
    let selectedIdea = null;
    let ideasSection;
    let selectedIdeaSection;
  
    async function handleClick() {
      showIdeas = true;
      await tick();
      ideasSection.scrollIntoView({ behavior: 'smooth' });
    }
  
    async function expandIdea(idea) {
      selectedIdea = idea;
      await tick();
      selectedIdeaSection.scrollIntoView({ behavior: 'smooth' });
    }
    function scrollToIdeas() {
    ideasSection.scrollIntoView({ behavior: 'smooth' });
  }
  </script>
  <main class="flex flex-col items-center justify-center min-h-screen bg-gradient-to-r from-gray-800 to-black animate-gradient">
    <div class="text-center">
      <h1 class="text-6xl font-bold text-white mb-8">Althea</h1>
      <div class="flex justify-center flex-row items-center w-full max-w-2xl">
        <label for="research-topic" class="text-white text-2xl font-semibold mb-2 pr-4 flex-shrink-0">Research topic</label>
        <div class="relative w-full">
          <input
            type="text"
            id="research-topic"
            class="px-4 py-2 rounded-md ring-white ring-1 bg-transparent focus:outline-none focus:ring-2 focus:ring-blue-500 text-white text-lg w-full"
            placeholder="Enter your research topic"
            bind:value={researchTopic}
          />
          {#if researchTopic}
            <button class="absolute inset-y-0 right-0 flex items-center pr-4" on:click={handleClick}>
              <svg class="h-6 w-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </button>
          {/if}
        </div>
      </div>
    </div>
  
    {#if showIdeas}
      <div bind:this={ideasSection} class="bg-gradient-to-r from-blue-800 to-gray-800 animate-gradient min-h-screen w-full flex justify-center items-center">
        <div class="flex justify-center flex-wrap items-center">
          <div class="text-white text-lg text-center font-semibold mx-4 my-2 px-6 py-4 bg-gray-700 rounded-md">
            <div>Idea 1</div>
            <button class="mt-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={() => expandIdea('Idea 1')}>Expand</button>
          </div>
          <div class="text-white text-center text-lg font-semibold mx-4 my-2 px-6 py-4 bg-gray-700 rounded-md">
            <div>Idea 2</div>
            <button class="mt-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={() => expandIdea('Idea 2')}>Expand</button>
          </div>
          <div class="text-white text-center text-lg font-semibold mx-4 my-2 px-6 py-4 bg-gray-700 rounded-md">
            <div>Idea 3</div>
            <button class="mt-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={() => expandIdea('Idea 3')}>Expand</button>
          </div>
        </div>
      </div>
    {/if}
  
    {#if selectedIdea}
    <div bind:this={selectedIdeaSection} class="bg-gradient-to-r from-green-800 to-blue-800 animate-gradient min-h-screen w-full flex justify-center items-center relative">
        <button class="absolute top-4 left-4 flex items-center" on:click={scrollToIdeas}>
          <svg class="h-6 w-6 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
          <span class="text-white ml-2">Back</span>
        </button>
        <div class="text-center">
          <h2 class="text-4xl font-bold text-white mb-4">{selectedIdea}</h2>
          <p class="text-white text-lg">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed non risus. Suspendisse lectus tortor, dignissim sit amet, adipiscing nec, ultricies sed, dolor. Cras elementum ultrices diam. Maecenas ligula massa, varius a, semper congue, euismod non, mi. Proin porttitor, orci nec nonummy molestie, enim est eleifend mi, non fermentum diam nisl sit amet erat. Duis semper. Duis arcu massa, scelerisque vitae, consequat in, pretium a, enim. Pellentesque congue. Ut in risus volutpat libero pharetra tempor. Cras vestibulum bibendum augue. Praesent egestas leo in pede. Praesent blandit odio eu lacus. Quisque pellentesque egestas pede.
          </p>
        </div>
      </div>
    {/if}
  </main>
  
  <style>
    @keyframes gradient {
      0% {
        background-position: 0% 50%;
      }
      50% {
        background-position: 100% 50%;
      }
      100% {
        background-position: 0% 50%;
      }
    }
  
    .animate-gradient {
      animation: gradient 15s ease infinite;
    }
  </style>