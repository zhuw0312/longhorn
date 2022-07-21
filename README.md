# longhorn
A container runtime compatible with Kubernetes (Docker v1.13+, containerd v1.3.7+, etc.)
Kubernetes v1.18+.
open-iscsi is installed, and the iscsid daemon is running on all the nodes. This is necessary, since Longhorn relies on iscsiadm on the host to provide persistent volumes to Kubernetes. For help installing open-iscsi, refer to this section.
RWX support requires that each node has a NFSv4 client installed.
For installing a NFSv4 client, refer to this section.
The host filesystem supports the file extents feature to store the data. Currently we support:
ext4
XFS
bash, curl, findmnt, grep, awk, blkid, lsblk must be installed.
Mount propagation must be enabled.

yum --setopt=tsflags=noscripts install iscsi-initiator-utils -y 
yum install jq -y 

systemctl enable --now iscsid 

# delete
kubectl create -f https://raw.githubusercontent.com/longhorn/longhorn/v1.3.0/uninstall/uninstall.yaml
kubectl delete -f https://raw.githubusercontent.com/longhorn/longhorn/v1.3.0/deploy/longhorn.yaml
kubectl delete -f https://raw.githubusercontent.com/longhorn/longhorn/v1.3.0/uninstall/uninstall.yaml
# delete check
curl -s https://raw.githubusercontent.com/longhorn/longhorn/v0.8.1/scripts/cleanup.sh |bash -s v062
curl -s https://raw.githubusercontent.com/longhorn/longhorn/v0.8.1/scripts/cleanup.sh |bash -s v070
# kubectl get crd
NAME                                          CREATED AT
......
engineimages.longhorn.io                      2020-07-08T08:52:25Z
engines.longhorn.io                           2020-07-08T08:52:23Z
