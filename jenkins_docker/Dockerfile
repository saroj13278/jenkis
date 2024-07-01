# Use the official Ubuntu base image
FROM ubuntu:latest

# Update the package list and install required packages
RUN apt-get update && \
    apt-get install -y openssh-server sudo

# Create a new user 'remote_user' and set a password
RUN useradd -m remote_user && echo "remote_user:password" | chpasswd && adduser remote_user sudo

# Create SSH directory and set permissions
RUN mkdir /home/remote_user/.ssh && chown remote_user:remote_user /home/remote_user/.ssh && chmod 700 /home/remote_user/.ssh

# Copy the SSH public key to the authorized_keys file
# Note: You should have a public key file named remote-key.pub in the same directory as this Dockerfile
COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

# Set the correct permissions for the authorized_keys file
RUN chown remote_user:remote_user /home/remote_user/.ssh/authorized_keys && chmod 600 /home/remote_user/.ssh/authorized_keys

# Start the SSH service
RUN service ssh start

# Expose the SSH port
EXPOSE 22

RUN apt-get install -y curl


RUN apt-get install -y mysql-client
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN apt-get install -y unzip
RUN unzip awscliv2.zip
RUN ./aws/install


# Run the SSH service in the foreground
CMD ["/usr/sbin/sshd", "-D"]
