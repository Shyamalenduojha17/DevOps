# Component Of Manifest File:
  ### There are 4 Main Component of Manifest File. Such as:
                   * API-Verion
                   * Kind
                   * Metadata
                   * Spec
## 1. [API-Version](https://blog.knoldus.com/what-is-apiversion-in-kubernetes-part-1/#:~:text=Kubernetes%20apiVersion,-When%20we%20create&text=The%20format%20of%20the%20apiVersion,a%20new%20apiVersion%20is%20created.) :
   ###   An object definition in Kubernetes requires a apiVersion field. When Kubernetes has a release that updates what is available for you to use—changes something in its API—a new apiVersion is created. The format of the apiVersion is api_group/version.
## 2. [Kind](https://kodekloud.com/blog/kubernetes-objects/#) :
   ###   Kind/Objects are sort of like blueprints. They provide detailed instructions to Kubernetes on how the applications must be set up and managed. 
 For example, a Deployment object might specify that you want three replicas (copies) of some application running at all times, while a Service object might define how you want to expose your application to the internet. Kubernetes then takes these instructions and automatically configures and manages the application accordingly, ensuring that it always matches the desired state.
