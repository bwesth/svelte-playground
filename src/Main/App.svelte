<script>
import Component from "../Basics/Component.svelte";
import John from "../Basics/John.svelte";
import Introduction from "../Admin_stuff/Introduction.svelte";
import Ideas from '../Admin_stuff/Ideas.svelte'
import StartingOut from "../Basics/StartingOut.svelte";
import Reactivity from "../Basics/Reactivity.svelte";
import Props from "../Basics/Props.svelte";
import Logic from "../Basics/Logic.svelte";
import Events from "../Basics/Events.svelte";


function getCookie() {
	return document.cookie
	
}

function setCookie(username) {
	document.cookie = username
	location.reload()
}

const clearCookie = () => {
	document.cookie = ""
	location.reload()
}

const todo = [
	"First Meeting with Mircea",
	"If all we figure out in the first meeting is: we know what we're making, we're good!",
	"Come up with a meeting agenda",
	"PLAN A: An extension that redirects you to our microlearning website, then back to the extension",
	"Come up with list of ideas / Brainstorm app ideas",
	"Read both papers provided by Mircea",
	"Introduction to Svelte Scrimba (John)",
	"Google Extensions vid (John)",
	"Svelte Videos (John)",
	"Begin to familiarize ourselves with Svelte (Take notes while learning)",
	"Compile the notes somewhere!",
	"(Microlearning)",
	"Take a look at Codecademy’s Quizzes?",
	"Take a look at SoloLearn?",
	"Take a look at Duolingo?",
	"Look for other microlearning apps?",
	"Look up some stuff on microlearning?",
	"Start making a website?",
]

const quotes = [
	{source: "Aiki paper", text: "Based on these different outcomes, future implementations of the extension may consider different, specialized versions which cater to different types of users. Currently, Aiki is designed as an ultra-simple one-fits-all solution, put specializations are worth exploring: for instance design with a focus on promoting awareness and/or reflection a focus on distracting from procrastination behavior, or a focus on maximizing for engagement with the learning tasks."},
	{source: "Aiki paper", text: "When inquiring about this further in this and other participants’ post-study interviews, we discussed a design goal of designing the extension / learning environment to provide positive feedback in order to create positive associations with the microlearning tasks."},
	{source: "Aiki paper", text: "Future designs of similar extensions might consider implementing modes, such as a focus-mode and a leisure-mode (either automatically detected or manually controlled), where specific websites are not intercepted."},
	{source: "Aiki paper", text: "One way to mitigate this is to explore a design where the microlearning opportunity appears as a window-overlay on top of the time-wasting site."},
	{source: "Aiki paper", text: "This suggests that task-based interceptions may make more sense to some users."},
	{source: "Zeeguu RP", text:'“(...) when people reflexively turn to a device—increasingly a smartphone—to act on a need to learn something, do something, discover something, watch something, or buy something.” (Ramaswamy, 2015).'}
]

let name = getCookie()
const home = () => ({page: Introduction, props: {name: name, clearCookie: clearCookie}})

let options = [
	{name: "Component", page: Component},
	{name: "Ideas", page: Ideas},
	{name: "Starting Out", page: StartingOut},
	{name: "Reactivity", page: Reactivity},
	{name: "Props", page: Props},
	{name: "Events", page: Events},
	{name: "Logic", page: Logic}
],
selected = home()

</script>


<div class="sized">
{#if getCookie() === (undefined || "")}
<div class="intro">
	<p>I'm sorry, do I know you?</p>
	<input type="text" bind:value={name}>
	<button on:click={() => setCookie(name)} >Lets go</button>
</div>
	{:else}
<div class="main">
	<button on:click={() => {selected = home()}}>Home</button>
	{#each options as option}
		<button on:click={() => {selected = option}} >{option.name}</button>
	{/each}

<svelte:component this={selected.page} {...selected.props}/>
</div>
{/if}
</div>


<style>
	.sized {
		height: 100%;
		widows: 100%;
	}

	.intro {
		display: flex;
		flex-direction: column;
		height: 100%;
		widows: 100%;
		align-items: center;
		justify-content: center;
	}

	.intro input, button {
		justify-self: center;
		height: 10%;
		width: 20%;
		text-align: center;
	}
	
</style>


