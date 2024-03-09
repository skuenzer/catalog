# Python Flask Web Server

This directory contains a Python [`Flask`](https://flask.palletsprojects.com) web server running on Unikraft.

## Set Up

To run this example, [install Unikraft's companion command-line toolchain `kraft`](https://unikraft.org/docs/cli), clone this repository and `cd` into this directory.

## Run and Use

Use `kraft` to run the image and start a Unikraft instance:

```bash
kraft run --rm -p 8080:8080 --plat qemu --arch x86_64 -M 512M .
```

If the `--plat` argument is left out, it defaults to `qemu`.
If the `--arch` argument is left out, it defaults to your system's CPU architecture.

Once executed, it will open port `8080` and wait for connections.
To test it, you can use `curl`:

```bash
curl localhost:8080
```

You should see a "Hello, Flask World!" message.

## Inspect and Close

To list information about the Unikraft instance, use:

```bash
kraft ps
```

```text
NAME            KERNEL                          ARGS                             CREATED         STATUS   MEM   PORTS                   PLAT
naughty_sultan  oci://unikraft.org/python:3.12  /usr/bin/python3 /app/server.py  14 seconds ago  running  0MiB  0.0.0.0:8080->8080/tcp  qemu/x86_64
```

The instance name is `naughty_sultan`.
To close the Unikraft instance, close the `kraft` process (e.g., via `Ctrl+c`) or run:

```bash
kraft rm naughty_sultan
```

Note that depending on how you modify this example your instance **may** need more memory to run.
To do so, use the `kraft run`'s `-M` flag, for example:

```bash
kraft run -p 8080:8080 --plat qemu --arch x86_64 -M 1024M .
```

## `kraft` and `sudo`

Mixing invocations of `kraft` and `sudo` can lead to unexpected behavior.
Read more about how to start `kraft` without `sudo` at [https://unikraft.org/sudoless](https://unikraft.org/sudoless).

## Learn More

- [How to run unikernels locally](https://unikraft.org/docs/cli/running)
- [Building `Dockerfile` Images with `BuildKit`](https://unikraft.org/guides/building-dockerfile-images-with-buildkit)