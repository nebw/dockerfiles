FROM base/archlinux
MAINTAINER nimajnebwild@gmail.com

RUN echo 'Server = http://ftp.spline.inf.fu-berlin.de/mirrors/archlinux/$repo/os/$arch' > /etc/pacman.d/mirrorlist
RUN pacman -Sy --noconfirm && \
	pacman-db-upgrade
RUN pacman -Syu --noconfirm

RUN pacman --noconfirm --needed -S \
      pacman-contrib \
      git \
      base-devel \
      gtkglext \
      hdf5 \
      opencv \
      python \
      vim \
      python-numpy \
      python-pandas \
      python-scipy \
      python-pip \
      jupyter-notebook \ 
	&& paccache -rfk0

# set UTF-8 locale
RUN echo 'en_US.UTF-8 UTF-8' > /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8

RUN pacman --noconfirm --needed -S \
        cuda \
        cudnn \
        python-tensorflow-opt-cuda \ 
        tensorboard \ 
        python-pytorch-cuda \ 
    && paccache -rfk0;

RUN pacman --noconfirm --needed -S \
        python-h5py \
        python-scikit-learn \
        python-matplotlib \
        python-seaborn \
    && paccache -rfk0;

RUN pip3 install keras

ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.0"

ARG UNAME=testuser
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID -o $UNAME
RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME
USER $UNAME
CMD /bin/bash
