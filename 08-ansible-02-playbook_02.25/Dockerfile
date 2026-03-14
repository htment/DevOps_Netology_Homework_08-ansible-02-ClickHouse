# Используем официальный образ Ubuntu
FROM ubuntu:22.04

# Отключаем интерактивный режим
ENV DEBIAN_FRONTEND=noninteractive

# Устанавливаем необходимые пакеты
RUN apt-get update && \
    apt-get install -y \
        nano \
        wget \
        curl \
        net-tools \
        iputils-ping \
        openssh-server \
        sudo \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Создаем директорию для SSH
RUN mkdir /var/run/sshd

# Создаем пользователя art с паролем 123 ############## ЭТО ТЕСТОВЫЙ БЛОК В КОНЦЕ УБРАТЬ!!!!!!!!!!!!!!!!!!
RUN useradd -m -s /bin/bash art && \
    echo 'art:123' | chpasswd && \
    usermod -aG sudo art

# Настраиваем SSH для аутентификации по паролю
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PermitEmptyPasswords no/PermitEmptyPasswords no/' /etc/ssh/sshd_config

# Открываем порт для SSH
EXPOSE 22

# Запускаем SSH сервер
CMD ["/usr/sbin/sshd", "-D"]
