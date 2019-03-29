FROM ubuntu
USER root

RUN apt-get update && \
    apt-get -y install software-properties-common tzdata && \
    apt-add-repository -y ppa:git-core/ppa && \
    apt-get update && \
    apt-get -y install nginx && \
    apt-get install -y git vim &&\
    git clone https://github.com/pyenv/pyenv.git ~/.pyenv && \
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc && \
    echo 'if command -v pyenv 1>/dev/null 2>&1; then\n eval "$(pyenv init -)"\nfi' >> ~/.bashrc

RUN apt-get install -y make build-essential libssl-dev zlib1g-dev \
                       libbz2-dev libreadline-dev libsqlite3-dev wget \
                       curl llvm libncurses5-dev xz-utils tk-dev \
                       libxml2-dev libxmlsec1-dev libffi-dev

ENV PATH $PATH:/root/.pyenv/bin

RUN pyenv install 3.6.5 && \
    pyenv global 3.6.5 && \
    pyenv rehash

ENV PATH $PATH:/root/.pyenv/shims

COPY requirements.txt ./
RUN pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

COPY app /var/app

COPY default.conf /etc/nginx/conf.d/default.conf

CMD ["/bin/bash", "/var/app/startup.sh"]