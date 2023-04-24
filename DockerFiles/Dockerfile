FROM ubuntu:latest

LABEL maintainer="Your Name <your-email@example.com>"

# Update the packages and install SSH server, Python and pip
RUN apt-get update && \
    apt-get install -y openssh-server python3 python3-pip && \
    mkdir /var/run/sshd

# Configure SSH server
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    echo "root:password" | chpasswd && \
    echo "ListenAddress 0.0.0.0" >> /etc/ssh/sshd_config

# Copy public key to container and set permissions
COPY id_rsa.pub /root/.ssh/authorized_keys
RUN chmod 600 /root/.ssh/authorized_keys && \
    chown root:root /root/.ssh/authorized_keys

# Set the working directory to /app and copy the Flask app files
#WORKDIR /app
#COPY . /app

# Install Flask requirements
#RUN pip3 install --no-cache-dir -r requirements.txt

# Expose ports for incoming SSH and Flask connections
EXPOSE 22
EXPOSE 80

# Start SSH server and Flask app
CMD ["/usr/sbin/sshd", "-D"]



