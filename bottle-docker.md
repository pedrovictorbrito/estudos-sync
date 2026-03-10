Dockerizing a Bottle application is a great move—it’s a lightweight framework, so it pairs perfectly with a lean container. Since Bottle has no dependencies (it's just a single file), the process is remarkably straightforward.
Here is a step-by-step guide to getting your app into a container.
1. Project Structure
Ensure your project looks something like this:
my-bottle-app/
├── app.py           # Your Bottle application
├── requirements.txt # Dependencies (even if it's just 'bottle')
└── Dockerfile       # The instructions for Docker

2. Prepare the App (app.py)
When running in Docker, you must set the host to 0.0.0.0 so it listens on all network interfaces, not just localhost.
from bottle import route, run

@route('/')
def hello():
    return {"message": "Hello from Docker!"}

if __name__ == '__main__':
    run(host='0.0.0.0', port=8080)

3. The Dockerfile
We’ll use a "slim" Python image to keep the footprint small.
# Use a lightweight Python base image
FROM python:3.11-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements file and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Expose the port Bottle is running on
EXPOSE 8080

# Command to run the application
CMD ["python", "app.py"]

4. Build and Run
Open your terminal in the project folder and run the following:
Build the Image
docker build -t my-bottle-app .

Run the Container
docker run -p 8080:8080 my-bottle-app

> Note: The -p 8080:8080 flag maps your computer's port 8080 to the container's port 8080.
> 
Pro-Tips for Bottle
 * Production Server: Bottle’s built-in server is for development. For production, add gunicorn or waitress to your requirements.txt and update your CMD:
   * CMD ["gunicorn", "-b", "0.0.0.0:8080", "app:app"]
 * Hot Reloading: If you want to see changes without rebuilding the image during development, use a Volume:
   * docker run -p 8080:8080 -v $(pwd):/app my-bottle-app
Would you like me to show you how to set up a docker-compose.yml file to handle multiple services like a database alongside your Bottle app?
