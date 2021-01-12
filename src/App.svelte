<script>
	import { randomUniform, randomInt } from "d3-random";
	import { onMount } from "svelte";

	let w;
	let h;

	//these are the bounds of how many seconds it will take for spongebob to appear after the button is clicked
	const intervalBounds = {
		min: 1000,
		max: 7000,
	};

	const spongeBobWidth = 200;
	const spongeBobHeight = 206;

	const getRandomPosition = () => {
		const x = randomInt(0 + spongeBobWidth, w - spongeBobWidth)();
		const y = randomInt(0 + spongeBobHeight, h - spongeBobHeight)();
		return { x, y };
	};

	let spongeBobVisible = false;

	let randomPosition = getRandomPosition();

	let timer;

	let clicked = new Date();
	let appeared = new Date();

	let difference = appeared - clicked;

	const roundToHundreths = (n) => Math.round(n * 100) / 100;

	$: differenceSeconds = roundToHundreths(difference / 1000);

	const startTimer = (interval) => {
		timer = setTimeout(() => {
			spongeBobVisible = true;
			appeared = new Date();
		}, interval);
	};

	const handleClick = () => {
		clicked = new Date();
		difference = clicked - appeared;
		clearTimeout(timer);
		spongeBobVisible = false;
		randomPosition = getRandomPosition();
		const newInterval = randomUniform(
			intervalBounds.min,
			intervalBounds.max
		)();
		startTimer(newInterval);
	};

	onMount(() => {
		const startingInterval = randomUniform(
			intervalBounds.min,
			intervalBounds.max
		)();
		randomPosition = getRandomPosition();
		startTimer(startingInterval);
	});
</script>

<style>
	.app {
		align-items: center;
		background-color: darkgray;
		display: flex;
		flex-direction: column;
		position: relative;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.spongebob {
		display: none;
		pointer-events: none;
		position: absolute;
	}

	button {
		border: none;
		background-color: lightblue;
		box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19),
			0 6px 6px rgba(0, 0, 0, 0.23);
		font-size: 16px;
		line-height: 20px;
		margin-bottom: 20px;
		width: 200px;
	}

	.visible {
		display: block;
	}

	.info {
	}
</style>

<div bind:clientWidth={w} bind:clientHeight={h} class="app">
	<img
		class="spongebob"
		class:visible={spongeBobVisible}
		alt="spongebob"
		src="./spongebob.png"
		style={`left: ${randomPosition.x}px; 
		top: ${randomPosition.y}px; 
		width:${spongeBobWidth}px;
		height:${spongeBobHeight}px;`} />
	<button on:click={handleClick}>
		Click this button when you see Spongebob.
	</button>
	<div class="info">
		The time between click and appearance is
		{differenceSeconds}
		seconds.
	</div>
</div>

<!-- 

// This looks awesome!
// I don't understand any of import {  } from "
// Very nice!
// randomUniform() generates a random number between x (inclusive) and y (exclusive): randomUniform(x, y)()

going ot the bathroom ok
hi, still there?
yeah
It should be @ the center of the screen always 
You did it!
haha

FUCCK!!!

oooooooh fucckck ok
it's not super important though - top left is fine too
it's testing reaction times based o
https://svelte.dev/tutorial/basics this tutorial is pretty good and it is very
easy to learn angular and vue are evil, react is pretty good, but svelte is even
easier woot hello! how are you good. welcome to hellsinki thanks! yes. yeah,
i'll start a server and share it with you. haha :D clientHeight HI! Great! Super
glad to be heere It looks svelty The Finland capital! SO we just type stuff and
it makes the app work,r ight? !! Super into sharing...servers Ok in shared
servers you will see it just go to localhost:8080 in your browser i guess yeah
ok, so do you wanna do it or you want me to or how do you want to do it ok do
you wanna go in the audio call or do you want to just type and watch ok I see
it! blank page Show me! Voyeur mode. Type and watch wow! i see spongebob

hahah nice
undefined undefined

it's supposed to bind the width and height of .app to those values
oh so it's working - 100vh/vw is full screen right? yes
Cool, how do we make them appear after a random amt of time?
what do you want the minimum and maxium time to be after the click
3 and 7
oh shit - busting out the curly braces! haha
i need that clientWidth and clientHeight shit to work
should i just abandon it for now
idk why its not working. give me one minute if i can't figure it out ill abandon it omg figured it out
!!
It works!!!
cool. now how big do you want this spongebob picture to be (pixels)
12 inches
haha 200 x 200
i think the height is calculated automatically from
 the aspect ratio
 oh cool
 nice, it worked

 ok so now we are going to generate a random position for spongebob, is that what you want?
 
-->
