# Viva Questions and Short Answers

1. What is DevOps in simple terms?
DevOps is a practice that combines development and operations to deliver software faster and more reliably.

2. Why did you use Docker in this project?
Docker gives a consistent runtime environment so the app works the same on every machine.

3. What is a Docker image?
A Docker image is a packaged blueprint containing app code, dependencies, and runtime settings.

4. What is a Docker container?
A container is a running instance of a Docker image.

5. Why expose port 8501?
Streamlit serves the web app on port 8501 by default, so we map that port to localhost.

6. What is CI/CD and what did you implement?
CI/CD automates build and validation steps. I implemented CI to install dependencies, run a smoke test, and build the Docker image.

7. Why is the CI smoke test useful?
It quickly verifies essential files and dependencies so obvious breakages are caught early.

8. Why keep deployment local and not cloud?
The submission requirement is localhost-only, so local Docker is enough and avoids unnecessary complexity.

9. What problem does .dockerignore solve?
It reduces build context size and prevents unnecessary files from being copied into Docker images.

10. How is ML deployment demonstrated here?
The trained model files are bundled with the app and loaded at runtime inside a Docker container on localhost.
