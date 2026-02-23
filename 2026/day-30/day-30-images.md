A Docker layer is a read-only filesystem change created by each instruction in a Dockerfile. Docker stacks these layers using a union filesystem to build the final image.Docker images
are built from multiple read-only layers, each created by a Dockerfile instruction. Docker uses layers for caching, storage efficiency, faster builds, and layer sharing across images.
Docker Use Layers because:
**Reusability**
If 10 images use Debian base:
Docker downloads it once
Reuses it everywhere
Saves disk space.

**Faster Builds (Caching)**
If we build:
FROM ubuntu
RUN apt update
COPY app.py .
If we change only app.py:
Docker reuses cached layers
Only rebuilds last layer
Much faster builds.

**Faster Pulls**
If server already has base layers:
Docker only downloads missing layers

**Storage Efficiency**
Layers are shared across images.
Example:
nginx
ubuntu
your custom app

All may share common base layers.
