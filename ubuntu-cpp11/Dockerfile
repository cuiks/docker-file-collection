FROM ubuntu:22.04
ENV USER=deploy
ENV PASSWD=deploy
ENV WORKDIR=projects

# 修改中科大源
# ADD https://mirrors.ustc.edu.cn/repogen/conf/ubuntu-http-4-jammy /etc/apt/sources.list
ADD ./sources.list /etc/apt/sources.list

# 更新源
RUN apt-get clean -y && apt-get update -y && apt-get upgrade -y

# 安装开发环境必要的包
RUN apt-get install -y vim gcc g++ make cmake build-essential net-tools python3 python3-pip sudo libboost-dev rsync openssh-server cmake git ssh curl wget openssl m4

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