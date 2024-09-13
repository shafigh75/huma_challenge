# 🚢 Welcome to **Huma Docker Swarm Setup** 🌊

This guide will walk you through the steps I took to set up a Docker Swarm cluster, push my services to a local Docker registry, and deploy them using Docker Swarm. 

---

## 🛠️ **Step 1: Setting Up My Local Docker Registry**

Before I can deploy my services, I'll need a place to store my Docker images. Let's start by creating a **local Docker registry**.

```bash
docker service create --name registry --publish published=5000,target=5000 registry:2
```

This command creates a Docker service running a local registry on port `5000`, allowing us to store and retrieve images locally. It’s like your personal Docker Hub but cozier. 😎

---

## 🛳️ **Step 2: Build & Push My Docker Images**

Now that my local registry is set up, it’s time to build my service images and push them to this new registry.

### 2.1 **Build the Docker Image:**

```bash
docker build -t <MY_SERVER_IP>:5000/accounter .
```

obviously, I Replaced `<MY_SERVER_IP>` with actual server’s IP address (where the registry is hosted). This builds our image and tags it for our local registry.

### 2.2 **Push the Image to Local Registry:**

```bash
docker push <MY_SERVER_IP>:5000/accounter
```

let's then Push that freshly packed service into our registry! 🎉 The registry is now ready to serve Our `accounter` image whenever you need it. (we must do the same for authentiq image as well)

---

## 🌀 **Step 3: Initialize Docker Swarm**

It's time to create our Docker Swarm! we’re ready to deploy multiple services across multiple nodes(2 nodes for our setup), this is where the magic happens.

```bash
docker swarm init --advertise-addr <MY_MASTER_IP>
```

This initializes a Swarm with our server as the **master node**. The `--advertise-addr` ensures that the master node can communicate with other nodes. 🚀

next, we use the JOIN command that is generated, on our worker node.

---

## 🚀 **Step 4: Deploy the Stack**

Now comes the exciting part: deploying our stack to the Swarm! 💥

```bash
docker stack deploy -c docker-compose.yml huma
```

This command tells Docker to read our `docker-compose.yml` file and deploy the services defined in the file. Our Swarm will spin up the services across available nodes. Sit back, grab a coffee, and watch the orchestration unfold! ☕️

---

## 🎉 **That's It!** 

With those four steps, we’ve successfully set up a local Docker registry, built and pushed our images, initialized Docker Swarm, and deployed our services. Our cluster is now running and ready to scale as needed!

---

### 🤖 **Handy Commands to Keep Things Rolling**

- **View Swarm nodes:**

  ```bash
  docker node ls
  ```

- **Check deployed services:**

  ```bash
  docker service ls
  ```

- **Monitor logs of a specific service:**

  ```bash
  docker service logs -f <service_name>
  ```

---
🎯 Accessing Your Services

Once our services are deployed, we can test and monitor them using the following URLs:
- **[Auth Service](https://auth.geek4geeks.ir/authentiq/v1/heartbeat)**: Test the authentication service here.
- **[Account Service](https://usermanager.geek4geeks.ir/accountico/heartbeat)**: Test the account management service.
- **[Visualizer Panel](https://visualizer.geek4geeks.ir)**: Access the Docker Swarm Visualizer panel to see what's happening under the hood.


---
Thanks for sailing the Swarm seas with me! 🐳

- authored by: Mohammad Shafighi
