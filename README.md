
# Webcam Processing for privacy issue fixed

This Docker image contains a Flask application that captures webcam video, processes it to detect faces, and saves the output video. The app provides endpoints to start and stop the video processing.

## Prerequisites

- Docker installed on your system
- A webcam connected to your system

## Building the Docker Image

To build the Docker image, navigate to the project directory and run:

```sh
docker build -t muffinhead25/my-flask-app:latest .
```

## Running the Docker Container

To run the Docker container with the necessary permissions for accessing the webcam, use the following command:

```sh
docker run --rm -it --device=/dev/video0 -v $(pwd)/output:/app/output -p 5000:5000 muffinhead25/my-flask-app:latest
```

Explanation:
- `--rm`: Automatically remove the container when it exits
- `-it`: Run the container in interactive mode
- `--device=/dev/video0`: Allow the container to access the webcam
- `-v $(pwd)/output:/app/output`: Mount the output directory to save the processed video
- `-p 5000:5000`: Map port 5000 of the container to port 5000 of the host
- `muffinhead25/my-flask-app:latest`: The Docker image to run

## Using the Flask App

Once the container is running, you can use the following endpoints to control the video processing:

### Start Processing

To start the video processing, send a GET request to:

```
http://localhost:5000/start
```

### Stop Processing

To stop the video processing, send a GET request to:

```
http://localhost:5000/stop
```

### Downloading the Processed Video

The processed video will be saved in the `output` directory of the current working directory on the host machine. You can find the video file named `output_with_face.mp4`.

## Example Commands

```sh
# Start the Flask app
docker run --rm -it --device=/dev/video0 -v $(pwd)/output:/app/output -p 5000:5000 muffinhead25/my-flask-app:latest

# In a separate terminal, start processing
curl http://localhost:5000/start

# Stop processing
curl http://localhost:5000/stop
```

## Notes

- Ensure the webcam is connected and accessible via `/dev/video0`.
- The output video will be saved in the `output` directory of the host machine.
```

### Add the `README.md` file to your project directory

Ensure the `README.md` file is in the same directory as your Dockerfile.

### Rebuild the Docker Image

Rebuild the Docker image to include the `README.md` file.

```sh
docker build -t muffinhead25/my-flask-app:latest .
```

With these instructions, anyone should be able to run your Docker container and use the Flask app to process webcam video.
