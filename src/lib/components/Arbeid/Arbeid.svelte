<script>
	import Heading from '../Heading.svelte';
	import Prosjekt from './Prosjekt.svelte';
	import Loading from '../Loading.svelte';

	const prosjekter = [
		{
			type: 'Bedrift',
			client: 'Omsorgskollektivet',
			href: 'https://www.omsorgskollektivet.no/',
			texture: ['./ok-full.webp', './ok-full2.webp', './ok-full3.webp']
		},
		{
			type: 'Organisasjon',
			client: 'Sound of Happiness',
			href: null,
			texture: ['./soh-full.webp', './soh-full2.webp', './soh-full3.webp']
		},
		{
			type: 'Restaurant',
			client: 'Le Monde Tapas',
			href: 'https://lemondetapas.no/',
			texture: ['./lmt-full.webp', './lmt-full2.webp', './lmt-full3.webp']
		},
		{
			type: 'Eksamen',
			client: 'Bid-B',
			href: 'https://ad-exam2.netlify.app/',
			texture: ['./bb-full.webp', './bb-full2.webp', './bb-full3.webp']
		},
		{
			type: 'Prosjekt',
			client: 'TILFELDIG',
			href: 'https://tilfeldig.netlify.app/',
			texture: ['./tf-full.webp', './tf-full2.webp', './tf-full3.webp']
		}
	];

	import * as THREE from 'three';
	import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

	import { onMount } from 'svelte';

	let mainPlaneMaterial;
	let secondaryPlaneMaterial;
	let tertiaryPlaneMaterial;
	let transitionStartTime;

	let textures = {};

	let isLoading = true;

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
		renderer.setPixelRatio(window.devicePixelRatio);
		renderer.setSize(window.innerWidth, window.innerHeight);
		renderer.render(scene, camera);

		camera.position.z = 1.5;
		if (isMobile) camera.position.z = 2.5;

		const controls = new OrbitControls(camera, renderer.domElement);
		controls.enableDamping = true;
		controls.dampingFactor = 0.02;

		const loadingManager = new THREE.LoadingManager();
		const textureLoader = new THREE.TextureLoader(loadingManager);

		// Preload all the textures
		prosjekter.forEach((prosjekt) => {
			prosjekt.texture.forEach((texturePath) => {
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

		const createMaterial = (initialTexture) => {
			const uniforms = {
				texture1: { value: new THREE.TextureLoader().load(initialTexture) },
				texture2: { value: null },
				blend: { value: 0 }
			};

			return new THREE.ShaderMaterial({
				uniforms,
				fragmentShader,
				vertexShader
			});
		};

		mainPlaneMaterial = createMaterial('./soh-full.webp');
		secondaryPlaneMaterial = createMaterial('./soh-full2.webp');
		tertiaryPlaneMaterial = createMaterial('./soh-full3.webp');

		const mainPlane = () => {
			const geometry = new THREE.PlaneGeometry(1.6, 1);
			const plane = new THREE.Mesh(geometry, mainPlaneMaterial);
			scene.add(plane);
		};

		mainPlane();

		const secondaryPlane = () => {
			const geometry = new THREE.PlaneGeometry(1.6, 1);
			const plane = new THREE.Mesh(geometry, secondaryPlaneMaterial);

			plane.position.x = 0.8;
			plane.position.z = 0.2;
			plane.position.y = -0.4;
			plane.scale.set(0.6, 0.6, 0.6);

			if (isMobile) {
				plane.position.x = 0;
				plane.position.y = -0.7;
				plane.position.z = 0.4;
				plane.scale.set(0.7, 0.7, 0.7);
			}

			scene.add(plane);
		};

		secondaryPlane();<script>
  // other imports and code...

  onMount(() => {
    // other code...

    const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);

    const mainPlane = () => {
      const geometry = new THREE.PlaneGeometry(1.6, 1);
      const plane = new THREE.Mesh(geometry, mainPlaneMaterial);
      if (isMobile) {
        // Adjust the position for mobile
        plane.position.x = ...;
        plane.position.y = ...;
        plane.position.z = ...;
      }
      scene.add(plane);
    };

    mainPlane();

    const secondaryPlane = () => {
      const geometry = new THREE.PlaneGeometry(1.6, 1);
      const plane = new THREE.Mesh(geometry, secondaryPlaneMaterial);
      if (isMobile) {
        // Adjust the position for mobile
        plane.position.x = ...;
        plane.position.y = ...;
        plane.position.z = ...;
      }
      scene.add(plane);
    };

    secondaryPlane();

    const tertiaryPlane = () => {
      const geometry = new THREE.PlaneGeometry(0.9, 1.8);
      const plane = new THREE.Mesh(geometry, tertiaryPlaneMaterial);
      if (isMobile) {
        // Adjust the position for mobile
        plane.position.x = ...;
        plane.position.y = ...;
        plane.position.z = ...;
      }
      scene.add(plane);
    };

    tertiaryPlane();

    // other code...
  });

  // other code...
</script>

<!-- the rest of your component... -->

		const tertiaryPlane = () => {
			const geometry = new THREE.PlaneGeometry(0.9, 1.8);
			const plane = new THREE.Mesh(geometry, tertiaryPlaneMaterial);

			plane.position.x = -0.8;
			plane.position.z = 0.3;
			plane.position.y = 0.1;
			plane.scale.set(0.4, 0.4, 0.4);

			if (isMobile) {
				plane.position.x = -0.2;
				plane.position.y = 0.8;
				plane.position.z = 0.5;
				plane.scale.set(0.5, 0.5, 0.5);
			}

			scene.add(plane);
		};

		tertiaryPlane();

		const light = new THREE.DirectionalLight(0xffffff, 1);
		light.position.set(0, 0, 1);

		const ambientLight = new THREE.AmbientLight(0xffffff, 1);

		scene.add(light, ambientLight);

		let target = new THREE.Vector3(); // The target position for the camera
		let mouse = new THREE.Vector2(); // The current mouse position

		window.addEventListener('mousemove', (event) => {
			// Calculate the target camera position based on the mouse position
			target.x = (event.clientX / window.innerWidth) * 2 - 1;
			target.y = -(event.clientY / window.innerHeight) * 2 + 1;
		});

		const animate = () => {
			requestAnimationFrame(animate);

			// Get all the planes
			const [mainPlane, secondaryPlane, tertiaryPlane] = scene.children.filter(
				(child) => child.type === 'Mesh'
			);

			// Slightly move the planes randomly
			mainPlane.position.x += Math.sin(Date.now() * 0.001) * 0.0002;
			mainPlane.position.y += Math.cos(Date.now() * 0.001) * 0.0002;

			secondaryPlane.position.x += -Math.sin(Date.now() * 0.001) * 0.0001;
			secondaryPlane.position.y += Math.cos(Date.now() * 0.001) * 0.0001;

			tertiaryPlane.position.x += Math.sin(Date.now() * 0.001) * 0.0001;
			tertiaryPlane.position.y += -Math.cos(Date.now() * 0.001) * 0.0001;

			// Update the camera position based on the target position
			mouse.x += (target.x - mouse.x) * 0.05;
			mouse.y += (target.y - mouse.y) * 0.05;

			camera.position.x = -mouse.x * 0.2;
			camera.position.y = -mouse.y * 0.2;
			controls.update();

			// Update the blend uniform over time to transition between the textures
			[mainPlaneMaterial, secondaryPlaneMaterial, tertiaryPlaneMaterial].forEach((material) => {
				if (material.uniforms.texture2.value && transitionStartTime) {
					const elapsedTime = Date.now() - transitionStartTime;
					material.uniforms.blend.value = Math.min(elapsedTime / 1000, 1);
				}
			});

			renderer.render(scene, camera);
		};

		animate();

		return () => {
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
			{#each prosjekter as prosjekt}
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
		transition: opacity 300ms ease;
		pointer-events: none;
		background-color: #525250ed;
	}

	.show-canvas {
		opacity: 1;
		z-index: 1;
	}
</style>
