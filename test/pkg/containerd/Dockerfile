# alpine 3.5 lacks go1.8
FROM golang:1.8
RUN apt update && apt install -y btrfs-tools
ENV CONTAINERD_COMMIT=199544ea8009bf6988a81456c7dec66b2d3268e0
RUN mkdir -p $GOPATH/src/github.com/containerd && \
  cd $GOPATH/src/github.com/containerd && \
  git clone https://github.com/containerd/containerd.git
WORKDIR $GOPATH/src/github.com/containerd/containerd
RUN git checkout $CONTAINERD_COMMIT
# i.e. snapshotters
ENTRYPOINT ["make", "root-test"]
LABEL org.mobyproject.config='{"net": "host", "capabilities": ["all"], "tmpfs": ["/tmp:exec"]}'

