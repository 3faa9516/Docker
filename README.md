# Building Images

Example for kali-linux
```bash
alias kali-build='docker stop kali >/dev/null 2>&1; docker remove kali >/dev/null 2>&1; docker image remove kali-amd64 2>/dev/null; docker build --build-arg UNAME=$(whoami) --build-arg PASSWD=$(openssl passwd) --platform linux/amd64 -t kali-amd64 /Users/nk/Docker/kali-linux/'
```

Creating new containers
```bash
alias kali-new='docker stop kali >/dev/null 2>&1; docker remove kali >/dev/null 2>&1; clear && docker run --platform linux/amd64 --name kali --hostname kali --mount type=bind,source=/Users/nk/Docker/kali-linux/Shared,target=/home/nk/Shared -it kali-amd64'
```

Running / attaching to existing container
```bash
alias kali='docker start kali >/dev/null && clear && docker attach kali'
```