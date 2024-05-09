Docker is needed to build the enviroment.
Reference your system manual (or wiki) to install docker first.

### Usage:
```
git clone git@github.com:Lori3f6/openwrt-buildenv-docker.git
cd openwrt-buildenv-docker/alpine
docker build . --tag <image-tag>
```
You could use build parameter `REV` to switch from branch/tags automatically.   
For example use `--build-arg REV=v22.03.2` to checkout to v22.03.2 tag.  
Use build parameter `APK_MIRROR` to switch a proper apk mirror could help you building the enviroment more smoothly.    
`image-tag` is a custom name for your built image, choose a name you like and keep it in mind. For example `env/openwrt-build:bleedingEdge`.  

For examaple with all settings:
```
docker build . --build-arg REV=v22.03.2 --build-arg APK_MIRROR=mirror.nju.edu.cn --tag <image-tag>
```
complete version ^

Then start the docker containter with built image.
```
docker run -d --restart always --name <custom-name> <image-tag>
```
`custom-name` is a name for your container (which is a instance of image just built), choose one properly and keep it in mind. (For example: `openwrt-build`)  
Use `docker exec` to enter shell inside container
```
docker exec -i -t <custom-name> ash
```
Then follow the [OpenWrt Developer Guide](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem) to configure your OpenWrt System (from Update Feeds step).


