FROM golang:1.27

ARG GIT_URL=https://github.com/86shin/isucon7-qualify.git

RUN git clone $GIT_URL /home/isucon/isubata
WORKDIR /home/isucon/isubata/webapp/go
# Support MySQL 8 caching_sha2_password while retaining the GOPATH layout.
# v1.7.1 has no external Go dependencies.
RUN rm -rf src/isubata/vendor/github.com/go-sql-driver/mysql && \
    git clone --depth=1 --branch=v1.7.1 https://github.com/go-sql-driver/mysql.git src/isubata/vendor/github.com/go-sql-driver/mysql && \
    rm -rf src/isubata/vendor/github.com/go-sql-driver/mysql/.git
# The upstream Makefile builds src/isubata using GOPATH, without go.mod.
RUN GO111MODULE=off make

EXPOSE 5000

ENTRYPOINT ["/home/isucon/isubata/webapp/go/isubata"]
