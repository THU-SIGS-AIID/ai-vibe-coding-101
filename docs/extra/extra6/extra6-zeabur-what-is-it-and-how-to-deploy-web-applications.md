# Extended Knowledge 6 - What is Zeabur and How to Deploy Web Applications

In this tutorial, we will introduce Zeabur - a platform for deploying web services. It can help us quickly complete the entire process from "writing code" to "letting others access your website on the internet."

# What is "Deployment"?

Before we begin, let's first clarify what "Deployment" actually means. For any website to be accessible by external users, it must have a publicly accessible network address (this can be an IP address like 123.45.67.89, or a domain name like [google.com](https://google.com/)). But having an address is not enough - your written webpage code (such as HTML, CSS, JavaScript files, or projects built with frameworks like React, Vue), along with related image/video resources, must all be "placed" on a server that's online 24 hours a day, ready to respond to network requests, so that anyone's browser can access and download these resources.

![](images/image1.png)

Image source: https://www.hostinger.com/tutorials/what-is-cloud-hosting

The entire process of uploading resources, configuring the environment, and getting the service "running" is called **Deployment**.

Simply put: Webpages you write on your computer can only be accessed through a local address in your own browser when you start the program locally, because this code only exists on your hard drive. "Deployment" is the process of transferring your code and resources to a professional server connected to the public network and configuring it properly, so that this server knows "how to respond when others access" - for example: when someone enters your domain name in their browser, the server will immediately find the corresponding webpage files and transmit the content back to their device, allowing the user to see your page.

If you deploy manually, a project often requires several steps, and each step can have pitfalls. Common key steps include:

1. **Server Preparation**: You need to first purchase a cloud server (such as Alibaba Cloud, Tencent Cloud, or AWS EC2), select the server region (such as Shanghai, Singapore), configuration (CPU, memory, disk size, etc.), and also learn how to remotely connect to the server (for example, through SSH tools).
  ![](images/image2.png)
2. **Environment Configuration**: Web applications need to run in a specific "environment" - for example, running Node.js projects requires installing Node.js first; running Python projects requires installing Python and the corresponding third-party libraries. If the environment versions don't match, the program may error and fail to start.
3. **Upload Resources**: You need to upload your local code and resources to the server. Common methods include FTP or Git. If the project is large (such as containing video files), once you disconnect midway, you sometimes need to re-upload.

![](images/image3.png)

4. **Start Service and Test**: After uploading, you also need to execute commands on the server to start the application and test whether "the assigned network address is accessible." If it's not accessible, it's possible that the server firewall hasn't opened the corresponding port (for example, your application listens on port 3000, but that port is blocked by the firewall), or there may be bugs in the program itself. In this case, you need to check server logs to troubleshoot.
   > 💡 You can think of a port as a "room number" that distinguishes different applications on the same device, while IP is the "house number" of that device. IP and port together (IP:port) can precisely locate a specific network service.
5. **Maintenance and Updates**: Later, every time you modify the code, you need to re-upload and restart the service. If the server goes down (for example, power outage, network failure), you also need to manually restart the application, and sometimes you need to configure additional "process guardian tools" to automatically pull up the program when it exits abnormally.

"Low-code deployment platforms" like Zeabur were born to solve these complex problems. It will automatically help you complete the steps of "buying servers, configuring environments, uploading code, starting services, monitoring operations." You only need to connect your code repository (like GitHub or GitLab) to Zeabur, and it will automatically pull the code, identify the application type, configure the corresponding runtime environment, and finally give you a public network address that anyone can access. It can even bind your own domain with one click (for example, changing your-app.zeabur.app to your-app.com).

![](images/image4.png)

Next, we will demonstrate step by step how to use Zeabur to go from "code repository" to "publicly accessible webpage" without writing any server commands. Of course, you can also use Vercel (which also has a free tier) for similar simple web deployment. However, [Vercel](https://vercel.com/) access is somewhat unstable in some network environments. Interested students can learn about it on their own after class (the operation is also very simple: just connect your GitHub project).

# Deploying Dify with Zeabur

In previous lessons, we've briefly touched on Dify. Now, we can easily start our own Dify service through [Zeabur](https://zeabur.com/projects). First, open the [console page](https://zeabur.com/projects), let's first look at the various areas above.

![](images/image5.png)

On this page, you can first see many squares - these are services that have already been started. In the top menu, you'll see several options: Agent, Servers, Docs, Templates, etc., which represent:

1. **Agent**: Can open Zeabur's built-in intelligent assistant (Agent) to ask it how to operate, or to check the current server status.
2. **Servers**: Here you can add cloud servers you purchased yourself, or purchase servers directly through Zeabur.
3. **Docs**: View Zeabur's complete documentation.
4. **Templates**: Lists all built-in template images.

> The "Image" mentioned here can be understood as a "compressed package containing code and runtime environment." When a service is successfully running on a server, we can choose to package "this runtime environment + code" into an image. Afterward, on any new server, as long as we decompress and run this package, there's no need to reconfigure the environment and code, and the service can run directly.

In the upper right corner of the page, you can also see your balance. By default, there's about $5 of free credit per month. You don't need to worry too much about the specific billing rules for now - just know that as long as the server is running, it will consume credit.

![](images/image6.png)

Click the balance to view daily consumption details.

![](images/image7.png)

Now let's create our own Dify service. First, on the [console homepage](https://zeabur.com/projects), click "New Project".

![](images/image8.png)

Next is an explanation of the various creation methods:

1. **GitHub**
   Can connect to your GitHub account. After binding, you can directly select projects from your GitHub repository to deploy (GitHub is currently the world's largest code hosting platform).
2. **Template**
   Can deploy services based on templates. Zeabur has many built-in project templates (such as Dify, n8n, etc.), and you can quickly create and deploy applications based on these templates.
  ![](images/image9.png)
3. **Databases**
   For deploying database services, such as common databases like MySQL, MongoDB, etc.
   ![](images/image10.png)
4. **Functions**
   Can deploy function services. You can write JavaScript or Python code and have them called as functions.
   ![](images/image11.png)

   ![](images/image12.png)
5. **Local Project**
   Upload a local folder, and Zeabur will automatically identify the startup scripts inside. This is suitable for quickly deploying projects you've already developed locally to Zeabur.
   ![](images/image13.png)
6. **Docker Image**
   Deploy an already packaged Docker image. If your project has been packaged as a Docker image (for example, stored in Docker Hub or other image repositories), you can deploy it directly here.
   ![](images/image14.png)
7. **Cursor**
   If you have Cursor installed (such as Cursor IDE), you can deploy projects in Cursor directly to Zeabur through this entry.

If you want to deploy your own Dify service, it's recommended to choose the **Template** method, then enter "dify" in the search box. You'll see many versions maintained by different authors - you can choose any one (such as version v1.6.0).

![](images/image15.png)

Next, enter any name, and Zeabur will generate a temporary custom domain based on this name. Afterward, everyone can access your service through this URL.

![](images/image16.png)

After creation is complete, you'll see multiple programs (services) start in sequence. You need to wait patiently for all services to enter a "started" state. (Dify service is composed of multiple programs, each responsible for different functions, and they work together.)

Generally, you only need to click on the Dify application on the left to see the default access entry address. However, in this example, since there's an nginx layer in front, you need to click on the nginx service to get the final access address. You can understand it this way: nginx is the main program responsible for uniformly "receiving and sending requests" to the outside, and it distributes external access addresses to various internal services. Click Nginx on the left, and in the details page you can see the current service address, then open this address in your browser and wait for the service to fully start.

![](images/image17.png)

After a short wait, you'll see the Dify login interface. Enter your email address and registration password, and you can start using your own Dify service.

![](images/image18.png)

If you're interested, you can also start an n8n service. n8n is also a very popular AI workflow platform overseas.

![](images/image19.png)![](images/image20.png)

# ⚠️ How to Stop and Delete Projects

Since enabling server-related resources will incur costs, we must develop the habit of "promptly stopping unused services" during use to avoid consuming the monthly free credit.

To find the project management entry, first click the "Settings" option in the project.

![](images/image21.png)

After entering the settings page, scroll to the bottom of the page, and you'll see an interface similar to the following:

![](images/image22.png)

You can click "Suspend All Services" to pause all services to reduce costs; if services have issues, you can click "Restart All Services" to restart all services. If you're sure you no longer need this project, you can click "Delete Project" to completely delete the entire project.

# Deploying Snake Game with Zeabur and Trae

In the next part of this tutorial, we'll experience some advanced uses of Zeabur. We'll first use Trae to generate a Snake game, then deploy it to Zeabur's server and configure a publicly accessible link so anyone can open your game.

The first step is to create a Snake project locally using Trae.

### Implementing with HTML Framework

![](images/image23.png)

For Trae, generating an HTML-based Snake web game is very simple. After the game is generated, you only need to follow the Zeabur local deployment method introduced earlier and upload the folder containing all files.

![](images/image24.png)![](images/image25.png)![](images/image26.png)

After completion, you'll enter the service details interface:

![](images/image27.png)

Click the "Network" option on the left, find the "Public Address" area in the page. Click "Generate Domain" to generate an external access address, and you can enter any name you like.

![](images/image28.png)

![](images/image29.png)

After generation is complete, as long as you open this address in your browser, you can run your own Snake game. Other HTML-based web applications can also be deployed in exactly the same way.

![](images/image30.png)

### Implementing with React Framework

Earlier, we learned how to deploy HTML-based web applications. Next, let's try deploying a more commonly used frontend framework: a React application. Compared to pure HTML, React is considered a more mature, modern frontend development framework. It organizes page structure through components, which can significantly speed up the development of complex pages and is a mainstream choice for enterprise-level projects.

![](images/image31.png)

#### Refactoring to React Architecture

In Trae, you only need to tell the Agent: "Help me refactor this code to React architecture," and you can quite easily refactor the originally HTML-based structure into a React project.

![](images/image32.png)

However, compared to simple HTML files, React applications rely on more complex build tools and project structure, so the deployment process will be slightly more troublesome. A typical problem is reflected in port settings: by default, React applications generally listen on port 3000 (you can also see this in configuration files or startup logs).

However, deploying this way on Zeabur will fail - because Zeabur only supports applications listening on port 8080. That is, if you want React applications to run normally on Zeabur, we must first change the default listening port from 3000 to 8080.

To configure this step correctly, we first need to understand two concepts: what is a "Port", and what does "Listening Port" mean.

#### What is a Port?

> In computer networks, a port can be understood as a "logical communication endpoint" used to distinguish different network services running on the same device. Simply put, if an IP address is like a "house number" (for example, 162.128.1.1), then a port number is like a "room number" for different rooms in that building - each room corresponds to a service (such as a web server, email service, or your React application).
>
> Port numbers are represented by a 16-bit integer, with a range of 0 to 65535.

If you don't want to remember these details, you can simply understand: a port is a necessary part of forming a "network access address".

When we usually visit websites or IP addresses, we generally don't manually add a port number, because the default ports for the Web are 80 or 443 (HTTPS). Most browsers will automatically use these standard ports. For some special ports, like React's default 3000, or the 8080 required by Zeabur, we must add `:3000` or `:8080` after the address to access the corresponding content.

#### What is a "Listening Port"?

> "Listening port" refers to a port that a program actively "opens and monitors" on a device. When an application sets a listening port, it's essentially telling the operating system: "I'll wait for network requests on this port - whenever a request comes in, please forward it to me."

To understand it more vividly: imagine your computer is an office building, and the IP address is this building's address. Many companies or departments have opened offices in the building, each occupying different rooms, and the room numbers are the port numbers.

When the default React development server starts, it will "open" a room's door and arrange a "receptionist" to be on duty at the door - this room number is its listening port - 3000.

At the same time, the React program will tell this building's "property management" (operating system): "I'm in room 3000, please forward all letters addressed to 3000 (network requests) to me."

This way, when you visit the React website, the request first reaches the building; the property management sees the request needs to go to room 3000, and immediately forwards the request to React's "receptionist," who handles it and returns the result - this is the process of visiting a React application.

When you execute `npm start` locally (the default command to start the React development server locally, which can also be executed in the Agent sidebar of Vibe Coding), the React development server will automatically set the listening port to 3000.
Zeabur's platform design determines that it will only "recognize" applications listening on port 8080. If your React application still uses the default port 3000, Zeabur won't be able to forward requests correctly to your application, ultimately causing deployment to fail.

#### Modifying the Default Listening Port

There are many ways to change React's default listening port (3000) to the 8080 required by Zeabur. The simplest way is to directly instruct the Agent in Trae: "Please help me change the default port of this React project to 8080." Trae will help you modify the corresponding configuration files in the project. After modification, you only need to repackage and upload to Zeabur in the same way as before.

![](images/image33.png)

![](images/image34.png)

Specify an access URL in the network settings - the method is basically the same as deploying HTML projects - and you can start the React version of the service.

![](images/image35.png)

![](images/image36.png)

For other programs that need to modify port numbers, you can use the same approach: first change the default port, then upload to Zeabur for deployment. At this point, you've mastered the basic skills of deploying common web applications to servers.

You can try having Trae help you build different types of applications and deploy them to Zeabur's default servers. In later lessons, we'll also learn how to deploy applications to your own purchased cloud servers.
