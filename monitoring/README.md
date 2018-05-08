# Kubernetes monitoring in less than 5 minutes

Kubelet natively exposes cadvisor metrics at https://kubernetes.default.svc:443/api/v1/nodes/<node-name>/proxy/metrics/cadvisor and we can use a prometheus server to scrape this endpoint. These metrics can then be visualized using Grafana.

Setup:
0. If you have not already deployed the nginx-ingress then - Comment out statement 191 to 210 - Uncomment statement 183 or 184 depending upon your cluster setup.
0. Deployment: kubectl deploy -f k8s/monitoring/monitoring.yaml
0. Once grafana is running:
 	- Access grafana at monitoring.yourdomain.com/grafana in case of Ingress or http://:3000 in case of type: LoadBalancer
 	- Add DataSource: 
 	  - Name: DS_PROMETHEUS - Type: Prometheus 
 	  - URL: http://prometheus-service:8080 
 	  - Save and Test 0. You can now build your custon dashboards or simply import dashboards from grafana.net. Dasboard #315 and #1471 are good to start with.

Note:
0. A Cluster-binding role is already being created by the config. The role currently as admin permissions, however you can modify it to a viewer role only.