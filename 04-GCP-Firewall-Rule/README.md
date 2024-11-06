# Create a GCP Firewall Rule to enable K8s Service NodePort Access from Internet.



### Search "Firewall Rule -> VPC" 

### Name : k8s-svc 
### Tag  : k8s-svc 
### Source : 0.0.0.0/0
### Protocol: TCP
### Port Range: 30000-32767


## Now Edit the nodes & add the "k8s-svc" tag in firewall section 
