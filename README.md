# Podman-Desktop 

* Accessing Podman from another WSL2 distribution   
    1) Install the podman client on your WSL distribution 
        ```
        $ sudo apt update
        $ sudo apt install podman
        ```
    2) Assign uucp group membership to user on your WSL distribution (to communicate with the Podman Machine's socket file)
        ```
        $ sudo usermod --append --groups 10 your_user
        ```
    3) Set an alias to use the remote Podman and DOCKER_HOST environment variable (edit shell profile on WSL distribution)
        ```
        alias podman='podman --remote --url="unix:///mnt/wsl/podman-sockets/podman-machine-default/podman-root.sock"'

        export DOCKER_HOST=unix:///mnt/wsl/podman-sockets/podman-machine-default/
        ``` 
        sample .zshrc 
        ```
        eval "$(starship init zsh)"

        alias kubectl=/mnt/c/ProgramData/chocolatey/bin/kubectl.exe
        alias oc=/mnt/c/ProgramData/chocolatey/bin/oc.exe
        alias dive=/mnt/c/ProgramData/chocolatey/bin/dive
        alias podman='podman --remote --url="unix:///mnt/wsl/podman-sockets/podman-machine-default/podman-root.sock"'


        export KUBECONFIG=/mnt/c/Users/your_user/.kube/config
        export PATH=$PATH:/opt/apache-maven-3.9.6/bin
        export JAVA_HOME=/usr/lib/jvm/temurin-17-jdk-amd64
        export DOCKER_HOST=unix:///mnt/wsl/podman-sockets/podman-machine-default/podman-root.sock

        source <(kubectl completion zsh)
        source <(oc completion zsh)

        plugins=(
            docker
            git
            kubectl
            oc
            zsh-syntax-highlighting
            zsh-autosuggestions
        )

        if [ $commands[oc] ]; then
        source <(oc completion zsh)
        compdef _oc oc
        fi
        ```
