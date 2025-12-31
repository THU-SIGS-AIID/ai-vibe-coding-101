# Extra 1 - What is Git and GitHub

In previous lessons, we learned how to write code using web-based vibe coding tools. Every conversation creates a new version of the code. But let's think about a question: If we want to revert to a previous modification, is there a convenient way? Is there a tool that can record our code at different stages, allowing us to switch and modify between different versions at any time?

To meet this need, version control software was born. In this article, we will introduce the most famous version control program—Git—and the best code hosting platform—GitHub. We will learn how to use Git for code management, how to get others' code from GitHub, how to upload our own code, and how to collaborate with others on large projects.

Whether it's version tracking for personal projects, code synchronization in team collaboration, or contributing to the open-source community, Git and GitHub are essential tools for modern developers. By mastering them, you will be able to manage code more efficiently, create checkpoints as needed, switch freely between different stages of code, and easily handle everything from single file changes to developing large projects—making every code iteration controllable and traceable.

# What is Git

Git is a distributed version control system created in 2005 by Linux kernel developer Linus Torvalds. Its core function is to track the modification history of files, allowing developers to view and roll back to previous versions at any time, and efficiently merge changes when collaborating with others.

![](images/image1.png)

Compared to early centralized version control systems, Git's "distributed" nature allows each developer's local device to store the full history of the code repository. Most operations (such as commits, rollbacks, and branch management) can be performed without depending on a central server, making Git more flexible and suitable for large-scale collaboration and offline work.

> 💡 Before operating Git, let's first understand what a terminal is.
>
> ## What is a Terminal?
>
> A terminal is essentially a text-based "computer access point." In the early days, before graphical interfaces (no icons, no mouse clicks) appeared, users could only interact with computers by typing text commands. This method has been passed down through generations and has become the terminal we are introducing today.
>
> It doesn't rely on fancy interfaces and works purely through "command + feedback." This makes it one of the most basic and direct methods of human-computer interaction.
>
> Terminals vary across different systems. On Windows, common ones are "Command Prompt (cmd)" and "PowerShell." You can launch these command-line programs by typing "cmd" or "powershell" in your computer's run/search box.
>
> ![](images/image2.png)
>
> ![](images/image3.png)
>
> The former is an older tool that only supports basic commands like viewing files and copying, suitable for simple tasks. The latter is a more advanced version that can handle complex operations like process management and remote control, and is also compatible with cmd commands—making it more commonly used in development or system administration scenarios. macOS and Linux both come with "Terminal" by default, and their command logic is similar, originating from Unix (a classic computer system developed by Bell Labs engineers in the late 1960s).
>
> Terminals remain crucial today because of their efficiency and wide compatibility. For example, a single command can batch rename files, which is much faster than repeatedly clicking with a mouse. Additionally, local servers, cloud servers, and professional development environments often don't have graphical interfaces, making terminal operation necessary. Many tasks, such as installing various programs (like Git, Python, system tools, or development dependencies), running code, managing computer processes, and configuring system parameters, also require terminal commands.
>
> You might wonder what to do if you can't remember all those terminal commands. In fact, with the rapid development of large language models, there's no longer a need for rote memorization as before. Now, you just need to ask the model when needed (e.g., "How to use Git to get remote code?" or "How to delete a folder or batch create folders via command line?"), and then copy the useful commands from the reply.
>
> ![](images/image4.png)

## How to Install Git

We will demonstrate three methods for installing Git on different computer operating systems. Please follow the instructions based on your system version:

### Windows

1. Go to the [Git official download page](https://git-scm.com/download/win) and download the installer suitable for your system: [Installation Package](https://github.com/git-for-windows/git/releases/download/v2.51.0.windows.1/Git-2.51.0-64-bit.exe). By default, the x64 installer is recommended.
2. Double-click the installer and follow the installation wizard instructions:
  ![](images/image5.png)

   1. It is recommended to keep the default options. If you need to customize, please note the following points: (In most cases, you can just click "Next" all the way)
      * Select the default editor used by Git: Choose your preferred editor (such as VS Code). You can default to the first option, Vim (a text editor), or select the "Visual Studio Code as Git's default editor" option (requires VS Code to be pre-installed). You can keep the default selection and click "Next" to continue.
       ![](images/image6.png)
      * Choose how to use Git: These three options control Git's accessibility in the system. It's recommended to choose option 2 ("from command line and 3rd-party software")—it adds basic Git tools to the PATH, allowing you to use Git in Git Bash, Command Prompt, PowerShell, and IDEs without cluttering your system.
       ![](images/image7.png)
3. After installation, right-click on the desktop. If you see "Git Bash Here" in the menu, the installation was successful.

![](images/image8.png)

### MacOS

For macOS, you can first check if Git is already installed by typing `git --version` in the terminal. If not, the system will prompt you to install it—just follow the instructions to complete the installation.

1. Method 1: Install via Homebrew
   If you have [Homebrew](https://brew.sh/) (a Mac package manager) installed, open the terminal and type:
   ```Bash
   brew install git
   ```
2. Method 2: (Recommended) Install via Xcode: https://developer.apple.com/xcode/, which has Git built-in. After installation, just follow the instructions to proceed.

### Linux

Most Linux distributions can install Git through their package managers:

* Ubuntu/Debian:

```Bash
sudo apt update
sudo apt install git
```

* CentOS/RHEL:

```Bash
sudo yum install git
```

* Verify Installation: Type `git --version` in the terminal. If a version number is displayed, the installation was successful.

## Git Initialization

After installing Git, you first need to configure your user information—this is a basic step for version control using Git. Execute the following commands in the terminal (replace the content in brackets with your own information):

```Bash
# Set global username (will be displayed in commit records)
git config --global user.name "Your Name"

# Set global email (recommended to use the email registered on platforms like GitHub/GitLab)
git config --global user.email "your.email@example.com"
```

Git will embed this information into every commit record as the "author information" for each modification. When viewing version history (e.g., using `git log`), you can clearly see who modified each line of code, making it easy to trace responsibility and communicate. In collaborative projects, unified identity information allows team members to quickly identify who made which changes, thereby improving collaboration efficiency (e.g., finding the relevant developer via commit records to discuss issues).

You can check the current Git configuration information by typing `git config --list` in the command line to confirm the settings were successful.

# What is GitHub

GitHub is a code hosting platform based on Git. It not only provides remote storage for Git repositories but also includes collaboration tools (such as Issues, Pull Requests, Projects), making it easier for developers to share code and collaborate. In short, Git is a local version control tool, while GitHub is a remote "code repository cloud drive + collaboration community."

GitHub is not only the world's largest code hosting platform but also the most active and influential open-source community globally. The core idea of "open source" here is that anyone can download and run the software's source code. This model allows people from all over the world to check each other's code and make modifications, or create new projects based on it. For example, you can find various learning tutorials and the full source code for frameworks used to train GPT models (such as PyTorch) on GitHub. Every day, countless people collaborate globally to review and improve code.

![](images/image9.png)

Many large companies open-source their programs or tutorials on GitHub to gain an industry competitive advantage—this can also be seen as a form of advertising. In the GitHub community, the number of "stars" a project receives is a primary measure of its value; the more stars a project or organization has, the greater its credibility and influence.

![](images/image10.png)

In our course, support resources and assignments will also be uploaded to a dedicated GitHub repository. Through the process of uploading assignments, you will gradually become familiar with and master the use of GitHub, laying a solid foundation for version control in future application development.

## Registering a GitHub Account

1. Visit the [GitHub official website](https://github.com/) and click "Sign up" in the top right corner.
  ![](images/image11.png)
2. Enter your email address (recommended to use a commonly used one, as verification and notifications will be sent there), and set a password (must contain letters, numbers, and special characters).
3. Complete the human verification, follow the prompts to verify your email, and your account will be created.

## Creating Your First Repository on GitHub

Next, we will create the first storage folder, also known as a repository or "repo."

![](images/image12.png)![](images/image13.png)

![](images/image14.png)

1. **Repository name:** The name of the repository displayed to others.
2. **Description:** A detailed description of the repository.
3. **Choose visibility:** For personal repositories, if set to **private**, only you and specifically invited people can see it. If set to **public**, everyone can see it.
   For repositories within an organization, if **Private**, only people within the organization can see it. If **Public**, people outside the organization can also see it.
4. **README:** It's common practice for every repository to have a README file. You can think of it as a complete introduction to the repository, including usage instructions, file lists, and operation methods.
5. **Add .gitignore and license:**
   1. **.gitignore** file tells Git to ignore certain folders or files when uploading to GitHub, so they won't be tracked or added to the staging area. This is useful for temporary test files, dependency packages, or large files. Once specified, these files will no longer be tracked.
   2. **license** refers to the type of open-source license you choose. Different licenses detail whether others can use your code for commercial purposes and include other terms and conditions.

It's recommended to check "Add a README file," set the repository visibility to "Private," fill in the repository name and description according to your preference, and then click "Create repository" to finish creating your first remote repository.

![](images/image15.png)

After that, you will have a clean repository without any extra files. You can then start uploading files.

![](images/image16.png)

The command to get the repository is `git clone`, but it requires the repository address. You can find the repository address by clicking the green "Code" button, where you will see HTTPS and SSH options. Usually, you can use either of these two methods to download the repository to your local machine (only then can you modify and upload files).

![](images/image17.png)

In general, repositories cloned via HTTPS are suitable for temporary downloading and testing others' repositories, but not recommended for your own development. For a better learning experience, you should set up SSH authentication first.

## Binding Local SSH

In GitHub, "SSH protocol binding" essentially means associating your local device's SSH public key with your GitHub account, allowing GitHub to identify your device via the SSH protocol. This enables you to safely operate remote repositories without a password (such as clone, push, or pull code).

Simply put: it's like giving your device a "GitHub-exclusive access card." Once bound, when your device accesses a GitHub repository via the SSH protocol, GitHub will verify this "access card" (your SSH public key). Once confirmed as your authorized device, you can operate directly—no need to enter your username and password every time.

> 💡 What is SSH?
>
> ### Why is SSH protocol binding needed?
>
> GitHub supports two main protocols for repository operations: HTTPS protocol and SSH protocol:
>
> * **HTTPS protocol:** Every operation (such as `push`) requires entering your GitHub username and password (or Personal Access Token PAT). The verification process is tedious, and there's a risk of password leakage.
> * **SSH protocol:** Authentication is done via "key pairs," so there's no need to repeatedly enter passwords, and encrypted transmission is more secure.
>
> "SSH protocol binding" is a prerequisite step for enabling GitHub SSH authentication—only after "binding" the local SSH public key to your GitHub account can GitHub recognize your device and allow SSH operations on repositories.
>
> ### The Core Logic of "Binding": The Role of SSH Key Pairs
>
> SSH authentication relies on key pairs (public key + private key), which are matching encrypted files. Once generated, you need to provide the "public key" to GitHub ("binding"), while the "private key" stays on your local device:
>
> 1. **Private Key:** Stored in a designated directory on your local device (e.g., computer) (usually `~/.ssh/`), acting as "your exclusive key" that must never be shared with anyone.
> 2. **Public Key:** This is a "lock" that can be shared publicly—you need to copy it into the "SSH keys list" of your GitHub account ("binding" operation).
>
> When you operate on a GitHub repository via SSH (e.g., `git push git@github.com:xxx/xxx.git`):
>
> * Your local device uses the private key to encrypt the "operation request" and sends it to GitHub;
> * Upon receiving the request, GitHub tries to decrypt it using the public key you previously bound;
> * If decryption is successful, your device is confirmed as authorized, and the operation is allowed; otherwise, access is denied.
>
> ### Specific Steps for "Binding" (Core Workflow)
>
> Once you understand the principle, the actual operation is simple—the core is "Generate key pair → Upload public key to GitHub":
>
> 1. **Generate SSH Key Pair Locally**
>    1. **Use Trae to get the public key (Recommended)**
>       Prompt: `Help me create the SSH key needed for GitHub login. My email is your_email@gmail.com. Please return the public key for me to copy.`
>
>      ![](images/image18.png)
>
>       After entering the prompt, you also need to press Enter in the terminal on the left; otherwise, the command will wait indefinitely. Since Trae cannot perform any conditional judgments for you, we just need to keep pressing Enter.
>
>       Finally, you will see the public key read by Trae returned on the right. Just copy it and get ready to paste it in the next step.
>
>      ![](images/image19.png)
>    2. **Manually get the public key**
>       Open your local terminal (Git Bash or PowerShell on Windows; Terminal on macOS/Linux), and type the following command (replace `your_email@example.com` with the email you used when registering your GitHub account):
>
>       ```Bash
>       ssh-keygen -t ed25519 -C "your_email@example.com"
>       ```
>
>       1. Press Enter to accept the default values (default file path, no passphrase, or set a passphrase if needed). This will generate two files in the `~/.ssh/` directory:
>          * `id_ed25519`: Private key (saved locally, **never shared**);
>          * `id_ed25519.pub`: Public key (needs to be uploaded to GitHub).
> 2. **"Bind" the Public Key to Your GitHub Account**
>
> This is the core binding step—adding the local public key to the "SSH keys list" of your GitHub account:
>
> 1. **Copy the public key content:**
>    1. **Trae:** (If you used the Trae method above)
>    2. **Windows:** Open `C:\Users\<your_username>\.ssh\id_ed25519.pub` with Notepad and copy all its content;
>    3. **macOS/Linux:** Run `cat ~/.ssh/id_ed25519.pub` in the terminal and copy all the output (from the beginning `ssh-ed25519` to the end email).
> 2. **Log in to GitHub and go to the "SSH Key Management" page:**
>    1. Click on your avatar in the top right corner → **Settings** → Left menu **SSH and GPG keys** → Click **New SSH key**.
>      ![](images/image20.png)![](images/image21.png)
>    2. Enter any title (e.g., "Your Local Computer's SSH"), then paste the SSH public key you just obtained here.
>
> ![](images/image22.png)
>
> ![](images/image23.png)
>
> 3. **Verify if the binding was successful**
>
> Type the following command in the terminal (**Trae can also do this**) to test if GitHub can recognize your device:
>
> ```Bash
> ssh -T git@github.com
> ```
>
> * If you see something like `Hi [your GitHub username]! You've successfully authenticated...`, it means you have successfully bound the key;
> * If you encounter an error, it's usually because the public key was not copied completely, the private key permissions are too high (your local `~/.ssh/` directory should only be readable/writable by you), etc. Check these issues as needed.
>
> ### Important Notes
>
> If you have multiple devices (e.g., a laptop and a desktop), you need to generate a separate SSH key pair for each device and bind each public key to the same GitHub account—each device has its own "access card."
>
> Never share your private key (don't upload it to GitHub or share it with others), otherwise, someone could impersonate you and operate your repositories. If the private key is leaked, immediately delete the corresponding public key from GitHub and generate a new key pair.
>
> After binding SSH, use the SSH-formatted repository address (e.g., `git@github.com:username/repository.git`) for operations, instead of the HTTPS format (e.g., `https://github.com/username/repository.git`). If you previously cloned a repository using HTTPS, you can switch protocols with `git remote set-url origin <new_ssh_url>`.

# GitHub Operations Using Trae

We've explained what Git is, what GitHub is, what SSH is, and how to configure it. Now you can freely use Trae to perform Git operations. First, let's learn how to clone a remote repository to your local machine.

## Git Clone: Download an Existing Repository

You can directly tell it the address of the repository you want to clone.

![](images/image24.png)

## Git Pull: Get Updates from a Remote Repository

Before each update to the repository, as it might be maintained by multiple people, you need to pull the latest changes first. After that, you can modify and push files.

**Remember to include the folder name and its relative or absolute path to avoid pushing to the wrong repository.**

Prompt: `Help me pull this repository AIID-TEST in ./AIID-TEST.`

## Git Commit & Git Push: Stage Updates and Push to GitHub

Once everything is ready, you can try modifying local files, or adding or deleting items in the folder. Then, let Trae detect the changes and help you push them to GitHub.

Prompt: `I'm finished. Commit and push to the repository AIID-TEST in ./AIID-TEST.`

![](images/image25.png)

Push successful. Now you can see the updated content on GitHub.

# References

* Pro Git book: https://git-scm.com/book/en/v2
* GitHub Docs: https://docs.github.com/en
