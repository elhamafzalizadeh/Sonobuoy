# Sonobuoy

Sonobuoy is a conformance testing tool that makes it simpler to understand the condition of a Kubernetes cluster by running a variety of configuration tests in an accessible and non-destructive manner. The plugins include the Kubernetes conformance tests and it provides customizable, extendable, and cluster-agnostic reporting for your Kubernetes.
This tool is used for cluster owners to ensure their Kubernetes cluster follows CNCF guidelines through these test use cases.

 * 1-Integrated end-to-end conformance testing of Kubernetes.

 * 2-Workload debugging.

 * 3-Custom data collection through extensible plugins.


# Steps:

 * 1-Installing Sonobuoy
 * 2-Running Sonobuoy
 * 3-Test Results


## 1-Installing Sonobuoy

For installing gatekeeper follow these steps:

### Download the latest release

Download the latest release from https://github.com/vmware-tanzu/sonobuoy/releases

### Extract

```
tar -xvf <RELEASE_NAME>.tar.gz

sudo mv sonobuoy /usr/local/bin/

```

## 2-Running Sonobuoy

Use the following command to check the status of each of the plugins.

```
sudo sonobuoy run --wait --mode quick

```

### Test Modes

For running the main tests,we should review the test modes for running the e2e plugin. Valid modes are [certified-conformance conformance-lite non-disruptive-conformance quick]. (default:non-disruptive-conformance)


### Main Test

```
sudo sonobuoy run -m non-disruptive-conformance

```

### Check Logs

```
 sudo kubectl get logs -f sonobuoy -n sonobuoy

```

It takes about 80 minutes to complete.(About 369 test cases)

### Check Passed & Failed count during the test

```
 sudo sonobuoy status

```

## 3-Test Results

```
sudo sonobuoy retrieve

```

You can see the result file.(like 202308051043_sonobuoy_b8662f33-b4b8-4182-90a0-e7dd343a43a8.tar.gz)

### Check the result of test after completing.

```
sudo sonobuoy results <RESULT_FILE>.tar.gz

```

### Stop the Sonobuoy test

```
sudo sonobuoy delete

```

# Pulling Sonobuoy Images from a Private Repository

Create a yaml file like: custom-repo.config.yaml

```yaml
buildImageRegistry: <PRIVATE-REGISTRY>/build-image
dockerGluster: <PRIVATE-REGISTRY>/gluster
dockerLibraryRegistry: <PRIVATE-REGISTRY>/library
e2eRegistry: <PRIVATE-REGISTRY>/kubernetes-e2e-test-images
e2eVolumeRegistry: <PRIVATE-REGISTRY>/kubernetes-e2e-test-images/volume
gcRegistry: <PRIVATE-REGISTRY>
gcEtcdRegistry: <PRIVATE-REGISTRY>
promoterE2eRegistry: <PRIVATE-REGISTRY>/e2e-test-images
sigStorageRegistry: <PRIVATE-REGISTRY>/sig-storage

### Run the test with private registry

```
sudo sonobuoy run -m non-disruptive-conformance --e2e-repo-config custom-repo.config.yaml  --sonobuoy-image <PRIVATE-REGISTRY>/sonobuoy/sonobuoy:v0.56.16  --kube-conformance-image <PRIVATE-REGISTRY>/conformance:v1.26.1 --systemd-logs-image  <PRIVATE-REGISTRY>/sonobuoy/systemd-logs:v0.4

```

