# Install Prometheus on kubernetes Cluster using Helm Chart
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus --namespace prometheus
