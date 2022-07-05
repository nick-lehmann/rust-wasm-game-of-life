FROM rust:slim-buster

WORKDIR /home/

COPY . .

## Update general dependencies
RUN apt-get update && apt-get install -y \
  curl \
  git \
  gnupg2 \
  jq \
  sudo \
  zsh \
  vim \
  build-essential \
  openssl

## Install rust components via `rustup`
RUN rustup install nightly && \
    rustup component add rustfmt && \
    rustup component add rustfmt --toolchain nightly && \
    rustup component add clippy  && \
    rustup component add clippy --toolchain nightly

## Install common cargo commands
RUN cargo install cargo-expand && \
    cargo install cargo-edit

# Install `wasm-pack`
RUN curl https://rustwasm.github.io/wasm-pack/installer/init.sh -sSf | sh 

## setup and install oh-my-zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \
    cp -R /root/.oh-my-zsh /home/$USERNAME && \
    cp /root/.zshrc /home/$USERNAME && \
    sed -i -e "s/\/root\/.oh-my-zsh/\/home\/$USERNAME\/.oh-my-zsh/g" /home/$USERNAME/.zshrc && \
    chown -R $USER_UID:$USER_GID /home/$USERNAME/.oh-my-zsh /home/$USERNAME/.zshrc

ENV PATH="/root/.cargo/bin:$PATH"
