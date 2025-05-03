### 설치 절차

1. **CSI HostPath 드라이버 클론**

    ```bash
    git clone https://github.com/kubernetes-csi/csi-driver-host-path.git
    cd csi-driver-host-path/deploy/kubernetes-latest
    
    ```

2. **Snapshot Controller 버전 지정**

    ```bash
    export SNAPSHOTTER_VERSION=v2.0.1
    
    ```

3. **RBAC 리소스 적용**

    ```bash
    kubectl apply -f \
    https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/${SNAPSHOTTER_VERSION}/deploy/kubernetes/snapshot-controller/rbac-snapshot-controller.yaml
    ```

4. **Snapshot Controller 적용**

    ```bash
    kubectl apply -f \
    https://raw.githubusercontent.com/kubernetes-csi/external-snapshotter/${SNAPSHOTTER_VERSION}/deploy/kubernetes/snapshot-controller/setup-snapshot-controller.yaml
    ```

5. **CSI HostPath 드라이버 설치**

```bash
git clone https://github.com/kubernetes-csi/csi-driver-host-path.git
cd csi-driver-host-path/deploy/kubernetes-latest

./deploy.sh
kubectl get pods -o wide | grep csi
```

✅ 예시 출력:

```
csi-hostpathplugin-0     8/8   Running   1     ...   k8s-node1
snapshot-controller-0    1/1   Running   0     ...   k8s-node2

```

**6. StorageClass 작성 및 적용**