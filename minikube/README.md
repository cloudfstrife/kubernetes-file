# README

## 安装kvm2

```text
sudo apt install qemu-system libvirt-daemon-system
```

## 添加用户组

```text
sudo usermod -aG $USER libvirt-qemu
sudo adduser $USER libvirt
```

## 增加 `devices` 支持

编辑 `/etc/default/grub`

```text
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on systemd.unified_cgroup_hierarchy=0"
```

更新 grub

```text
sudo grub-mkconfig -o /boot/grub/grub.cfg 
```

## 重启并验证

```text
virt-host-validate
```

## 设置 KVM 为默认驱动

```text
minikube config set driver kvm2
```

## 启动集群

```text
minikube start --driver=kvm2 \
--cache-images=true \
--image-mirror-country=cn \
--delete-on-failure=true \
--image-repository=registry.cn-hangzhou.aliyuncs.com/google_containers \
--nodes=3 \
--addons=[dashboard,metrics-server,ingress,ingress-dns,csi-hostpath-driver] \
-v=8
```

## 删除

```text
minikube delete --all
```