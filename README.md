# kindk8s-oai

config maps and deployments of 5G-NR OAI in k8s 

## Quickstart

1. Generate open5gs and webui base image, as detailed [here](http://github.com/jnunyez/build-open5gs).
	
	- Images are also publicly available, download them from:

		```console
    	podman pull quay.io/jnunez/open5gs
    	podman pull quay.io/jnunez/webui
		```

2. Build the OAI gNodeB image. The repo to build this image is available in [here](http://github.com/jnunyez/build-oai). 
	- Image is available now, download it from:

		```console
    	podman pull quay.io/jnunez/oai_gnb
		```
3. Unit test of gNodeB image on k8s over baremetal cluster. Due to the HW dependencies we conduct the experiments on k8s over baremetal. 
	- Deploy 1 node cluster using kubeadm.
                
		```console
		deploy-kubeadm-cluster
		
		
		
4. Deploy open5gs and prerequisites in k8s. The manifests and detailed instructions for deploying open5gs in k8s are available [here](https://github.com/jnunyez/kindk8s-open5gs). Assure that all open5gs pods are running properly.

5. Assure the 5G-Core has registered the subscriber profiles planned to be subsequently used with the 5G-NR simulator. 
	
	- SIM provisioning can be done manually by opening the webui dashboard. The `webui` service is externally accessible using a NodePort to the default port in the app (i.e., port 3000). See screenshot of webui dashboard below:

		![Subscriber](./images/webui.png?raw=true)

	- Automated SIM provisioning (**TBA**)

6. Deploy a 5G gNB that attaches to the AMF and subsequently a 5G UE that will attach to the gNB. 

	- The UE must be already subscribed in the UDM as detailed in step 5.
 
	- Run the oai gnb deployment:

   		```console
   		deploy-oai-gnb
   		```

## ToDo

- image works on k8s, we use real cluster instead
- deploy OAI using O-RAN 7.2 in k8s over baremetal
