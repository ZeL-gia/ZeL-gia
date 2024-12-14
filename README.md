body {
	margin: 0;
	background: radial-gradient(circle, #020111, #000000);
	overflow: hidden;
	height: 100vh;
	cursor: pointer;
	font-family: "Arial", sans-serif;
	color: white;
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}

/* Add large instruction text */
.instructions {
	font-size: 2rem;
	font-weight: bold;
	z-index: 10;
	color: #ff9671;
	text-shadow: 1px -1px 7px rgb(142 142 142 / 80%);
}

.projectile {
	position: absolute;
	width: 12px;
	height: 12px;
	background: white;
	border-radius: 50%;
	box-shadow: 0 0 20px rgba(255, 255, 255, 0.8),
		0 0 30px rgba(255, 255, 255, 0.6), 0 0 40px rgba(255, 255, 255, 0.4);
}

.particule {
	position: absolute;
	font-size: 2rem;
	font-family: "Cursive", serif;
	font-weight: bold;
	color: white;
	transform: scale(0);
	opacity: 0;
}

.sparkle {
	position: absolute;
	width: 6px;
	height: 6px;
	border-radius: 50%;
	background: white;
	transform: scale(0);
	opacity: 0;
 play = 'none';

	if (!isSparkle) {
			el.textContent = getRandomLetter();
			el.style.color = colors[Math.floor(Math.random() * colors.length)];
	} else {
			el.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
	}

	el.style.left = `${x}px`;
	el.style.top = `${y}px`;
	document.body.appendChild(el);

	animateParticle(el, isSparkle);
}

// Animate a particle
function animateParticle(el, isSparkle) {
	const angle = Math.random() * Math.PI * 2; // Random direction
	const distance = anime.random(100, 200); // Increased distance for more dramatic spread
	const duration = anime.random(1200, 2000); // Longer duration for the dramatic effect
	const fallDistance = anime.random(20, 80); // Larger fall effect for realism
	const scale = isSparkle ? Math.random() * 0.5 + 0.5 : Math.random() * 1 + 0.5;

	anime
			.timeline({
					targets: el,
					easing: "easeOutCubic",
					duration: duration,
					complete: () => el.remove() // Remove element after animation
			})
			.add({
					translateX: Math.cos(angle) * distance,
					translateY: Math.sin(angle) * distance,
					scale: [0, scale],
					opacity: [1, 0.9]
			})
			.add({
					translateY: `+=${fallDistance}px`, // Larger gravity effect
					opacity: [0.9, 0],
					easing: "easeInCubic",
					duration: duration / 2
			});
}

// Add click listener for firework creation
document.addEventListener("click", (e) => {
	createFirework(e.clientX, e.clientY);

});

// Automatically trigger a firework when the page loads
window.onload = function () {
	const centerX = window.innerWidth / 2;
	const centerY = window.innerHeight / 2;
	createFirework(centerX, centerY);
