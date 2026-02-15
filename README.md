# Firefly III Quadlet

This repository includes the different resources to run a Firefly III instance in a container using Podman Quadlet.
The Firefly III instance and its PostgreSQL database is running within a Pod.

## How to use

Before starting, take time to read carefully the [Firefly III Documentation](https://docs.firefly-iii.org/how-to/firefly-iii/installation/docker/)

The first step is to check and update the secret or environment.
In the case of Firefly 3 secrets need to be defined:
- fireflyiii-app-key: app key
- fireflyiii-db-secret: PostgreSQL database password
- fireflyiii-cron-token: Token for cron jobs 

Create secret with `podman secret create fireflyiii-SECRETTOSET SECRETVALUE/FILEWITHSECRETVALUE`. Replace `SECRETTOSET` and `SECRETVALUE/FILEWITHSECRETVALUE` for each secret mentioned above.

Then, check quadlet file in the quadlet folder. Check that port, volume and environment are compatible with the current setup. From this folder copy all quadlet file to `~/.config/containers/systemd/`.
One can use the `../install_quadlet` script to perform these actions. If the script is run by `sudo` it will install as rootfull containers.

Finally run the systemd command to start the Pod `systemctl --user start fireflyiii-pod` and check that Firefly III application and database are correctly running `systemctl --user status fireflyiii` and `systemctl --user status fireflyiii-db`.

If everything goes well, then Firefly III can be accessed on [http://localhost:7777/](http://localhost:7777/).
