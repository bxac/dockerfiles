FROM centos:7
RUN yum install -y wget git mercurial gcc-c++ cmake openssl-devel libcurl-devel libzip5-devel libsodium-devel libuv-devel libstdc++-static
RUN yum install -y make rpm-build unzip bzip2 scl-utils
RUN yum install -y centos-release-scl
RUN yum install -y devtoolset-6
RUN source scl_source enable devtoolset-6
RUN mkdir /tmp/build
WORKDIR /tmp/build
RUN wget https://github.com/Kitware/CMake/releases/download/v3.13.2/cmake-3.13.2-Linux-x86_64.sh
RUN chmod +x cmake-3.13.2-Linux-x86_64.sh
RUN yes | ./cmake-3.13.2-Linux-x86_64.sh --skip-license --prefix=/usr

WORKDIR /tmp/build
RUN git clone https://github.com/enthought/bzip2-1.0.6 && cd bzip2-1.0.6 && make && make install
RUN git clone https://github.com/madler/zlib && cd zlib && ./configure && make && make install
RUN git clone https://github.com/nih-at/libzip && cd libzip && mkdir build && cd build && cmake .. -DBUILD_SHARED_LIBS=OFF -DBUILD_TOOLS=OFF -DBUILD_REGRESS=OFF -DBUILD_EXAMPLES=OFF && make && make install
RUN git clone https://github.com/openssl/openssl && cd openssl && ./config --no-tests && make && make install
RUN git clone https://github.com/curl/curl && cd curl && mkdir build && cd build && cmake -DBUILD_SHARED_LIBS=OFF -DCURL_STATICLIB=ON -DBUILD_TESTING=OFF -DBUILD_CURL_EXE=OFF -DCURL_DISABLE_LDAP=ON -DOPENSSL_USE_STATIC_LIBS=TRUE .. && make && make install
