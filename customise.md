# Customise

To customise this image first download the [2019](https://github.com/modalitysystems/modalitysoftware-docs/releases/download/ltsc2019/vsts-agent-ltsc2019.zip) version of the docker file package which will require a 2019 host, and extract the downloaded zip file.

![Dockerfile](images/dockerfile-install.png)

The tools installation has been taken out of the Dockerfile and put into a single install.ps1 file, this is to reduce the number of layers that Docker produces which greatly reduces of overall image size

Make appropriate adjustments but leave start.ps1 script unchanged

Open PowerShell from the extraction location and run the following command:

docker build -t vsts-agent:1.0 .

To create a container from this image and access a powershell prompt run the following command:

docker run --rm -it vsts-agent:1.0 powershell.exe

To create an Azure DevOps Agent from this image run the following command:

docker run -e AZP_URL=? -e AZP_TOKEN=? -e AZP_POOL=? -d vsts-agent:1.0

# Push to Container Registry

To avoid having to build an image on every Docker Host, the image should be pushed to a container registry such as [Docker Hub](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub) or [Azure Container Registry](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-get-started-docker-cli?tabs=azure-cli). For local networks with limited internet speeds then using a Private Docker Registry could be an option.

# Automate process with a Pipeline

Once you have your customised docker files, put them into source control and link them to a pipeline such as this:

![Pipeline](images/pipeline.png)
