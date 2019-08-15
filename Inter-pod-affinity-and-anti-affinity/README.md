IF already one pods is running with label env=test the pod affinity will schedule the new pod on the same sever
which should contain the topologyKey(ex: server: test , here tolology key is server) in node the label 
Anti Pod affinity is if some pods is already running with label env=dev the new pod won't schedule on the node 
and the node also conatin the tolopologyKey(ex: server: test , here tolology key is server) server 


    apiVersion: v1
    kind: Pod
    metadata:
      name: with-pod-affinity
    spec:
      affinity:
        podAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: env
                operator: In
                values:
                - test
            topologyKey: server
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            podAffinityTerm:
              labelSelector:
                matchExpressions:
                - key: env
                  operator: In
                  values:
                  - dev
              topologyKey: server
      containers:
      - name: with-pod-affinity
        image: k8s.gcr.io/pause:2.0

