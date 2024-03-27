# LINSTOR demo

```
talosctl gen secrets
```

```
talosctl gen config demo https://10.0.100.206:6443 \
    --config-patch-control-plane @patch-master.yaml \
    --config-patch-worker @patch-worker.yaml \
    --with-secrets secrets.yaml
```

```
t apply-config -n 10.0.100.206 -f controlplane.yaml --insecure
```

```
t -e 10.0.100.201 -n 10.0.100.201 disks --insecure 
```

```
t -e 10.0.100.201 -n 10.0.100.201 get kernelmodulespecs.runtime.talos.dev 
```

```
t bootstrap -e 10.0.100.206 -n 10.0.100.206 
```

```
t kubeconfig demo.conf -e 10.0.100.206 -n 10.0.100.206 
```

```
helm pull cilium/cilium --untar
```

```
helm install \
    cilium \
    cilium/cilium \
    --version 1.15.2 \
    --namespace kube-system \
    --set ipam.mode=kubernetes \
    --set=kubeProxyReplacement=true \
    --set=securityContext.capabilities.ciliumAgent="{CHOWN,KILL,NET_ADMIN,NET_RAW,IPC_LOCK,SYS_ADMIN,SYS_RESOURCE,DAC_OVERRIDE,FOWNER,SETGID,SETUID}" \
    --set=securityContext.capabilities.cleanCiliumState="{NET_ADMIN,SYS_ADMIN,SYS_RESOURCE}" \
    --set=cgroup.autoMount.enabled=false \
    --set=cgroup.hostRoot=/sys/fs/cgroup \
    --set=k8sServiceHost=localhost \
    --set=k8sServicePort=7445
```

```
task get-piraeus
```

```
task ns
```

```
helm install piraeus-operator ./piraeus -n piraeus-datastore --set=installCRDs=true
```

```
task generate-tls
```

```
task linstor
```

```
k apply -f linstor/sc.yaml 
```

