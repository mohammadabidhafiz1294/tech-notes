
# Somes Docker Commands

- [[Container]] runs inside the bash shell of the container:
```
sudo docker run -t -i --name new_container ubuntu:18.04 /bin/ bash root@79e36bff89b4:/#

```
here some flags explains:
 1.  `-t`  (terminal): This flag tells Docker to allocate a pseudo-tty (terminal) for the container, which allows you to run commands inside the container as if you were running them on a local terminal. When you run a container with the `-t` flag, you can interact with the container as if it were a local shell session.
 2.  `-i`  (interactive): This flag tells Docker to keep stdin open on the container, allowing you to interact with it in real-time. When you run a container with the `-i` flag, you can send input to the container and receive output from it.
 3.  `-f`  (follow): This flag tells Docker to follow the output of the container and display it in your terminal in real-time. When you run a container with the `-f` flag, you can see the log output from the container as it runs.