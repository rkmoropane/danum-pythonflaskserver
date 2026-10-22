# coding-project-template

# 🚀 Deploying Your First Application on Code Engine Using Python

> **Lab:** Deploying your first application on Code Engine using Python  
> **Estimated time:** 15 minutes  
> **Platform:** IBM Cloud Code Engine  
> **Application:** Hello World (Flask)  
> **Source repository:** [danum-pythonflaskserver](https://github.com/ibm-developer-skills-network/danum-pythonflaskserver)

---

## 📌 Overview

In this lab, you will deploy a simple Python Flask web application from GitHub to **IBM Cloud Code Engine**. The application exposes an endpoint at the root URL (`/`) and returns the text `Hello World`.

Code Engine creates and manages the infrastructure needed to run the application, then provides a URL that you can use to access it remotely.

## 🎯 Learning Objectives

By the end of this lab, you will be able to:

- Start Code Engine and create a project.
- Open the preconfigured Code Engine CLI.
- List applications deployed to Code Engine.
- Deploy a Python Flask application from a GitHub repository.
- Access the deployed application using its generated URL.
- Retrieve details about a deployed application.

## 🧰 Prerequisites

- Access to the provided IBM Cloud lab environment.
- The lab's Code Engine environment and CLI.
- The lab-provided registry namespace and registry secret.

> **Note:** The commands below are intended for the preconfigured lab environment. Values such as `${SN_ICR_NAMESPACE}` are supplied by that environment.

---

## 1. Set Up Code Engine

1. In the lab environment menu, open **Cloud**.
2. Select **Code Engine**.
3. In the Code Engine setup panel, click **Create Project**.
4. Wait while the environment is prepared. A progress indicator appears in the setup panel.
5. When setup is complete and Code Engine is active, click **Code Engine CLI**.
6. Use the terminal that opens below the panel. The lab preconfigures the CLI, sets the working directory, creates the project, and configures Kubeconfig.

---

## 2. List Existing Applications

Before deploying the application, list the applications that already exist in the current Code Engine project.

Run:

```bash
ibmcloud code-engine application list
```

The shorter alias is also available:

```bash
ibmcloud ce app list
```

If this is your first time running the lab, the list should contain no applications.

---

## 3. Deploy the Hello World Application

The lab uses a Python Flask application from this GitHub repository:

- **Repository:** [https://github.com/ibm-developer-skills-network/danum-pythonflaskserver](https://github.com/ibm-developer-skills-network/danum-pythonflaskserver)
- **Application name:** `helloworld`
- **Application port:** `5000`

Run the following command in the Code Engine CLI:

```bash
ibmcloud ce application create --name helloworld --build-source https://github.com/ibm-developer-skills-network/danum-pythonflaskserver --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld --registry-secret icr-secret --port 5000
```

### What the command does

| Option | Purpose |
|---|---|
| `application create` | Creates and deploys a Code Engine application. |
| `--name helloworld` | Names the application `helloworld`. |
| `--build-source` | Specifies the GitHub repository containing the source code. |
| `--image` | Specifies the container image destination in IBM Cloud Container Registry. |
| `--registry-secret icr-secret` | Uses the lab-provided registry secret. |
| `--port 5000` | Configures the application to listen on port `5000`. |

Code Engine builds and deploys the application and sets up the required infrastructure. Wait for the command to finish. The CLI should confirm creation and provide a URL for the application.

---

## 4. Open the Deployed Application

1. Find the URL printed after the deployment completes.
2. Open it by holding **Ctrl** (Windows/Linux) or **Cmd** (Mac) while clicking the link, or copy and paste the URL into a browser.
3. Confirm that the page displays:

```text
Hello World
```

This verifies that the deployed Flask application is reachable through its generated URL.

---

## 5. Inspect the Application Details

To view information about the deployed application, run:

```bash
ibmcloud ce app get --name helloworld
```

The output provides details about the application, including information such as its creation time, resources used, and number of instances.

---

## 6. Completion Checklist

Use this checklist to track your progress:

- [ ] Opened **Cloud → Code Engine**.
- [ ] Created a Code Engine project and waited for setup to finish.
- [ ] Started the **Code Engine CLI**.
- [ ] Listed the applications in the project.
- [ ] Deployed the `helloworld` application from GitHub.
- [ ] Opened the generated application URL.
- [ ] Confirmed that the page returned `Hello World`.
- [ ] Retrieved the application details using `ibmcloud ce app get`.

## 🧠 Key Takeaways

- IBM Cloud Code Engine can build and deploy an application from source code in a GitHub repository.
- The Code Engine CLI provides commands to list, create, and inspect applications.
- The deployment command specifies the application name, source repository, image destination, registry secret, and port.
- After deployment, Code Engine provides a URL for remote access.
- The `ibmcloud ce app get` command displays details about a deployed application.

## 🗂️ Commands Quick Reference

```bash
# List applications
ibmcloud code-engine application list

# Short alias for listing applications
ibmcloud ce app list

# Create and deploy the Hello World application
ibmcloud ce application create --name helloworld --build-source https://github.com/ibm-developer-skills-network/danum-pythonflaskserver --image us.icr.io/${SN_ICR_NAMESPACE}/helloworld --registry-secret icr-secret --port 5000

# Get application details
ibmcloud ce app get --name helloworld
```

---

## ✅ Lab Result

You have completed the lab when the `helloworld` application is deployed on Code Engine, its generated URL opens successfully, and the page displays `Hello World`.

**Original lab author:** Lavanya T S
