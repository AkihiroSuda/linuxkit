# FIXME: maintainers please push and update linuxkit/alpine
FROM linuxkit/alpine
RUN \
  apk add \
  btrfs-progs-dev \
  gcc \
  git \
  go \
  libc-dev \
  linux-headers \
  make \
  && true
ENV GOPATH=/root/go
RUN mkdir -p $GOPATH/src/github.com/containerd && \
  cd $GOPATH/src/github.com/containerd && \
  git clone https://github.com/containerd/containerd.git
WORKDIR $GOPATH/src/github.com/containerd/containerd
# CONTAINERD_COMMIT is defined in linuxkit/alpine
RUN git checkout $CONTAINERD_COMMIT
# i.e. snapshotters
ENTRYPOINT ["make", "root-test"]
LABEL org.mobyproject.config='{"net": "host", "capabilities": ["all"], "tmpfs": ["/tmp:exec"], "binds": ["/dev:/dev"]}'
