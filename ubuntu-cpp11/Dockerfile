FROM ubuntu:18.04
ENV USER=deploy
ENV PASSWD=deploy
ENV WORKDIR=projects

# 本教程使用ubuntu默认源（需要科学上网）
# 如需更换源请打开:
#RUN printf '\n\
#deb http://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse \n\
#deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse \n\
#deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse \n\
#deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse \n\
#deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse \n\
#deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse \n\
#deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse \n\
#deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse \n\
#deb http://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse \n\
#deb-src http://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse' > /etc/apt/sources.list

# 更新源
RUN apt-get clean -y && apt-get update -y && apt-get upgrade -y

# 安装开发环境必要的包
RUN apt-get install -y vim gcc gdb g++ build-essential net-tools python3 python3-pip sudo libboost-dev rsync openssh-server cmake git ssh curl wget openssl m4

# 安装gcc11
RUN apt-get -y install software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update -y
RUN apt-get -y install gcc-11 g++-11
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 60 --slave /usr/bin/g++ g++ /usr/bin/g++-11

# cmake (也可下载到本地COPY进容器。下载地址: https://cmake.org/files/)
# COPY ./*.gz /opt/
# RUN cd /opt/ && tar -zxvf cmake-3.22.4-linux-x86_64.tar.gz && sudo ln -s /opt/cmake-3.22.4-linux-x86_64/bin/* /usr/local/bin
# 在线现在 & 安装
RUN wget -P /opt/ https://cmake.org/files/v3.22/cmake-3.22.4-linux-x86_64.tar.gz && cd /opt/ && tar -zxvf cmake-3.22.4-linux-x86_64.tar.gz && sudo ln -s /opt/cmake-3.22.4-linux-x86_64/bin/* /usr/local/bin

# conan
RUN pip3 install conan -i https://pypi.douban.com/simple

# 添加用户并配置密码
RUN useradd -m ${USER} && yes ${PASSWD} | passwd ${USER}

# 赋予sudo权限并允许无密码sudo
RUN echo ${USER}' ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chmod 644 /etc/sudoers

CMD ["/usr/sbin/sshd", "-D"]

USER ${USER}
RUN mkdir -p /home/${USER}/${WORKDIR}/
ENV LC_ALL C.UTF-8