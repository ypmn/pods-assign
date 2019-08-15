IF already one pods is running with label env=test the pod affinity will schedule the new pod on the same sever
which should contain the topologyKey(ex: server: test , here tolology key is server) in node the label 
Anti Pod affinity is if some pods is already running with label env=dev the new pod won't schedule on the node 
and the node also conatin the tolopologyKey(ex: server: test , here tolology key is server) server 
