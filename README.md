# Particle-

Live at https://voidxayush.github.io/Particle-Simulation-/

Key Features included:
MediaPipe Integration: Tracks hand distance (spread) and finger tension (fist vs. open palm).
GLSL Shaders: Renders 15,000+ particles with high performance.
Morph Targets: Smoothly interpolates positions between Heart, Saturn, Flower, Zen (stacked stones), and Fireworks.
Physics Engine: Custom velocity-based system implementing noise, drag, and spring forces toward target shapes.
Modern UI: Glassmorphism design with fallbacks for mouse/touch if the camera is denied.

How to use this ?
Run Locally:
Save the code above as index.html.
You must serve it via a local server (browsers block Webcam access on file:// protocol).
If you have Python installed: run python -m http.server in the folder and go to http://localhost:8000.
Or use VS Code with the "Live Server" extension.
Controls:
Gestures (Webcam):
Open Hands: Particles scatter, noise increases (chaos).
Closed Fists: Particles tighten and form the shape solidly.
Hands Apart: Scales the object up.
Hands Together: Scales the object down.
Manual (Mouse):
Disable the camera toggle in the UI.
Drag to rotate.
Scroll to zoom.

Technical Details
Performance: Uses Three.Points and a custom ShaderMaterial. The vertex shader handles the size attenuation (particles get smaller when further away), and the fragment shader draws a soft, glowy circle instead of a square.
Vision: Uses the MediaPipe HandLandmarker. We calculate two specific metrics:
Openness Ratio: Distance from Index Tip to Wrist divided by Hand Scale. This is robust against moving your hand closer/further from the camera.
Spread: Euclidean distance between the two wrist landmarks.
Physics: We don't just snap particles to the shape. Every frame, a particle calculates a spring force towards its target position in the current shape (Heart, Saturn, etc.). We then add "Noise" (random velocity) based on how open your hand is. This creates the fluid, organic movement.
