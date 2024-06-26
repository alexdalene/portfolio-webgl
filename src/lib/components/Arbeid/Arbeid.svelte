<script>
	import Heading from '../Heading.svelte';
	import Prosjekt from './Prosjekt.svelte';
	import Loading from '../Loading.svelte';

	import * as THREE from 'three';
	import { onMount } from 'svelte';

	const projects = [
		{
			type: 'React',
			client: 'Holidaze',
			href: 'https://project-exam-2-orcin.vercel.app/',
			texture: ['./hz-full.webp', './hz-full2.webp', './hz-full3.webp']
		},
		{
			type: 'CMS',
			client: 'Sound of Happiness',
			href: null,
			texture: ['./soh-full.webp', './soh-full2.webp', './soh-full3.webp']
		},
		{
			type: 'JavaScript',
			client: 'Bid-B',
			href: 'https://ad-exam2.netlify.app/',
			texture: ['./bb-full.webp', './bb-full2.webp', './bb-full3.webp']
		},
		{
			type: 'CMS',
			client: 'Omsorgskollektivet',
			href: 'https://www.omsorgskollektivet.no/',
			texture: ['./ok-full.webp', './ok-full2.webp', './ok-full3.webp']
		},
		{
			type: 'Svelte',
			client: 'TILFELDIG',
			href: 'https://tilfeldig.netlify.app/',
			texture: ['./tf-full.webp', './tf-full2.webp', './tf-full3.webp']
		},
		{
			type: 'CMS',
			client: 'Le Monde Tapas',
			href: 'https://lemondetapas.no/',
			texture: ['./lmt-full.webp', './lmt-full2.webp', './lmt-full3.webp']
		},
		{
			type: 'CMS',
			client: 'Guttas Campus',
			href: 'https://guttascampus.no/',
			texture: ['./gc-full.webp', './gc-full2.webp', './gc-full3.webp']
		}
	];

	let mainPlaneMaterial;
	let secondaryPlaneMaterial;
	let tertiaryPlaneMaterial;
	let transitionStartTime;

	let textures = {};

	let isLoading = true;
	let isMouseMoving = false;
	let mouseMovement = new THREE.Vector2(); // The current mouse movement
	let prevMousePosition = new THREE.Vector2(); // The previous mouse position

	onMount(() => {
		const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
			navigator.userAgent
		);

		const scene = new THREE.Scene();
		const camera = new THREE.PerspectiveCamera(
			75,
			window.innerWidth / window.innerHeight,
			0.1,
			1000
		);

		const renderer = new THREE.WebGLRenderer({
			canvas: canvas,
			antialias: true,
			alpha: true
		});
		renderer.setSize(window.innerWidth, window.innerHeight);
		renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
		renderer.render(scene, camera);

		camera.position.z = 1.5;
		if (isMobile) camera.position.z = 2.5;

		const group = new THREE.Group();

		const loadingManager = new THREE.LoadingManager();
		const textureLoader = new THREE.TextureLoader(loadingManager);

		// Preload all the textures
		projects.forEach((project) => {
			project.texture.forEach((texturePath) => {
				textures[texturePath] = textureLoader.load(texturePath);
			});
		});

		loadingManager.onLoad = () => {
			isLoading = false;
		};

		const fragmentShader = `
		uniform sampler2D texture1;
		uniform sampler2D texture2;
		uniform float blend;

		varying vec2 vUv;

		void main() {
			vec4 color1 = texture2D(texture1, vUv);
			vec4 color2 = texture2D(texture2, vUv);
			gl_FragColor = mix(color1, color2, blend);
		}
		`;

		const vertexShader = `
		varying vec2 vUv;

		void main() {
			vUv = uv;
			gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
		}
		`;

		const createMaterial = () => {
			const uniforms = {
				texture1: { value: new THREE.TextureLoader() },
				texture2: { value: null },
				blend: { value: 0 }
			};

			return new THREE.ShaderMaterial({
				uniforms,
				fragmentShader,
				vertexShader
			});
		};

		mainPlaneMaterial = createMaterial();
		secondaryPlaneMaterial = createMaterial();
		tertiaryPlaneMaterial = createMaterial();

		// Create variables to store the planes
		let mainPlane, secondaryPlane, tertiaryPlane;

		const createPlane = (material) => {
			const geometry = new THREE.PlaneGeometry(1.6, 1);
			const plane = new THREE.Mesh(geometry, material);
			return plane;
		};

		mainPlane = createPlane(mainPlaneMaterial);
		secondaryPlane = createPlane(secondaryPlaneMaterial);
		tertiaryPlane = createPlane(tertiaryPlaneMaterial);

		// Scale the planes
		mainPlane.scale.set(1.2, 1.2, 1.2);
		secondaryPlane.scale.set(0.4, 0.4, 0.4);
		tertiaryPlane.scale.set(0.5, 0.5, 0.5);

		// Position the planes
		secondaryPlane.position.x = 0.7;
		secondaryPlane.position.z = 0.5;
		secondaryPlane.position.y = -0.4;

		tertiaryPlane.position.x = -0.7;
		tertiaryPlane.position.z = 0.4;
		tertiaryPlane.position.y = 0.3;

		if (isMobile) {
			mainPlane.scale.set(1, 1, 1);

			secondaryPlane.position.x = -0.1;
			secondaryPlane.position.y = -0.8;
			secondaryPlane.scale.set(0.7, 0.7, 0.7);

			tertiaryPlane.position.x = 0.1;
			tertiaryPlane.position.y = 0.8;
			tertiaryPlane.scale.set(0.8, 0.8, 0.8);
		}

		// Add the planes to the group
		group.add(mainPlane);
		group.add(secondaryPlane);
		group.add(tertiaryPlane);

		scene.add(group);

		/**
		 * Mouse
		 */
		let target = new THREE.Vector3(); // The target position for the camera
		let mouse = new THREE.Vector2(); // The current mouse position

		window.addEventListener('mousemove', (event) => {
			// Calculate the target camera position based on the mouse position
			target.x = (event.clientX / window.innerWidth) * 2 - 1;
			target.y = -(event.clientY / window.innerHeight) * 2 + 1;

			// Calculate the current mouse position
			let mousePosition = new THREE.Vector2();
			mousePosition.x = target.x;

			// Calculate the mouse movement
			mouseMovement.subVectors(mousePosition, prevMousePosition);

			// Store the current mouse position for the next frame
			prevMousePosition.copy(mousePosition);

			isMouseMoving = true;
		});

		/**
		 * Resize
		 */
		window.addEventListener('resize', () => {
			// Update camera
			camera.aspect = window.innerWidth / window.innerHeight;
			camera.updateProjectionMatrix();

			// Update renderer
			renderer.setSize(window.innerWidth, window.innerHeight);
			renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
		});

		/**
		 * Animate
		 */
		const clock = new THREE.Clock();

		const tick = () => {
			const elapsedTime = clock.getElapsedTime();

			// // Slightly move the planes randomly
			mainPlane.position.x += Math.sin(Date.now() * 0.001) * 0.0002;
			mainPlane.position.y += Math.cos(Date.now() * 0.001) * 0.0002;

			secondaryPlane.position.x += -Math.sin(Date.now() * 0.001) * 0.0002;
			secondaryPlane.position.y += Math.cos(Date.now() * 0.001) * 0.0002;

			tertiaryPlane.position.x += Math.sin(Date.now() * 0.001) * 0.0003;
			tertiaryPlane.position.y += -Math.cos(Date.now() * 0.001) * 0.0003;

			// Update the camera position based on the target position
			mouse.x += (target.x - mouse.x) * 0.03;
			mouse.y += (target.y - mouse.y) * 0.03;

			if (!isMobile) {
				group.position.x = mouse.x * 0.4;
				group.position.y = mouse.y * 0.1;
				group.rotation.y = mouse.x * 0.2;

				// Update the group rotation based on the mouse movement
				group.rotation.z += mouseMovement.x * 0.05;
			}

			// // If the mouse is not moving, gradually return the rotation to zero
			if (!isMouseMoving) {
				group.rotation.z *= 0.95;

				// If the rotation is very small, set it exactly to zero
				if (Math.abs(group.rotation.z) < 0.001) {
					group.rotation.z = 0;
				}
			}

			camera.position.z = 1.7;

			if (window.innerWidth < 1400) camera.position.z = 2;

			if (window.innerWidth < 900) camera.position.z = 2.5;

			if (window.innerWidth < 600) camera.position.z = 3;

			// Update the blend uniform over time to transition between the textures
			[mainPlaneMaterial, secondaryPlaneMaterial, tertiaryPlaneMaterial].forEach((material) => {
				if (material.uniforms.texture2.value && transitionStartTime) {
					const elapsedTime = Date.now() - transitionStartTime;
					material.uniforms.blend.value = Math.min(elapsedTime / 600, 1);
				}
			});

			renderer.render(scene, camera);

			// Set isMouseMoving to false for the next frame
			isMouseMoving = false;

			window.requestAnimationFrame(tick);
		};

		tick();

		return () => {
			// Remove the resize event listener when the component is unmounted
			window.removeEventListener('resize', () => {
				renderer.setSize(window.innerWidth, window.innerHeight);
				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();
			});

			renderer.dispose();
		};
	});

	const changeTexture = (textures) => {
		[mainPlaneMaterial, secondaryPlaneMaterial, tertiaryPlaneMaterial].forEach(
			(material, index) => {
				material.uniforms.texture1.value =
					material.uniforms.texture2.value || material.uniforms.texture1.value;
				material.uniforms.texture2.value = new THREE.TextureLoader().load(textures[index]);
				material.uniforms.blend.value = 0;
			}
		);

		transitionStartTime = Date.now();
	};

	let canvas;
	let isHovered = false;
</script>

<canvas id="canvas" bind:this={canvas} class:show-canvas={isHovered}></canvas>

{#if isLoading}
	<Loading />
{:else}
	<section id="arbeid">
		<Heading title="Fremhevet arbeid" />

		<div
			class:hide-projects={isHovered}
			on:mouseenter={() => (isHovered = true)}
			on:mouseleave={() => (isHovered = false)}
			role="list"
		>
			{#each projects as prosjekt}
				<Prosjekt {...prosjekt} {changeTexture} />
			{/each}
		</div>
	</section>
{/if}

<style>
	canvas {
		position: fixed;
		top: 0;
		left: 0;
		z-index: -1;
		opacity: 0;
		width: 100%;
		height: 100%;
		transition: opacity 600ms ease-in-out;
		pointer-events: none;
		background-color: rgba(0, 0, 0, 0.6);
		backdrop-filter: blur(4px);
	}

	.show-canvas {
		opacity: 1;
		z-index: 1;
	}
</style>
