# Guide for setting up GPU support using Docker in WSL2
See https://www.youtube.com/watch?v=xJtmj6hX5Lg for more info. This guide is based on the WSL portion.

## Install WSL
1. Launch Powershell 
2. Run `wsl --install`. This will add Ubuntu app, just search Ubuntu from start menu to start running Linux Subsystem.
3. Setup terminal with username and password. 
4. Update terminal using `sudo apt update && sudo apt upgrade`
 
## Add Docker to Ubuntu 
1. Download installation script with `curl -fsSL https://get.docker.com -o get-docker.sh`
2. The run the script with `sudo sh get-docker.sh`
3. Hit enter to ignore warnings--We want the Linux version
4. Run `Docker --version` to verify proper insallation. 

### Add user to docker and verify Docker is working
1. Ensure users have access to Docker: run `sudo groupadd docker` then `sudo usermod -aG docker $USER`
2. Exit terminal and relaunch.
3. Run Docker sample script with: `docker run hello-world`--should get "Hello from Docker!" message.

## Install and Setup NVIDIA Cuda Toolkit with Docker container
1. Run `curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list`
2. Run `sudo apt-get update`
3. Finally, run `sudo apt-get install -y nvidia-container-toolkit`

### Configure Docker to use Cuda Toolkit
1. Run `sudo nvidia-ctk runtime configure --runtime=docker` to create configuration file for Docker
2. Restart Docker using: `sudo systemctl restart docker`
3. To verify Docker has access to GPU run: `docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi`
4. Verify that both driver and Cuda version are shown.

## Launch TensorFlow from Docker container
Open container using `docker run --gpus all -it tensorflow/tensorflow:latest-gpu bash`
   
This will open a shell within the container. You can now run tensorflow with GPU access. 

Keep in mind that, using this command anything done within the container is lost once the container is exited. 

# Using Docker GPU setup in working directory (saves files)
Here we want to open a docker container mapping the current working directory to the docker container. 

This can be done using the command: `docker run --gpus all -it -v $PWD:/working -w /working tensorflow/tensorflow:latest-gpu bash`

Now you can access your working directory within the docker container. All files should be saved to the working directory when docker container is exited.

**Note:** See tensorflow-bootcamp repo or dogvision README's for more on running dockerfiles.