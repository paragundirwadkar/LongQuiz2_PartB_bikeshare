# bikeshare_cicd_M4P4
# Conitious deployment with docker , github runner and cloud

# update
sudo apt-get update
sudo apt-get upgrade -y

# docker installation
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world



# Github Runner commands on aws
mkdir actions-runner && cd actions-runner
curl -o actions-runner-linux-x64-2.305.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.305.0/actions-runner-linux-x64-2.305.0.tar.gz
echo "737bdcef6287a11672d6a5a752d70a7c96b4934de512b7eb283be6f51a563f2f  actions-runner-linux-x64-2.305.0.tar.gz" | shasum -a 256 -c
echo "737bdcef6287a11672d6a5a752d70a7c96b4934de512b7eb283be6f51a563f2f  actions-runner-linux-x64-2.305.0.tar.gz" | shasum -a 256 -c

tar -xvf ./actions-runner-linux-x64-2.305.0.tar.gz

# This is just sample : u need to use new token always
# https://github.com/paragundirwadkar/bikeshare_cicd_M4P4/settings/actions/runners/new?arch=x64&os=linux

./config.sh --url https://github.com/paragundirwadkar/bikeshare_cicd_M4P4 --token A6H5LCCVMIGRRNYTEVVH5Y3EVQ6T6
./run.sh

# doker commands
sudo docker ps
sudo docker logs -f <id from sudo docker ps >