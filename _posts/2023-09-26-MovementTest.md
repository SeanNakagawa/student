---
toc: true
comments: true
layout: post
title: Background/Platform Test
description: To test the background and platform with movements
type: hacks
courses: { csse: {week: 5} }
---

%%html
<html>
<head>
    <style>
        #canvas {
            margin: 0;
            border: 1px solid white;
            background-image: url('https://raw.githubusercontent.com/SeanNakagawa/student/main/images/room1.png');
            background-size: cover;
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <script>
        // Create empty canvas
        let canvas = document.getElementById('canvas');
        let c = canvas.getContext('2d');
        // Set the canvas dimensions
        canvas.width = 850;
        canvas.height = 350;
        // Define gravity value
        let gravity = 1.5;
        // Define the Player class
        class Player {
            constructor() {
                // Initial position and velocity of the player
                this.position = {
                    x: 300,
                    y: 200
                };
                this.velocity = {
                    x: 0,
                    y: 0
                };
                // Dimensions of the player
                this.width = 30;
                this.height = 30;
            }
            // Method to draw the player on the canvas
            draw() {
                c.fillStyle = 'red';
                c.fillRect(this.position.x, this.position.y, this.width, this.height);
            }
            // Method to update the player position and velocity
            update() {
                this.draw();
                this.position.y += this.velocity.y;
                this.position.x += this.velocity.x;
                // Apply gravity if player is not at the bottom
                if (this.position.y + this.height + this.velocity.y <= canvas.height)
                    this.velocity.y += gravity;
                else
                    this.velocity.y = 0;
            }
        }
        // Define the Platform class
        class Platform {
            constructor(image) {
                // Initial position of the platform
                this.position = {
                    x: 0,
                    y: 300,
                }
                this.image = image;
                this.width = 850;
                this.height = 30;
            }
            // Method to draw the platform on the canvas
            draw() {
                c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
            }
        }
        // Define the Tube class
        class Tube {
            constructor(image) {
                // Initial position of the tube
                this.position = {
                    x: 48,
                    y: 180
                }
                this.image = image;
                // Define the hitbox dimensions (decrease the height by 75%)
                this.hitbox = {
                    x: this.position.x,
                    y: this.position.y,
                    width: 200, // Adjust the width of the hitbox
                    height: 75 // Decrease the height of the hitbox by 75%
                };
            }
            // Method to draw the tube on the canvas
            draw() {
                c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
            }
        }
        // Load images
        let image = new Image();
        let imageTube = new Image();
        image.src = 'https://raw.githubusercontent.com/SeanNakagawa/student/main/images/floor1.png'
        imageTube.src = 'https://raw.githubusercontent.com/SeanNakagawa/student/main/images/bed1.png'
        // Create platform and tube objects
        let platform = new Platform(image);
        let tube = new Tube(imageTube);
        // Create a player object
        player = new Player();
        // Define keyboard keys and their states
        let keys = {
            right: {
                pressed: false
            },
            left: {
                pressed: false
            }
        }
        // Animation function to continuously update and render the canvas
        function animate() {
            requestAnimationFrame(animate);
            c.clearRect(0, 0, canvas.width, canvas.height);
            // Draw the platform, player, and tube
            platform.draw();
            player.update();
            tube.draw();
            // Control player horizontal movement
            if (keys.right.pressed && player.position.x + player.width <= canvas.width - 50) {
                player.velocity.x = 15;
            } else if (keys.left.pressed && player.position.x >= 50) {
                player.velocity.x = -15;
            } else {
                player.velocity.x = 0;
            }
            // Check for collision between player and platform
            if (
                player.position.y + player.height <= platform.position.y &&
                player.position.y + player.height + player.velocity.y >= platform.position.y &&
                player.position.x + player.width >= platform.position.x &&
                player.position.x <= platform.position.x + platform.width
            ) {
                player.velocity.y = 0;
            }
            // Check for collision between player and tube
            if (
                player.position.y + player.height <= tube.hitbox.y &&
                player.position.y + player.height + player.velocity.y >= tube.hitbox.y &&
                player.position.x + player.width >= tube.hitbox.x &&
                player.position.x <= tube.hitbox.x + tube.hitbox.width
            ) {
                player.velocity.y = 0;
                player.position.y += 0.1;
                player.velocity.y = 0.0001;
                gravity = 0.2;
            }
            // Reset gravity and collision when not colliding with tube
            if (
                player.position.y + player.height == tube.hitbox.y + tube.hitbox.height ||
                player.position.y + player.height <= tube.hitbox.y ||
                player.position.x + player.width <= tube.hitbox.x ||
                player.position.x >= tube.hitbox.x + tube.hitbox.width
            ) {
                gravity = 1.5;
            }
            // Check for collision between player and tube from other sides
            if (
                player.position.x + player.width <= tube.hitbox.x &&
                player.position.x + player.width + player.velocity.x >= tube.hitbox.x &&
                player.position.y + player.height >= tube.hitbox.y &&
                player.position.y <= tube.hitbox.y + tube.hitbox.height
            ) {
                player.velocity.x = 0;
            }
            if (
                player.position.x >= tube.hitbox.x + tube.hitbox.width &&
                player.position.x + player.velocity.x <= tube.hitbox.x + tube.hitbox.width &&
                player.position.y + player.height >= tube.hitbox.y &&
                player.position.y <= tube.hitbox.y + tube.hitbox.height
            ) {
                player.velocity.x = 0;
            }
            if (
                player.position.x >= tube.hitbox.x &&
                player.position.x + player.velocity.x <= tube.hitbox.x &&
                player.position.y + player.height >= tube.hitbox.y &&
                player.position.y <= tube.hitbox.y + tube.hitbox.height
            ) {
                player.velocity.x = 0;
            }
            if (
                player.position.x + player.width <= tube.hitbox.x + tube.hitbox.width &&
                player.position.x + player.width + player.velocity.x >= tube.hitbox.x + tube.hitbox.width &&
                player.position.y + player.height >= tube.hitbox.y &&
                player.position.y <= tube.hitbox.y + tube.hitbox.height
            ) {
                player.velocity.x = 0;
            }
        }
        // Start the animation loop
        animate();
        // Event listener for keydown events
        addEventListener('keydown', ({ keyCode }) => {
            switch (keyCode) {
                case 65:
                    console.log('left');
                    keys.left.pressed = true;
                    break;
                case 83:
                    console.log('down');
                    break;
                case 68:
                    console.log('right');
                    keys.right.pressed = true;
                    break;
                case 87:
                    console.log('up');
                    player.velocity.y -= 20;
                    break;
            }
        });
        // Event listener for keyup events
        addEventListener('keyup', ({ keyCode }) => {
            switch (keyCode) {
                case 65:
                    console.log('left');
                    keys.left.pressed = false;
                    break;
                case 83:
                    console.log('down');
                    break;
                case 68:
                    console.log('right');
                    keys.right.pressed = false;
                    break;
                case 87:
                    console.log('up');
                    player.velocity.y = -20;
                    break;
            }
        })
    </script>
</body>
</html>
