# gzweb_docker

This Image works with Gazebo 7.16 + gzweb 1.4.0 + node 10.22.1

# For running the image
```bash
sudo docker run -it -p 8080:8080 kapildesh/gzweb7:v1 bash
```
# For adding models

- inside the container make a directory as
```bash
mkdir custom_models 
```
- copy local models inside the container
```bash
sudo docker cp host-machine-model-path <container-id>:/root/custom_models
```
- now deploy these models to be used by gzweb
```bash
cd ~/gzweb
export GAZEBO_MODEL_PATH=/root/custom_models
npm run deploy --- -m local
```
- (*Optional*) coarse the models to be easily renderable on mobile devices
```bash
cd ~/gzweb
npm run deploy --- -c
```
# For running Gzweb
```bash
export GAZEBO_MASTER_URI="http:172.17.0.1:11345" # 172.17.0.1 being the ip of the host machine provided by the docker engine
cd ~/gzweb
npm start
```
