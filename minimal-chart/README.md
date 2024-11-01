
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


repositories.yaml
apiVersion: v1
repositories:
  - name: snapshots
    url: http://172.17.0.2:8081/repository/helm-snapshots
    username: admin
    password: admin123
