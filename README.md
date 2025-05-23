## Prerequesits
- [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) (if you are running Windows. This is just more reliable than running it barebones on Windows in the long run)
- [Nvidia Cuda](https://developer.nvidia.com/cuda-downloads) (Or the AMD/Intel equivalent depending on your GPU)
- [Docker](https://www.docker.com/) (Only a requirement for Open-WebUI)
### Installing Ollama
In a Powershell terminal, run each command hitting enter after each line and letting them run
- `wsl`
- `sudo apt update`
- `sudo apt upgrade -y`
- `sudo apt install curl`
- `curl https://ollama.ai/install.sh | sh`

To obtain new AI models you can run:
	`ollama pull {model:arg}`
 
A full list of available models and their arguments can be found on the Ollama Libraries page of their website, [ollama.com/library](https://ollama.com/library)
### Access Ollama on other machines
To forward WSL ports so that Ollama can be accessed by other machines:

1. You will first want to find the IPv4 address of your WSL instance. In WSL, run the following command to find the IPv4 address

`hostname -I`

2. Then, in Powershell (as admin) Run the following command

`netsh interface portproxy add v4tov4 listenport=11434 listenaddress=0.0.0.0 connectport=11434 connectaddress={WSL_IPv4_Address}`

To check that your change applied properly, run

`netsh interface portproxy show all`

## Open-WebUI
Installed through Docker, once installed can be accessed from your_host_ip:3000 (localhost:3000 for example)

To install Open-WebUI
1. Pull the latest version of the Docker image:

`docker pull ghcr.io/open-webui/open-webui:main`

2. Start the container using the recently pulled Docker image:

`docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main`


To update Open-WebUI

1. Stop and remove the current container:

`docker rm -f open-webui`

2. Pull the latest version of the Docker image:

`docker pull ghcr.io/open-webui/open-webui:main`

3. Start the container again:

`docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main`
