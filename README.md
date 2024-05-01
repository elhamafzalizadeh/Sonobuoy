# Sonobuoy

Sonobuoy is a conformance testing tool that makes it simpler to understand the condition of a Kubernetes cluster by running a variety of configuration tests in an accessible and non-destructive manner. The plugins include the Kubernetes conformance tests and it provides customizable, extendable, and cluster-agnostic reporting for your Kubernetes.
This tool is used for cluster owners to ensure their Kubernetes cluster follows CNCF guidelines through these test use cases.

 * 1-Integrated end-to-end conformance testing of Kubernetes.

 * 2-Workload debugging.

 * 3-Custom data collection through extensible plugins.


# Steps:

 * 1-Installing Sonobuoy
 * 2-Running sonobuoy
 * 3-get test results


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

It takes about 80 minutes to complete.(About 369 test cases in this mode)




