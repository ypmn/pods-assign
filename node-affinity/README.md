  This node affinity rule says the pod can only be placed on a node with a label 
  whose key is server and whose value is either apps1 or apps2. 
  In addition, among nodes that meet that criteria, 
  nodes with a label whose key is server and whose value is apps2 should be preferred.
  
  
    apiVersion: v1
    kind: Pod
    metadata:
      name: with-node-affinity
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: server
                operator: In
                values:
                - apps1
                - apps2
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 1
            preference:
              matchExpressions:
              - key: server
                operator: In
                values:
                - apps2
      containers:
      - name: with-node-affinity
        image: k8s.gcr.io/pause:2.0
