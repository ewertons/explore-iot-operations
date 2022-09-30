# auth-server-template

This example is a template server for E4K broker custom authentication. Custom authentication allows a third-party server to decide whether to authenticate connecting MQTT clients. The server template provided here can be used as a starting point for implementing the authentication logic.

## Deploying the template

The template server needs to be built and deployed as a Kubernetes service. You will need to provide the repository for hosting its container image.

1. Run the [build_image.sh](deploy/build_image.sh) script and pass the image tag to use. This script builds and pushes the template image.

```sh
IMAGE_TAG=example.example.io/auth-server-template:latest ./deploy/build_image.sh
```

2. Run the [make_credentials.sh](deploy/make_credentials.sh) script to generate server credentials for the template. This script generates test certificates and saves them as Kubernetes secrets.

```sh
./deploy/make_credentials.sh
```

3. Edit [auth-server-template.yaml](deploy/auth-server-template.yaml#L10) and set the image that you created in step 1.

4. Deploy the pod and service for the template.

```sh
kubectl apply -f ./deploy/auth-server-template.yaml
```

5. When finished, run [cleanup.sh](deploy/cleanup.sh) to delete resources.
