<script>
	import { onMount } from 'svelte';

	import * as THREE from 'three';
	import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

	export let type;
	export let client;
	export let href;

	let canvas;
	let renderer;
	let scene;
	let camera;
	let mesh1;
	let mesh2;
	let controls;

	onMount(() => {
		// Select all articles
		const articles = document.querySelectorAll('.prosjekt');

		// Loop through all articles
		articles.forEach((article) => {
			// Add event listener for mouseover
			article.addEventListener('mouseover', () => {
				article.style.color = 'var(--color-background)';
				article.style.borderColor = 'var(--color-background)';
				// On mouseover, add 'faded' class to all articles except the one being hovered
				articles.forEach((otherArticle) => {
					if (otherArticle !== article) {
						otherArticle.style.opacity = 0;
					}
				});
			});

			// Add event listener for mouseout
			article.addEventListener('mouseout', () => {
				article.style.color = 'var(--color-text)';
				article.style.borderColor = 'var(--color-text)';
				// On mouseout, remove 'faded' class from all articles
				articles.forEach((otherArticle) => {
					otherArticle.style.opacity = 1;
				});
			});
		});

		// Select all .prosjekt elements
		const projekts = document.querySelectorAll('.prosjekt');

		// Loop through all .prosjekt elements
		projekts.forEach((prosjekt) => {
			// Add event listener for mousemove
			prosjekt.addEventListener('mousemove', (event) => {
				// Calculate the normalized position of the cursor
				const x = (event.clientX / window.innerWidth) * 2 - 1;
				const y = -(event.clientY / window.innerHeight) * 2 + 1;

				// Update the position of the camera
				camera.position.x = -x * 0.2;
				camera.position.y = -y * 0.2;
				controls.update();
			});
		});

		// Create a Three.js scene
		scene = new THREE.Scene();

		// Create a camera
		camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
		camera.position.z = 1.5;

		// Create a renderer and add it to the canvas
		renderer = new THREE.WebGLRenderer({ canvas: canvas, alpha: true, antialias: true });
		renderer.setPixelRatio(window.devicePixelRatio);
		renderer.setSize(window.innerWidth, window.innerHeight);

		// Load a texture
		const loader = new THREE.TextureLoader();

		// Define the texture URLs for different projects
		const textureFull = {
			'Sound of Happiness': '/favicon.png',
			Omsorgskollektivet: '/ok-full.png',
			'Le Monde Tapas': '/favicon.png',
			'Blekksprut Tattoo': '/favicon.png'
		};

		// Load a texture based on the project type or client
		const textureUrl = textureFull[client];

		// Create a mesh with a box geometry and basic material
		const geometry = new THREE.PlaneGeometry(1.5, 1);
		const texture1 = loader.load(textureUrl);
		const material = new THREE.MeshStandardMaterial({ color: 0xffffff, map: texture1 });
		mesh1 = new THREE.Mesh(geometry, material);

		// Add the mesh to the scene
		scene.add(mesh1);

		const textureMobile = {
			'Sound of Happiness': '/favicon.png',
			Omsorgskollektivet: '/ok-mobile.png',
			'Le Monde Tapas': '/favicon.png',
			'Blekksprut Tattoo': '/favicon.png'
		};

		const textureUrl2 = textureMobile[client];

		const geometry2 = new THREE.PlaneGeometry(0.4, 0.75);
		const texture2 = loader.load(textureUrl2);
		const material2 = new THREE.MeshStandardMaterial({ color: 0xffffff, map: texture2 });
		mesh2 = new THREE.Mesh(geometry2, material2);
		mesh2.position.z = 0.1;
		mesh2.position.x = 0.7;
		mesh2.position.y = -0.2;

		// Add the mesh to the scene
		scene.add(mesh2);

		// Add point light
		const light = new THREE.PointLight(0xffffff, 2, 100);
		light.position.set(0, 0, 1);
		scene.add(light);

		// Add ambient light
		const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
		scene.add(ambientLight);

		// Create a new orbit controls
		controls = new OrbitControls(camera, renderer.domElement);

		// Start the animation loop
		animate();

		return () => {
			// Clean up Three.js resources
			mesh1.geometry.dispose();
			mesh1.material.dispose();
			renderer.dispose();
		};
	});

	function animate() {
		requestAnimationFrame(animate);

		// Randomly move the mesh slightly
		mesh1.position.x = Math.sin(Date.now() * 0.001) * 0.005;
		mesh1.position.y = Math.cos(Date.now() * 0.001) * 0.005;

		// Randomly move the mesh slightly from original position
		mesh2.position.x = -Math.sin(Date.now() * 0.001) * 0.005 + 0.7;
		mesh2.position.y = -Math.cos(Date.now() * 0.001) * 0.005 - 0.2;

		// Update the orbit controls
		controls.update();

		// Render the scene
		renderer.render(scene, camera);
	}
</script>

<canvas bind:this={canvas}></canvas>

<article>
	<div
		class="prosjekt"
		on:mouseover={() => ((canvas.style.opacity = 1), (canvas.style.zIndex = 2))}
		on:mouseout={() => ((canvas.style.opacity = 0), (canvas.style.zIndex = -1))}
		on:focus={() => ((canvas.style.opacity = 1), (canvas.style.zIndex = 2))}
		on:blur={() => ((canvas.style.opacity = 0), (canvas.style.zIndex = -1))}
		role="button"
		tabindex="0"
	>
		<p>{type}</p>
		<h3>{client}</h3>

		<a {href} target="_blank">
			<span class="link">[ LIVE ]</span>
			<svg
				width="16"
				height="16"
				viewBox="0 0 16 16"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
				aria-hidden="true"
			>
				<path
					d="M4.05001 12L3.20001 11.15L9.95001 4.4H4.00001V3.2H12V11.2H10.8V5.25L4.05001 12Z"
					fill="currentColor"
				/>
			</svg>
		</a>
	</div>
</article>

<style>
	canvas {
		background-color: #7c7d7a97;
		position: fixed;
		top: 0;
		left: 0;
		z-index: -1;
		opacity: 0;
	}

	.prosjekt {
		display: grid;
		grid-template-columns: repeat(12, 1fr);
		z-index: 2;
		position: relative;
		transition: all 400ms ease-in-out;

		width: 100%;
		padding-block: var(--spacing-tight);

		border-top: 1px solid var(--color-text);

		& p {
			grid-column: 1 / span 2;
		}

		& h3 {
			grid-column: 4 / span 4;
		}

		& a {
			grid-column: 12 / span 2;
			width: min-content;
			white-space: nowrap;
			display: flex;
			align-items: center;
			gap: var(--spacing-compact);
		}
	}
</style>
