ginowen-deployment.yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: ginowen-deployment
  spec:
    replicas: 3
    selector:
      matchLabels:
        app: ginowen
    template:
      metadata:
        labels:
          app: ginowen
      spec:
        containers:
        - name: ginowen
          image: xxxxx/owen:1.0   #最好用阿里云或者dockerhub
          imagePullPolicy: IfNotPresent
          ports:
          - containerPort: 6789

ginowen-service.yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: ginowen-service
  spec:
    selector:
      app: ginowen  # 选择带有 app=redis 标签的 Pod
    ports:
      - protocol: TCP
        port: 6789  # 服务端口
        targetPort: 6789  # 容器内的端口
        nodePort: 30789  # 外部访问的端口
    type: NodePort  # 默认为 ClusterIP，可以改为 LoadBalancer 或 NodePort




kubectl apply -f ginowen-deployment.yaml
kubectl apply -f ginowen-service.yaml


即可
