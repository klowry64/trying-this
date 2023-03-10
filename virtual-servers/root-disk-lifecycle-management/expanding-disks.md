# Expanding Disks

A Virtual Server root or additional block disk can be instantly expanded from [cloud.coreweave.com](https://cloud.coreweave.com) in the Virtual Server upgrade page, from the volume namangement page and using the CLI with `kubectl`. Expansion of volumes are instant, however the VM needs to be restarted to detect the larger disk size. A shared filesystem volume can be expanded without restart.

![Expand root disk with Virtual Server Upgrade](<../../.gitbook/assets/Screen Shot 2022-05-25 at 4.32.05 PM.png>)

#### Expand with kubectl

1. Increase the disk size. Specify the total size you want the disk to be: `kubectl patch pvc myVS -p '{"spec":{"resources":{"requests":{"storage": "500Gi"}}}}'`
2. Restart the VM, either via the [Cloud UI](https://apps.coreweave.com) or with [virtctl](../remote-access-and-control.md#installing-virtctl): `virtctl restart myVS`. Please note that rebooting from inside the VM is not enough.
3. If you are using a CoreWeave provided base image, the system should come up with the partition and filesystem expanded. If not, you might need to manually grow it on linux: `sudo resize2fs /dev/vda1`. In Windows disks can be resized using the "Disk Management" tool.
