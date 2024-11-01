# Helm Chart Packaging and Pushing

This guide provides step-by-step instructions on how to package and push a Helm chart using Docker.

## Prerequisites

Before you begin, ensure that you have the following:

- Docker installed on your system.
- A minimal Helm chart located in `/home/user/minimal-chart`.
- A configuration file for Helm repositories located at `/home/user/.config/helm/repositories.yaml`.

## Step 1: Prepare the Output Directory

First, create the output directory where the packaged chart will be stored:

```bash
mkdir -p /home/user/output
chmod 777 /home/user/output

docker run -it --rm \
  -v /home/user/minimal-chart:/charts \
  -v /home/user/.config/helm/repositories.yaml:/config/repositories.yaml \
  -v /home/user/output:/apps \
  alpine/helm package /charts


docker run -it --rm \
  -v /home/user/output:/apps \
  -v /home/user/.config/helm/repositories.yaml:/config/repositories.yaml \
  alpine/helm push /apps/minimal-chart-0.1.0.tgz oci://172.17.0.2:8081/repository/helm-snapshots --repository-config /config/repositories.yaml


apiVersion: v1
repositories:
  - name: snapshots
    url: http://172.17.0.2:8081/repository/helm-snapshots
    username: admin
    password: admin123



This structured format clearly outlines each step in a numbered format, making it easier for users to follow the instructions. You can save this content as `README.md` for your project.
