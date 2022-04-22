## gcc11开发环境

### 包含工具包
- vim
- net-tools
- openssl
- curl & wget
- ssh & openssh-server
- python3 python3-pip
- gcc & g++ & gdb & gcc11 && g++11
- make & cmake
- conan

### ssh
- 默认用户名: deploy
- 默认密码: deploy
- 默认端口: 127.0.0.1:2222
- 注: 可通过`Dockerfile`进行修改

### 工作目录
- /home/deploy/projects/
注: 可通过`Dockerfile`进行修改


## How To RUN
### docker-compose 使用方法(假设你已经安装docker & docker-compose)
- git clone 本仓库
- cd $repo/ubuntu-cpp1
- docker-compose up -d

### clion配置
- <img src="https://note-site-pic-1259606004.cos.ap-beijing.myqcloud.com/img/20220422095131.png"/>
- <img src="https://note-site-pic-1259606004.cos.ap-beijing.myqcloud.com/img/20220422095202.png"/>
- <img src="https://note-site-pic-1259606004.cos.ap-beijing.myqcloud.com/img/20220422100302.png"/>
- <img src="https://note-site-pic-1259606004.cos.ap-beijing.myqcloud.com/img/20220422100432.png"/>

### conan 初始化
- ssh deploy@127.0.0.1:2222
- cd /home/deploy/projects/$prodir
- conan install . --install-folder=cmake-build-debug-ubuntu-gcc11/conan-dependencies --build=missing
	- `cmake-build-debug-ubuntu-gcc11/conan-dependencies` 为我的项目目录。可自定义
