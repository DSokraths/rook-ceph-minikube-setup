Steps: 

1. - VB=> Create Volume
2. - git clone --single-branch --branch v1.14.9 https://github.com/rook/rook.git
3. - cd rook/deploy/examples
4. - rook/deploy/examples/operator.yaml : set ROOK_ENABLE_DISCOVERY_DAEMON: "true"
					  + change ports CSI_RBD_GRPC_METRICS_PORT: "9092"
5. - rook/deploy/examples/cluster.yaml  : uncomment provider = host
6. - inside cluster.yaml : 		  + change mon count to 1.
7. - kubectl apply -f operator.yaml
8. - kubectl apply -f crds common cluster-test
9. - kubectl delete -f cluster.yaml 
10.- kubectl delete -f operator.yaml 


After Installation : 

1. kubectl get pods -n rook-ceph -l app=rook-ceph-mgr : find the dashboard pod
2. kubectl port-forward -n rook-ceph pod/rook-ceph-mgr-a-6b7f4f4bb4-rf5pt 7000:7000 
3. kubectl -n rook-ceph get secret rook-ceph-dashboard-password -o jsonpath="{['data']['password']}" | base64 --decode && echo
4. exec at build tools pod: ceph status , ceph osd status





