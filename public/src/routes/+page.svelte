<script lang="ts">
  import { onMount } from 'svelte';
  
  // Define proper types for our data
  interface PromptTemplate {
    id: string;
    name: string;
    path: string;
  }
  
  interface Step {
    id: string;
    title: string;
    description: string;
    link?: string;
    linkText?: string;
    content?: PromptTemplate[];
    contentType?: 'prompts' | 'markdown';
  }

  // Import prompt templates and markdown outputs
  const promptTemplates: PromptTemplate[] = [
    { id: 'chatGPT-prompt-1', name: 'ChatGPT Prompt 1', path: '/chatGPT-prompt-1.md' },
    { id: 'chatGPT-prompt-2', name: 'ChatGPT Prompt 2', path: '/chatGPT-prompt-2.md' },
    { id: 'chatGPT-prompt-3', name: 'ChatGPT Prompt 3', path: '/chatGPT-prompt-3.md' }
  ];

  const markdownOutputs: PromptTemplate[] = [
    { id: 'melaka-prompt-1', name: 'Melaka Output 1', path: '/melaka-prompt-1.md' },
    { id: 'melaka-prompt-2', name: 'Melaka Output 2', path: '/melaka-prompt-2.md' },
    { id: 'plus-prompt-3', name: 'Plus Output 3', path: '/plus-prompt-3.md' }
  ];

  // External links
  const rawDataLink = 'https://docs.google.com/spreadsheets/d/1xGabr65sYrTTuZb2URsm6wfHUPbXdK9ULOBId5kt3hE/edit?usp=sharing';
  const xmindLink = 'https://xmind.ai/share/ofCt9Dkk?xid=Wp7vW9UI';
  const smartArtLink = 'https://docs.google.com/presentation/d/1_W5DeYmnTuMOX-RluyshK26ndUQrwGfL/edit?usp=drive_link&ouid=101657559488423790022&rtpof=true&sd=true';
  const videoLink = 'https://drive.google.com/file/d/1yicW1DLJY_11eLrmV6b1rLsqF-HkGaau/view?usp=sharing';
  const folderLink = 'https://drive.google.com/drive/folders/1yBkI2Wea95dlJ2svK4vAYr_4YONYvG5N?usp=drive_link';

  // State for active tabs and sections
  let activePrompt: PromptTemplate = promptTemplates[0];
  let activeOutput: PromptTemplate = markdownOutputs[0];
  let activeStep: string | null = null;
  
  // State for file contents
  let promptContents: Record<string, string> = {};
  let markdownContents: Record<string, string> = {};
  
  // Function to copy text to clipboard
  async function copyToClipboard(text: string, id: string): Promise<void> {
    try {
      await navigator.clipboard.writeText(text);
      const element = document.getElementById(id);
      if (element) {
        element.innerText = 'Copied!';
        setTimeout(() => {
          const el = document.getElementById(id);
          if (el) {
            el.innerText = 'Copy';
          }
        }, 2000);
      }
    } catch (err) {
      console.error('Failed to copy text: ', err);
    }
  }
  
  // Fetch file contents
  onMount(async () => {
    try {
      // Fetch prompt templates
      for (const prompt of promptTemplates) {
        const response = await fetch(prompt.path);
        promptContents[prompt.id] = await response.text();
      }
      
      // Fetch markdown outputs
      for (const output of markdownOutputs) {
        const response = await fetch(output.path);
        markdownContents[output.id] = await response.text();
      }
    } catch (error) {
      console.error('Error loading file contents:', error);
    }

    // Add animation trigger after a small delay
    setTimeout(() => {
      isPageLoaded = true;
    }, 300);
  });

  // Steps for the tutorial
  const steps: Step[] = [
    {
      id: 'step1',
      title: 'Import Raw Data',
      description: 'Start with raw tabular data from Google Sheets',
      link: rawDataLink,
      linkText: 'View Google Sheet'
    },
    {
      id: 'step2',
      title: 'Use ChatGPT',
      description: 'Transform data with intelligent prompts',
      content: promptTemplates,
      contentType: 'prompts'
    },
    {
      id: 'step3',
      title: 'Convert to Markdown',
      description: 'Format data as hierarchical markdown',
      content: markdownOutputs,
      contentType: 'markdown'
    },
    {
      id: 'step4',
      title: 'Import to XMind',
      description: 'Visualize your data as a mind map',
      link: xmindLink,
      linkText: 'Open in XMind'
    },
    {
      id: 'step5',
      title: 'Finalize in SmartArt',
      description: 'Export to PowerPoint for presentations',
      link: smartArtLink,
      linkText: 'Download PPTX'
    }
  ];

  // Add a function to handle image loading errors
  function handleImageError(event: Event): void {
    const target = event.target as HTMLImageElement;
    target.src = 'https://placehold.co/600x400?text=XMind+Preview';
  }

  // Add some visual animation state
  let isPageLoaded = false;
  
  // Add logo URLs with static resources
  const chatGptLogo = "https://upload.wikimedia.org/wikipedia/commons/0/04/ChatGPT_logo.svg";
  const xmindLogo = "/faviconX.png";  // Using the static favicon file
  const openAiLogo = "https://upload.wikimedia.org/wikipedia/commons/4/4d/OpenAI_Logo.svg";
  const pptLogo = "https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/Microsoft_Office_PowerPoint_%282019%E2%80%93present%29.svg/512px-Microsoft_Office_PowerPoint_%282019%E2%80%93present%29.svg.png";
  
  // XMind tutorial image from static folder with reduced size
  const xmindTutorialImage = "/xmind-tutorial.png";
</script>

<svelte:head>
  <title>XMind Smart Converter | Raw Data to SmartArt</title>
  <meta name="description" content="Seamlessly transform your raw data into beautiful mind maps and SmartArt" />
  <link rel="icon" href="/faviconX.png" />
</svelte:head>

<main class="min-h-screen bg-gradient-to-br from-slate-50 via-blue-50 to-indigo-50 py-4 px-3 sm:px-4 font-sans text-slate-700 overflow-x-hidden">
  <div class="max-w-4xl mx-auto">
    <!-- Google Drive Link Banner -->
    <div class="mb-4 bg-white/80 backdrop-blur-md rounded-lg border border-white/50 shadow-md p-3 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}">
      <a href="https://drive.google.com/drive/folders/1yBkI2Wea95dlJ2svK4vAYr_4YONYvG5N?usp=drive_link" 
         target="_blank" 
         rel="noopener noreferrer"
         class="flex items-center justify-between text-slate-700 hover:text-blue-600 transition-colors">
        <div class="flex items-center">
          <svg class="w-5 h-5 mr-2 text-blue-500" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 11l8.71 5.03-3.35 5.81-8.71-5.03 3.35-5.81zM7.69 14.97L3 11.38l4.26-7.38 4.69 2.7-4.26 8.27z"></path>
            <path d="M15.92 22.53l-1.64-2.84 8.69-5.03-1.36-2.43-8.69 5.16-4.69-2.83L20.69 2.47l4.69 2.84-9.46 17.22z"></path>
          </svg>
          <span class="font-medium">Access All Files in Google Drive</span>
        </div>
        <span class="text-sm bg-blue-100 text-blue-700 px-2 py-0.5 rounded-full">Open Folder</span>
      </a>
    </div>
    
    <!-- Header with glass effect (more compact) -->
    <header class="text-center mb-8 relative">
      <div class="absolute inset-0 bg-gradient-to-r from-blue-300/30 to-purple-300/30 rounded-xl blur-xl -z-10 transform -translate-y-4 opacity-70"></div>
      <div class="bg-white/60 backdrop-blur-xl py-5 px-4 rounded-xl shadow-lg border border-white/70 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}">
        <div class="flex justify-center mb-3 space-x-4">
          <img src="/faviconX.png" alt="XMind Logo" class="h-10 w-10 object-contain animate-float" />
          <div class="text-lg font-bold text-transparent bg-clip-text bg-gradient-to-r from-blue-500 to-purple-500 flex items-center">→</div>
          <img src={chatGptLogo} alt="ChatGPT Logo" class="h-9 w-9 object-contain" />
          <div class="text-lg font-bold text-transparent bg-clip-text bg-gradient-to-r from-blue-500 to-purple-500 flex items-center">→</div>
          <img src={pptLogo} alt="PowerPoint Logo" class="h-9 w-9 object-contain" />
        </div>
        <h1 class="text-2xl md:text-3xl font-bold mb-2 tracking-tight text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600">
            Tutorial: Raw Data to XMind to SmartArt
        </h1>
        <p class="text-base text-slate-600 max-w-xl mx-auto">
          Transform tabular data into mind maps
        </p>
      </div>
    </header>

    <!-- Visual Step Cards (More compact) -->
    <section class="mb-10 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}" style="transition-delay: 100ms;">
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-3">
        {#each steps as step, i}
          <div 
            class="bg-white/80 backdrop-blur-md rounded-lg overflow-hidden border border-white/50 hover:border-blue-300/70 hover:bg-white/90 transition-all duration-300 cursor-pointer shadow-md transform hover:-translate-y-1"
            on:click={() => activeStep = activeStep === step.id ? null : step.id}
          >
            <div class="p-3 h-full flex flex-col">
              <div class="flex items-center mb-2">
                <div class="h-6 w-6 rounded-full bg-gradient-to-br from-blue-500 to-purple-600 flex items-center justify-center text-white font-semibold shadow-sm text-xs">
                  {i + 1}
                </div>
                <h3 class="ml-2 text-sm font-semibold text-slate-700">{step.title}</h3>
              </div>
              <p class="text-xs text-slate-600 flex-grow">{step.description}</p>
              
              {#if step.link}
                <div class="mt-2 pt-1 border-t border-slate-200">
                  <a href={step.link} target="_blank" rel="noopener noreferrer" 
                    class="text-xs text-blue-600 hover:text-blue-800 flex items-center">
                    <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
                    </svg>
                    {step.linkText}
                  </a>
                </div>
              {/if}
            </div>
          </div>
        {/each}
      </div>
    </section>

    <!-- Step-by-Step Guide (More compact) -->
    <section class="mb-10 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}" style="transition-delay: 200ms;">
      <h2 class="text-xl font-bold mb-4 text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 inline-flex items-center">
        <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path>
        </svg>
        Steps
      </h2>
      
      <div class="space-y-3">
        {#each steps as step, i}
          <div class="bg-white/80 backdrop-blur-md rounded-lg border border-white/50 overflow-hidden transition-all duration-300 shadow-md {activeStep === step.id ? 'border-blue-400' : ''}">
            <div 
              class="p-3 cursor-pointer font-semibold flex items-center justify-between transition-colors {activeStep === step.id ? 'bg-gradient-to-r from-blue-100 to-purple-100' : 'hover:bg-white/70'}"
              on:click={() => activeStep = activeStep === step.id ? null : step.id}
            >
              <div class="flex items-center">
                <span class="h-6 w-6 rounded-full bg-gradient-to-br from-blue-500 to-purple-600 flex items-center justify-center text-white text-xs mr-2 shadow-sm">
                  {i + 1}
                </span>
                <span class="text-slate-700 text-sm">{step.title}</span>
              </div>
              <svg class="w-4 h-4 text-slate-500 transition-transform duration-300 {activeStep === step.id ? 'rotate-180' : ''}" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
              </svg>
            </div>
            
            {#if activeStep === step.id}
              <div class="p-3 border-t border-slate-200 animate-fadeIn">
                <p class="mb-3 text-slate-600 text-sm">{step.description}</p>
                
                {#if step.link}
                  <a href={step.link} target="_blank" rel="noopener noreferrer" 
                    class="inline-flex items-center px-3 py-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white text-sm rounded-md hover:from-blue-500 hover:to-purple-500 transition-all shadow-md">
                    <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
                    </svg>
                    {step.linkText}
                  </a>
                {/if}
                
                {#if step.contentType === 'prompts'}
                  <div class="mt-4">
                    <div class="flex space-x-1 border-b border-slate-200 mb-3">
                      {#each (step.content || []) as prompt, i (prompt.id)}
                        <button 
                          class={`px-3 py-1 rounded-t-lg text-xs transition-colors ${activePrompt.id === prompt.id ? 'bg-blue-100 text-blue-700' : 'text-slate-500 hover:text-slate-700 hover:bg-white'}`}
                          on:click={() => activePrompt = prompt as PromptTemplate}
                        >
                          {prompt.name}
                        </button>
                      {/each}
                    </div>
                    
                    <div class="relative">
                      <pre class="bg-white/70 p-3 rounded-md overflow-x-auto text-xs text-slate-700 border border-slate-200 shadow-inner max-h-60">{promptContents[activePrompt?.id] || 'Loading...'}</pre>
                      <button 
                        id={`copy-${activePrompt?.id}`}
                        class="absolute top-2 right-2 px-2 py-1 bg-blue-500/80 hover:bg-blue-600/90 text-white text-xs rounded transition-colors"
                        on:click={() => copyToClipboard(promptContents[activePrompt?.id], `copy-${activePrompt?.id}`)}
                      >
                        Copy
                      </button>
                    </div>
                  </div>
                {/if}
                
                {#if step.contentType === 'markdown'}
                  <div class="mt-4">
                    <div class="flex space-x-1 border-b border-slate-200 mb-3">
                      {#each (step.content || []) as output, i (output.id)}
                        <button 
                          class={`px-3 py-1 rounded-t-lg text-xs transition-colors ${activeOutput.id === output.id ? 'bg-blue-100 text-blue-700' : 'text-slate-500 hover:text-slate-700 hover:bg-white'}`}
                          on:click={() => activeOutput = output as PromptTemplate}
                        >
                          {output.name}
                        </button>
                      {/each}
                    </div>
                    
                    <div class="relative">
                      <pre class="bg-white/70 p-3 rounded-md overflow-x-auto text-xs text-slate-700 border border-slate-200 shadow-inner max-h-60"><code>{markdownContents[activeOutput?.id] || 'Loading...'}</code></pre>
                      <button 
                        id={`copy-${activeOutput?.id}`}
                        class="absolute top-2 right-2 px-2 py-1 bg-blue-500/80 hover:bg-blue-600/90 text-white text-xs rounded transition-colors"
                        on:click={() => copyToClipboard(markdownContents[activeOutput?.id], `copy-${activeOutput?.id}`)}
                      >
                        Copy
                      </button>
                    </div>
                  </div>
                {/if}
              </div>
            {/if}
          </div>
        {/each}
      </div>
    </section>

    <!-- XMind Section (More compact) -->
    <section class="mb-10 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}" style="transition-delay: 300ms;">
      <h2 class="text-xl font-bold mb-4 text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 inline-flex items-center">
        <img src="/faviconX.png" alt="XMind Logo" class="h-5 w-5 mr-2" />
        XMind Visualization
      </h2>
      <div class="bg-white/80 backdrop-blur-md rounded-lg border border-white/50 shadow-lg p-4 relative overflow-hidden">
        <div class="absolute top-0 right-0 w-full h-full bg-gradient-to-br from-blue-100/50 to-purple-100/50 -z-10"></div>
        
        <p class="mb-3 text-slate-600 text-sm">
          View your structured data as an interactive mind map in XMind.
        </p>
        <div class="bg-white/70 p-3 rounded-md flex justify-center mb-3 shadow-inner border border-slate-200">
          <img 
            src={xmindTutorialImage} 
            alt="XMind Preview" 
            class="max-w-full h-auto rounded max-h-48 object-contain shadow-sm transform transition-transform hover:scale-[1.02] duration-300"
            on:error={handleImageError}
          />
        </div>
        <div class="flex flex-wrap gap-3 items-center justify-center sm:justify-start">
          <a href={xmindLink} target="_blank" rel="noopener noreferrer" 
            class="inline-flex items-center px-3 py-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white text-sm rounded-md hover:from-blue-500 hover:to-purple-500 transition-all shadow-md">
            <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
            </svg>
            Open in XMind
          </a>
          <a href="https://xmind.app" target="_blank" rel="noopener noreferrer" class="text-blue-600 hover:text-blue-800 transition-colors flex items-center text-sm">
            <img src="/faviconX.png" alt="XMind Logo" class="h-4 w-4 mr-1" />
            Visit XMind
          </a>
        </div>
      </div>
    </section>

    <!-- SmartArt Section (More compact) -->
    <section class="mb-10 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}" style="transition-delay: 400ms;">
      <h2 class="text-xl font-bold mb-4 text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 inline-flex items-center">
        <img src={pptLogo} alt="PowerPoint Logo" class="h-5 w-5 mr-2" />
        SmartArt Conversion
      </h2>
      <div class="bg-white/80 backdrop-blur-md rounded-lg border border-white/50 shadow-lg p-4 relative overflow-hidden">
        <p class="mb-3 text-slate-600 text-sm">
          Download the final SmartArt PPTX file for your presentations.
        </p>
        <a href={smartArtLink} target="_blank" rel="noopener noreferrer" 
          class="inline-flex items-center px-3 py-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white text-sm rounded-md hover:from-blue-500 hover:to-purple-500 transition-all shadow-md">
          <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
          </svg>
          Download SmartArt PPTX
        </a>
      </div>
    </section>

    <!-- Video Tutorial (More compact) -->
    <section class="mb-10 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}" style="transition-delay: 500ms;">
      <h2 class="text-xl font-bold mb-4 text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 inline-flex items-center">
        <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z"></path>
        </svg>
        Video Tutorial
      </h2>
      <div class="bg-white/80 backdrop-blur-md rounded-lg border border-white/50 shadow-lg p-4 relative overflow-hidden">
        <p class="mb-3 text-slate-600 text-sm">
          Watch a step-by-step video tutorial of the entire process.
        </p>
        <div class="aspect-w-16 aspect-h-9 bg-white/70 rounded-md mb-3 shadow-inner border border-slate-200 overflow-hidden">
          <iframe 
            src="https://drive.google.com/file/d/1yicW1DLJY_11eLrmV6b1rLsqF-HkGaau/preview" 
            class="w-full h-48 rounded"
            allowfullscreen
          ></iframe>
        </div>
        <a href={videoLink} target="_blank" rel="noopener noreferrer" 
          class="inline-flex items-center px-3 py-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white text-sm rounded-md hover:from-blue-500 hover:to-purple-500 transition-all shadow-md">
          <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"></path>
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
          </svg>
          Watch Video
        </a>
      </div>
    </section>

    <!-- Footer (More compact) -->
    <footer class="mt-10 pt-4 border-t border-slate-200/70 transition-all duration-700 {isPageLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'}" style="transition-delay: 600ms;">
      <div class="flex flex-wrap justify-center gap-4 mb-4">
        <a href="https://openai.com/chatgpt" target="_blank" rel="noopener noreferrer" 
          class="flex items-center bg-white/50 hover:bg-white/80 transition-colors px-3 py-1 rounded-full border border-white/60 shadow-sm">
          <img src={chatGptLogo} alt="ChatGPT Logo" class="h-4 w-4 mr-1" />
          <span class="text-slate-700 text-xs">ChatGPT</span>
        </a>
        <a href="https://xmind.app" target="_blank" rel="noopener noreferrer" 
          class="flex items-center bg-white/50 hover:bg-white/80 transition-colors px-3 py-1 rounded-full border border-white/60 shadow-sm">
          <img src="/faviconX.png" alt="XMind Logo" class="h-4 w-4 mr-1" />
          <span class="text-slate-700 text-xs">XMind</span>
        </a>
        <a href="https://www.microsoft.com/powerpoint" target="_blank" rel="noopener noreferrer" 
          class="flex items-center bg-white/50 hover:bg-white/80 transition-colors px-3 py-1 rounded-full border border-white/60 shadow-sm">
          <img src={pptLogo} alt="PowerPoint Logo" class="h-4 w-4 mr-1" />
          <span class="text-slate-700 text-xs">PowerPoint</span>
        </a>
      </div>
      <div class="text-center text-slate-500 text-xs pb-2">
        <p>© {new Date().getFullYear()} </p>
      </div>
    </footer>
  </div>
</main>

<style>
  :global(body) {
    font-family: 'Poppins', sans-serif;
    overflow-x: hidden;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  .animate-fadeIn {
    animation: fadeIn 0.3s ease-out forwards;
  }
</style>
