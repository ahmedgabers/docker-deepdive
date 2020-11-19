# Security

- Kernel namespaces

- Control groups

- Linux Capabilities

- Image Scanning


---

## Image Scanning

- Checking the software packages, binaries, libraries, operative system files and more
against well known vulnerabilities databases.

- Analyzing the Dockerfile and image metadata to detect security sensitive configurations
like running as privileged (root) user, exposing insecure ports

- User defined policies

- Integrate Scanning into CI/CD

---

class: pic
## Open Source Docker Scanning Tool: Anchore Engine

![anchore](images/anchore_engine_architecture.png)

---

class: extra-details

- API Service: Central communication interface that can be accessed by code, using a
REST API, or directly, using the command line.

-  Image Analyzer Service: Executed by the “worker”, these Anchore nodes perform the
actual Docker image scanning.

- Catalog Service: Internal database and system state service.

- Queuing Service: Organizes, persists and schedules the engine tasks.

- Policy Engine Service: Policy evaluation and vulnerabilities matching rules.

- Kubernetes Webhook Service: Kubernetes-specific webhook service to validate images
before they are spawned.

---

## Installation

- Deploy [Anchore Engine](https://github.com/anchore/anchore-engine) using docker-compose:

```yaml
curl https://docs.anchore.com/current/docs/engine/quickstart/docker-compose.yaml > docker-compose.yaml
docker-compose up -d
```
---

## Installation

- Install the [CLI client](https://github.com/anchore/anchore-cli)

```yaml
apt-get update
apt-get install python-pip
pip install anchorecli
```

- Export credentials

```yaml
export ANCHORE_CLI_URL=http://localhost:8228/v1
export ANCHORE_CLI_USER=admin
export ANCHORE_CLI_PASS=foobar
```
---

## Integrate Image Scanning in CI/CD

![dockercicd](docker_scanner_with_jenkins.png)

---

class: extra-details

- In a typical workflow, this container image is then run through some automated testing. 

- If an image does not pass the Docker security scanning (doesn’t meet the organization’s requirements for security or compliance) then it doesn’t make sense to invest the time required to perform automated tests on the image. 

- A better approach is to fail the build and returning the appropriate reports back to the developer to address the issues..

---

## Runtime Security

- [Falco Project](https://falco.org/docs/)

- [Palo Alto: Prisma Cloud](https://www.paloaltonetworks.com/prisma/cloud)

- [Sysdig](https://sysdig.com/products/secure/runtime-security/)

