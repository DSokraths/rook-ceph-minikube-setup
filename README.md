Steps: 

1. - VB=> Create Raw Volume
2. - cd rook/deploy/examples
3. - rook/deploy/examples/operator.yaml :
        - a. set ROOK_ENABLE_DISCOVERY_DAEMON: "true"
        - b. change ports CSI_RBD_GRPC_METRICS_PORT: "9092"
     
4. - rook/deploy/examples/cluster.yaml  :
        - a. uncomment provider = host
        - b. change mon count to 1.
     
5. - kubectl apply -f operator.yaml
6. - kubectl apply -f crds common cluster-test
7. - kubectl delete -f cluster.yaml 
8. - kubectl delete -f operator.yaml 


After Installation : 

1. - kubectl get pods -n rook-ceph -l app=rook-ceph-mgr : find the dashboard pod
2. - kubectl port-forward -n rook-ceph pod/rook-ceph-mgr-a-6b7f4f4bb4-rf5pt 7000:7000 
3. - kubectl -n rook-ceph get secret rook-ceph-dashboard-password -o jsonpath="{['data']['password']}" | base64 --decode && echo
4. - exec at build tools pod: ceph status , ceph osd status





