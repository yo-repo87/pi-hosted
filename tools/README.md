## PLEASE NOTE ##


Most of the follwing scripts are only needed if you are trying to load one of these containers.  Please see table below for a recap of use cases.

---

| Script Name  | Additional Doc | Type | Description | wget install |
| ------------ | -------------- | ---- | ----------- | ------------ |
|[install_caddy.sh](../tools/install_caddy.sh)||Preinstall|Preinstall Setup for Caddy|wget -qO- https://git.io/JMsEe \| bash|
|[install_drupal.sh](../tools/install_drupal.sh)||Preinstall|Preinstall Setup for Drupal|wget -qO- https://git.io/JMsEj \| bash|
|[install_invidious.sh](../tools/install_invidious.sh)||Preinstall|Install Invidious|wget -qO- https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/tools/install_invidious.sh \| bash|
|[install_photoprism.sh](../tools/install_photoprism.sh)|[Documentation](../docs/photoprism.md)|Preinstall|Install Photo Prism|wget -qO- https://git.io/JM5Tr \| bash|
|[install_portainer_agent.sh](../tools/install_portainer_agent.sh)||Preinstall|Install Portainer Agent<br>Portainer agent is used for remote management of the host you install it on.||
|[install_reactive-resume.sh](../tools/install_reactive-resume.sh)|[Documentation](../docs/reactive-resume_installation.md)|Preinstall|Install Reactive-Resume|wget -qO- https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/tools/install_reactive-resume.sh \| bash|
|[install_throttled.sh](../tools/install_throttled.sh)|[Documentation](../docs/throttled.md)|Install|Preinstall Setup for the Throttled Script|wget -qO- https://git.io/JXzw0 \| bash|
|[install_vikunja.sh](../tools/install_vikunja.sh)||Preinstall|Preinstall Setup for Vikunja|wget -qO- https://git.io/JMsuZ \| bash|
|[install_whoogle.sh](../tools/install_whoogle.sh)||Preinstall|Install Whoogle|wget -qO- https://raw.githubusercontent.com/pi-hosted/pi-hosted/master/tools/install_whoogle.sh \| bash|
|[nginx-proxy-manager.sh](../tools/nginx-proxy-manager.sh)|[Documentation](../docs/nginx_proxy_manager.md)|Preinstall|Preinstall Setup for NPM|wget -qO- https://git.io/JPXF5 \| bash|
|[reset_premissions_nextcloud.sh](../tools/reset_premissions_nextcloud.sh)||Extra|Basic Script to reset the premissions of NextcloudPi|wget -qO- https://git.io/JDklN \| bash|
|[rpi_docker_monitor.sh](../tools/rpi_docker_monitor.sh)|[Documentation](../docs/rpi_docker_monitor.md)|Preinstall|Preinstall Setup for Docker Monitor|wget -qO- https://git.io/JPXba \| bash|
|[traefik.sh](../tools/traefik.sh)||Preinstall|Preinstall Setup for Traefik|wget -qO- https://git.io/JMsuA \| bash|
|[unpoller-install.sh](../tools/unpoller-install.sh)|[Documentation](../docs/UnPoller-Monitor.md)|Preinstall|Preinstall Setup for UnPoller|wget -qO- https://git.io/JMszE \| bash|
|[update_libseccomp2.sh](../tools/update_libseccomp2.sh)||Update|PI OS 32 libseccomp2 Repair utility|wget -qO- https://git.io/JPXdj \| bash|
|[update_portainer_agent.sh](../tools/update_portainer_agent.sh)||Update|Upgrade Portainer Agent||

## Helix OS catalog variant

`convert_to_helix.py` rewrites a Portainer app template so its host folders fit
[Helix OS](https://github.com/yo-repo87/helix-os) (shares under `/mnt/user`) instead of the
Raspberry Pi `/portainer/...` layout:

| Pi-Hosted path | Helix path |
|---|---|
| `/portainer/Files/AppData/Config/<app>` (and `/portainer/Files/<x>`) | `/mnt/user/appdata/<app>` |
| `/portainer/Downloads`, `/portainer/Files/Downloads` | `/mnt/user/downloads` |
| `/portainer/{TV,Movies,Music,Podcasts,Books,Comics,Pictures}` | `/mnt/user/media/<Name>` |

System paths (`/etc/localtime`, `/var/run/docker.sock`, `/dev/*`) and named volumes are untouched.

Generated files (use them as a template URL in Helix, or any Portainer-compatible tool):

- `template/portainer-v3-amd64-helix.json`
- `template/portainer-v3-arm64-helix.json`

Regenerate after the upstream catalog changes:

```bash
for a in amd64 arm64; do
  python3 tools/convert_to_helix.py --in template/portainer-v3-$a.json --out template/portainer-v3-$a-helix.json
done
```
