# Usamos a imagem mais recente do Ubuntu como base
FROM ubuntu:latest
# Evita que a instalação de pacotes peça interações manuais
ENV DEBIAN_FRONTEND=noninteractive
# Instala os pacotes necessários e limpa o cache
RUN apt update && apt install -y \
openssh-server \
sudo \
fail2ban \
nano \
systemd \
&& apt clean && rm -rf /var/lib/apt/lists/*
# Cria um usuário "aluno" com a senha "alunoif" para o exercício
RUN useradd -m -s /bin/bash aluno && echo "aluno:alunoif" | chpasswd
# Adiciona o usuário "aluno" ao grupo sudo
RUN usermod -aG sudo aluno
# ATENÇÃO: A linha abaixo é propositalmente insegura para fins didáticos,
# permitindo que o ataque de força bruta funcione para o teste.
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
# Habilita o serviço SSH para iniciar com o sistema
RUN systemctl enable ssh
# Expõe a porta 22 do container
EXPOSE 22
# Comando que inicia o systemd (que por sua vez iniciará o sshd)
CMD ["/sbin/init"]