<body>
    <h1>Backend-Frontend Kubernetes Deployment</h1>
    <p>This project demonstrates deploying a simple backend and frontend application using Kubernetes.</p>
    <h2>Project Overview</h2>
    <ul>
        <li><strong>Backend:</strong> A simple .NET application that listens on a port and returns responses.</li>
        <li><strong>Frontend:</strong> A web page that makes requests to the backend.</li>
        <li><strong>NGINX:</strong> Acts as a reverse proxy for frontend-backend communication.</li>
        <li><strong>Kubernetes:</strong> Used for container orchestration and service management.</li>
    </ul>
    <h2>Setup and Deployment</h2>
    <h3>1. Clone the repository</h3>
    <pre><code>git clone https://github.com/GeorgeD615/GridCloudSeminarTask2.git</code></pre>
    <h3>2. Navigate to the project folder</h3>
    <pre><code>cd ../GridCloudSeminarTask2</code></pre>
    <h3>3. Start Minikube</h3>
    <pre><code>minikube start --driver=docker</code></pre>
    <h3>4. Build and load Docker images into Minikube</h3>
    <pre><code>
docker build -t backend-app:latest ./API
docker build -t nginx-proxy:latest ./k8s/nginx
minikube image load backend-app:latest
minikube image load nginx-proxy:latest
    </code></pre>
    <h3>5. Apply Kubernetes configurations</h3>
    <pre><code>
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/backend-service.yaml
kubectl apply -f k8s/nginx.yaml
    </code></pre>
    <h3>6. Check if all pods and services are running</h3>
    <pre><code>
kubectl get pods
kubectl get services
    </code></pre>
    <h3>7. Expose NGINX service</h3>
    <pre><code>minikube service nginx-service --url</code></pre>
    <h2>Testing the Deployment</h2>
    <ul>
        <li>Open the URL provided by <code>minikube service nginx-service --url</code> in a browser.</li>
        <li>Click the button to request a random number from the backend.</li>
        <li>If everything is set up correctly, a random number should appear.</li>
    </ul>
    <h2>Cleaning Up</h2>
    <pre><code>
kubectl delete -f k8s/backend-deployment.yaml
kubectl delete -f k8s/backend-service.yaml
kubectl delete -f k8s/nginx.yaml
minikube stop
minikube delete
    </code></pre>
    <p>Now your backend and frontend are running in Kubernetes, accessible through NGINX.</p>
</body>
