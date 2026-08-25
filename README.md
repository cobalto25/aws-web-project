Step-by-Step Guidance

Welcome to the Step-by-Step Guidance version of this project. Let's do this!



📣 If you're EVER stuck - ask the NextWork community. Students like you are already asking questions about this project.

Make sure to fill out all the tasks in this project and get documentation automatically generated for you (wooohoooo)!





Before we get started, it's important that you know what we're trying to do today.







Ready to set up your web app from scratch?




In this step, you're going to:





Launch an EC2 instance.



Set up VSCode on your local computer.



Use Remote - SSH to connect VSCode with your EC2 instance.







Set up your web app

First things first... have you already done Project 1 (Set Up a Web App in the Cloud) of the 6 Day DevOps Challenge?






Alrighty, it's good to see you again! If you've done the first project, we'll assume that you already have an IAM Admin User and still have VS Code installed.

Setting up your web app environment again is going to be awesome - let's go!




Launch an EC2 Instance

Since we want your web app to be entirely created and run on the cloud, we'll use a virtual server (EC2 instance) to house our development work.

Let's get an EC2 instance up and running!





Log in to AWS as an IAM Admin User.



Head to Amazon EC2.



Switch your Region to the one closest to you.



💡 Tip: We recommend using the following regions
Did you know that not all regions have the same number of AWS services available?

There are only 13 AWS Regions that provide ALL the services we'll use in the 6 Day DevOps Challenge. We'd recommend using one of these regions from the very start of the challenge, so all your resources are in the same place. Even if you don't live in these regions, you can still use them:





us-east-1 (N.Virginia)



us-east-2 (Ohio)



us-west-2 (Oregon)



eu-west-1 (Ireland)



eu-west-2 (London)



eu-central-1 (Frankfurt)



eu-north-1 (Stockholm)



eu-south-1 (Milan)



eu-west-3 (Paris)



ap-southeast-1 (Singapore)



ap-southeast-2 (Sydney)



ap-northeast-1 (Tokyo)



ap-south-1 (Mumbai)





In your EC2 console, select Instances from the left hand navigation panel.



Choose Launch instances.







Set up your EC2 instance. In Name, enter the value:

nextwork-devops-





Choose Amazon Linux 2023 AMI under Amazon Machine Image(AMI).



Leave t2.micro under Instance type.



Under Key pair (login), select Create a new key pair and use nextwork-keypair as your key pair's name.



If you happened to have saved your key pair from the previous project, check: is your private key (nextwork-keypair.pem) still in your local computer? If you can still find it, you can use the existing newtwork-keypair key pair instead of creating a new one.



Store nextwork-keypair.pem in a new folder called DevOps in your local computer's Desktop.







Back to our EC2 instance setup, head to the Network settings section.



For Allow SSH traffic from, select the dropdown and choose My IP. This makes sure only you can access your EC2 instance. You can double check your IP by clicking here.







Choose Launch instance.



🙋‍♀️ Didn't see a success message?

Share any errors/questions with the NextWork community!





Open VS Code in your local computer.







Select Terminal from the top menu bar.



Select New Terminal from the dropdown.





💡 What is a terminal?
A terminal is where you send instructions to your computer using text instead of clicks. For example, instead of right-clicking on your desktop to create a new folder, you can type a simple text command in your terminal instead. It's like sending text messages to your computer's operating system to tell it what to do.

Every computer has a terminal. On Windows, it's often called Command Prompt or PowerShell, while macOS and Linux systems use Terminal.





Navigate your terminal to the DevOps folder:





cd ~/Desktop/DevOps (Mac/Linux)



cd C:\Users\YourUserName\Desktop\DevOps (Windows)



Once you’re in the DevOps folder, you might want to check if your .pem file is there. Use ls (Mac/Linux) or dir (Windows).



Change the permissions of your .pem file:

In the terminal, run the following command to allow access to your .pem file.






chmod 400 nextwork-keypair.pem




💡 What is chmod?
This command stands for "change mode", and it changes the permissions of your .pem file. Using 400 makes it readable only by you (the owner) and restricts access for everyone else.

We're changing the permissions of your .pem file so that you have access to it when you connect to your EC2 instance later. Blocking out everyone else keeps your .pem file i.e. your secret key secure.





icacls "nextwork-keypair.pem" /reset
icacls "nextwork-keypair.pem" /grant:r ":R"
icacls "nextwork-keypair.pem" /inheritance:r




💡 What is icacls?
Icacls (which stands for Integrity Control Access Control Lists) is a tool for Windows that lets you decide who can open or change the files on your system. In these icacls commands, you're using:





/reset to remove default permission settings on the file



/grant:r "USERNAME:R" to give the current user (that's you!) read access to your secret key



/inheritance:r to make sure changes in the permissions of other files and the DevOps folder won't change the permission settings for this file.





Make sure to enter your Windows username. If you don't know your username, run whoami in your terminal to find out.



🎥 Ran into an error? Getting stuck on this step? 
If you're doing this project on a Windows computer, you can watch a video tutorial about this step. Kudos to Praneeth (an awesome NextWork student) 😎

We also talk about running these commands on Windows in this community post.

Connect to your EC2 Instance

Let's use the terminal in VS Code to set up a 🔌 connection 🔌 to your EC2 instance. Once we're connected, we can work inside your EC2 instance to set up that web app.





Head back to your AWS Management Console.



Click on Instances from the left hand navigation panel.



Click on the checkbox next to your EC2 instance to view its details.



Under the Details tab, look for Public IPv4 DNS. You'll need it in a bit, so save it here:

 







Head back to VS Code and open your terminal again.



Use the following command to connect to your EC2 instance:

ssh -i  ec2-user@





Make sure to replace the PATH TO YOUR .PEM FILE with the actual path to your private key file (e.g., ~/Desktop/DevOps/nextwork-keypair.pem).



Replace YOUR PUBLIC IPV4 DNS with the Public DNS you just found.



🙋‍♀️ I'm getting an error!
Ah, classic! Many students have run into an error at this step, and we'll get you unstuck. Make sure there are no spaces in your folder names (e.g. the DevOps folder cannot be titled Dev Ops).

Check out these community posts on SSH connection errors:





🎥 Windows video guide



EC2 Not Connecting?



SSH Disconnecting?



SSH still loading after 10 min



"Permission denied" error



"Permission denied" error



"Cannot find path" error



“Connection timed out” error



"Could not establish connection" error



"Could not establish connection" error



Other errors


Still stuck? Share any other errors/questions with the NextWork community!





Your terminal will ask if you want to continue connecting to this EC2 instance. Enter yes to continue connecting.



Congrats! You've connected your EC2 instance via SSH.



Install Apache Maven and Amazon Corretto 8

Connection DONE. This means your terminal has now entered into your EC2 instance and can use it like a computer that's right in front of you! What a vibe 🥁

Now let's install two tools that are going to help us build Java web apps. Remember Apache Maven and Amazon Corretto 8?





Install Apache Maven using the commands below:

wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz

sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt

echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc

source ~/.bashrc




💡 What is Apache Maven?
Apache Maven is a tool that helps developers build and organize Java software projects. It's also a package manager, which means it automatically download any external pieces of code your project depends on to work.

We're also using Maven today because it's really useful for kick-starting web projects! It uses something called archetypes, which are like templates, to lay out the foundations for different types of projects e.g. web apps.

We'll use Maven later on to help us set up all the necessary web files to create a web app structure, so we can jump straight into the fun part of developing the web app sooner.





Now we're going to install Java 8, or more specifically, Amazon Correto 8.

sudo dnf install -y java-1.8.0-amazon-corretto-devel

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64

export PATH=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64/jre/bin/:$PATH







💡 What is Java? What is Amazon Correto 8?
Java is a popular programming language used to build different types of applications, from mobile apps to large enterprise systems. Maven, which we just downloaded, is a tool that NEEDS Java to operate. So if we don't install Java, we won't be able to use Maven to generate/build our web app today

Amazon Corretto 8 is a version of Java that we're using for this project. It's free, reliable and provided by Amazon.


💡 Woah! What's all this text popping up in the terminal?
The text you see after these commands is the terminal keeping you updated about it's progress with installing Java. It shows the specific packages it's going to install, downloading status, and even verifying that everything was installed.





To verify that Maven is installed correctly, run mvn -v next. Make sure the output mentions a Maven version 3.5.x.



To verify that you've installed Java 8 correctly, run java -version.





💡 Important 
If the Java version command above doesn't return openjdk version 1.8 (=> Java 8), run the following command that allows you to choose the correct Java version: sudo alternatives --config java


🙋‍♀️ Seeing error messages while installing Maven/Java?
Share any errors/questions with the NextWork community!

Create the Application

We've assembled both Maven and Java into our EC2 instance. Now let's cut straight to generating the web app!





Use mvn to generate a Java web app. To do this, use these commands:

mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false




💡 Break down these commands for me... What is mvn? 
When you run mvn commands, you're asking Maven to perform tasks (like creating a new project or building an existing one). 

The mvn archetype:generate command specifically tells Maven to create a new project from a template (which Maven calls an archetype). This command sets up a basic structure for your project, so you don't have to start from scratch.

Extra for Experts: Some of the details you've specified in this command are...





-DartifactId=nextwork-web-project names your project



-DarchetypeArtifactId=maven-archetype-webapp specifies that you're creating a web application.



-DinteractiveMode=false runs the command without pausing for user input, so Maven will go ahead and install everything without waiting for your confirmation.





Watch out for a BUILD SUCCESS message in your terminal once your application is all set up.



Connect VS Code with your EC2 Instance

In this step, you'll connect VS Code to your EC2 instance so you can see and edit the web app you've just created.






If you don't have Remote - SSH installed in VS Code already, select the Extensions icon at the side of your VS Code window. Search for Remote - SSH and click Install for the extension.



Click on the double arrow icon at the bottom left corner of your VS Code window. This button is a shortcut to use Remote - SSH.



Select Connect to Host...




If you see an existing EC2 instance listed as an SSH Host, that's an EC2 instance you've set up for this series before! We would've terminated that instance by now, so we should remove it to avoid any confusion later on.



Select Configure SSH Hosts..., and clear everything in your config file (which should look like /Users/username/.ssh/config).



Save your changes, and select Connect to Host... again.







Select + Add New SSH Host...



Enter the SSH command you used to connect to your EC2 instance:

ssh -i  ec2-user@



🙋‍♀️ I'm getting an error!
Ah, classic! Many students have run into an error at this step, and we'll get you unstuck. Make sure there are no spaces in your folder names (e.g. the DevOps folder cannot be titled Dev Ops).

Check out these community posts that solve connection errors with using Remote - SSH:





🎥 Windows video guide



EC2 Not Connecting?



SSH Disconnecting?



SSH still loading after 10 min



"Permission denied" error



"Permission denied" error



"Cannot find path" error



“Connection timed out” error



"Could not establish connection" error



"Could not establish connection" error



Other errors


Still stuck? Share any other errors/questions with the NextWork community!





Select the configuration file at the top of your window. It should look similar to /Users/username/.ssh/config







A Host added! popup will confirm that you've set up your SSH Host - yay!



Select the blue Open Config button on that popup.



Confirm that all the details in your configuration file look correct:





Host should match up with your EC2 instance's IPv4 DNS.



IdentityFile should match up to nextwork-keypair.pem's location in your local computer.



User should say ec2-user







Now you’re ready to connect VS Code with your EC2 instance.



Click on the double arrow button on the bottom left corner and select Connect to Host again.



You should now see your EC2 instance listed at the top.







Select the EC2 instance and off we gooooooooooo to a new VS Code window ✈️



Check the bottom right hand corner of your new VS Code window - it should show your EC2 instance's IPV4 DNS.



Now that VS Code is connected to your EC2 instance, let's open up your web app's files.





From VS Code's left hand navigation bar, select the Explorer icon.



Select Open folder.



Enter /home/ec2-user/nextwork-web-project.



Press OK.







VS Code might show you a popup asking if you trust the authors of the files in this folder. If you see this popup, select Yes, I trust the authors.



Check your VS Code window's file explorer again - a folder called nextwork-web-project is here!







Try expanding all the subfolders in the file explorer. All folders have a > icon next to their name.



💡 What are all these files and subfolders?
All the files and subfolders you see under nextwork-web-project are parts of a web app! You can start working right away on the content you want to display on your web app, since Maven's taken care of the basic structuring and setup.  Let's get to know some of these web app files/folders:





The src (source) folder holds all the source code files that define how your web app looks and works.



src is further divided into webapp, which are the web app's files e.g. HTML, CSS, JavaScript, and JSP files, and resources, which are the configuration files a web app might need e.g. connection settings to a database.



pom.xml is a Maven Project Object Model file. It stores information and configuration details that Maven will use to build the project. We'll use pom.xml later in this project series!





From your file explorer, click into index.jsp.







Let's try modifying index.jsp by changing the placeholder code to the code snippet below. Don't forget to replace {YOUR NAME} from the following code with your name:

<html>

<body>

<h2>Hello </h2>

<p>This is my NextWork web application working!</p>

</body>

</html>








Save the changes you've made to index.jsp by selecting Command/Ctrl + S on your keyboard.



Amazing! If you've kept all your resources, there's no more web app set up left to do - straight to GitHub you go 🔥

⬇️ Click here to head to the next step.





👀 You can still complete this project without doing Project 1 (Set Up a Web App in the Cloud) first - but we highly recommend giving it a go and writing documentation on your web app set up too!

If you get stuck in this step, make sure to check out Project 1's step by step guide for in-depth explanations and troubleshooting.

Set up an IAM Admin User





Do you have an IAM user?






Oooo it's the start of a new era!

If you don't have an IAM user yet - here are the steps to create one (this takes less than 10 mins).



💡 What is an IAM user? Why are we setting one up?
In AWS, a user is a person or a computer that can do things on the AWS cloud.

When you create an AWS account for the first time, the login you get is called the root user of the AWS account. AWS actually recommends to not use your root user for everyday tasks to protect it from security breaches.

You should create IAM users instead. If a root user is a master key to your AWS account, think of IAM users as key copies. IAM users have separate usernames and passwords to your root user, and you can set them to have limited access to your account's resources.





Head to your AWS Account as the root user.



Open the AWS IAM console.



From the left hand navigation panel, choose Users.



Choose Create user.



For the User name, name it:

-IAM-Admin






Make sure to select the checkbox next to Provide user access to the AWS Management Console - optional.‍



💡 This does not apply to all accounts, but if you're prompted with a pop up panel that says Are you providing access to a person?, choose I want to create an IAM user.‍







For the console password, choose Custom password.



Type in a password that you will be able to remember/access in the future.



💡 Top tip: You will use this password for all future projects, so make sure to choose a secure one!







Deselect the checkbox for Users must create a new password at next sign-in - Recommended.







Choose Next.



In the permissions set up page, choose Attach policies directly.



From the list of Permissions policies, select AdministratorAccess.



Choose Next.



Choose Create user.



Voilà - you've just created your new user! Stay on this page.





Choose Download .csv file.







Copy the Console sign-in URL.







Now you're ready to start using your IAM user. 🏁



Log out of your root user's AWS Account.



Paste and go to your copied console sign-in URL.



Open your downloaded .csv file containing your user's access instructions.



Log in using your IAM user's username and password in the .csv file.







Once you're logged in, you're ready to use your IAM user for this project! Make sure to keep the login details safe - you'll need them for the entire 6 Day DevOps Challenge!







Log in to the AWS Management Console with your IAM Admin User.



🙏 PLEASE make sure you log in to your IAM Admin User instead of the root user - it's truly best practice for account security.




Launch an EC2 Instance

Before we get into the juicy work of building your web app, we need to set up a home for your web app's files.

Since we want your web app to be entirely created and run on the cloud, we'll use a virtual server (EC2 instance) to house our development work.





Head to Amazon EC2.



Switch your Region to the one closest to you.



💡 Tip: We recommend using the following regions
Did you know that not all regions have the same number of AWS services available?

There are only 13 AWS Regions that provide ALL the services we'll use in the 6 Day DevOps Challenge. We'd recommend using one of these regions from the very start of the challenge, so all your resources are in the same place. Even if you don't live in these regions, you can still use them:





us-east-1 (N.Virginia)



us-east-2 (Ohio)



us-west-2 (Oregon)



eu-west-1 (Ireland)



eu-west-2 (London)



eu-central-1 (Frankfurt)



eu-north-1 (Stockholm)



eu-south-1 (Milan)



eu-west-3 (Paris)



ap-southeast-1 (Singapore)



ap-southeast-2 (Sydney)



ap-northeast-1 (Tokyo)



ap-south-1 (Mumbai)




🙋‍♀️ Extra for Experts: How do you know only these regions have all the services we need?


By checking out AWS' guidance on services by region! Once you select a region, you can sift through the list and identify whether it has all the services you need.





In your EC2 console, select Instances from the left hand navigation panel.



Choose Launch instances.







Set up your EC2 instance:



In Name, enter the value:

nextwork-devops-





Don't forget to enter your name!



Choose Amazon Linux 2023 AMI under Amazon Machine Image(AMI).



Leave t2.micro under Instance type.



Select Create a new key pair and use nextwork-keypair as your key pair's name.



Store nextwork-keypair.pem in a new folder called DevOps in your local computer's Desktop.







Back to our EC2 instance setup, head to the Network settings section.



For Allow SSH traffic from, select the dropdown and choose My IP. This makes sure only you can access your EC2 instance. You can double check your IP by clicking here.







Choose Launch instance.



🙋‍♀️ Didn't see a success message?
Share any errors/questions with the NextWork community!

Install VS Code

Do you have VS Code installed on your computer?






Let's goooooo! We'll set up VS Code in just a few minutes, and learn why we use it along the way.





Head to the Visual Studio Code website.



💡 What is VS Code?
Visual Studio Code (VS Code) is one of the most popular tools for creating and managing coding projects. You'll often hear people call VS Code an IDE (Integrated Development Environment), which means software that help you write and edit code. It's similar to how Microsoft Word or Google Docs help you write documents!

VS Code also comes with extra tools that we'll use to connect to virtual servers like EC2 instances.





Install VS Code by following the installation instructions for your OS e.g. Linux, Mac, Windows.



💡 How can I decide which setting/chip option I should pick?
If you're unsure of which chip/settings option to pick for your device:





Mac: Select the Apple icon from the top left hand corner of your computer's menu bar. Select About this Mac, and note whether your Chip says Apple or Intel.



Windows: Click the Start button and search for System Information. Note whether your System Type says x64-based or ARM-based PC.



Linux: Open a terminal and run uname -m. Note whether the output says x86_64 or aarch64/arm64.







Once downloaded, you might need to unzip a zip file to access VS Code.







Open VS Code in your local computer (you'll find it in your Downloads folder).



If a popup asks you to confirm opening VS Code, select Open.







Welcome to VS Code!







Awesome! You're already set up to use VS Code.



Open VS Code in your local computer.







Select Terminal from the top menu bar.



Select New Terminal from the dropdown.





💡 What is a terminal?
A terminal is where you send instructions to your computer using text instead of clicks. For example, instead of right-clicking on your desktop to create a new folder, you can type a simple text command in your terminal instead. It's like sending text messages to your computer's operating system to tell it what to do.

Every computer has a terminal. On Windows, it's often called Command Prompt or PowerShell, while macOS and Linux systems use Terminal.





Navigate your terminal to the DevOps folder:





cd ~/Desktop/DevOps (Mac/Linux)



cd C:\Users\YourUserName\Desktop\DevOps (Windows)



Once you’re in the DevOps folder, you might want to check if your .pem file is there. Use ls (Mac/Linux) or dir (Windows).



Change the permissions of your .pem file:

In the terminal, run the following command to allow access to your .pem file.






chmod 400 nextwork-keypair.pem




💡 What is chmod?
This command stands for "change mode", and it changes the permissions of your .pem file. Using 400 makes it readable only by you (the owner) and restricts access for everyone else.

We're changing the permissions of your .pem file so that you have access to it when you connect to your EC2 instance later. Blocking out everyone else keeps your .pem file i.e. your secret key secure.





icacls "nextwork-keypair.pem" /reset
icacls "nextwork-keypair.pem" /grant:r ":R"
icacls "nextwork-keypair.pem" /inheritance:r




💡 What is icacls?
Icacls (which stands for Integrity Control Access Control Lists) is a tool for Windows that lets you decide who can open or change the files on your system. In these icacls commands, you're using:





/reset to remove default permission settings on the file



/grant:r "USERNAME:R" to give the current user (that's you!) read access to your secret key



/inheritance:r to make sure changes in the permissions of other files and the DevOps folder won't change the permission settings for this file.





Make sure to replace "USERNAME" with your Windows username. If you don't know your username, run whoami in your terminal to find out.



🎥 Ran into an error? Getting stuck on this step? 
If you're doing this project on a Windows computer, you can watch a video tutorial about this step. Kudos to Praneeth (an awesome NextWork student) 😎

We also talk about running these commands on Windows in this community post.




Connect to your EC2 Instance

Let's use the terminal in VS Code to set up a 🔌 connection 🔌 to your EC2 instance. Once we're connected, we can work inside your EC2 instance to set up that web app.





Head back to your AWS Management Console.



Click on Instances from the left hand navigation panel.



Click on the checkbox next to your EC2 instance to view its details.



Under the Details tab, look for Public IPv4 DNS. You'll need this in the next instruction!







Head back to VS Code and open your terminal again.



Use the following command to connect to your EC2 instance: ssh -i [PATH TO YOUR .PEM FILE] ec2-user@[YOUR PUBLIC IPV4 DNS]





Replace [PATH TO YOUR .PEM FILE] with the actual path to your private key file (e.g., ~/Desktop/DevOps/nextwork-keypair.pem). Delete the square brackets!



Replace [YOUR PUBLIC IPV4 DNS] with the Public DNS you just found. Delete the square brackets!



🙋‍♀️ I'm getting an error!
Ah, classic! Many students have run into an error at this step, and we'll get you unstuck. Share any other errors/questions with the NextWork community!





Your terminal will ask if you want to continue connecting to this EC2 instance. Enter yes to continue connecting.



Congrats! You've connected your EC2 instance via SSH.



Install Apache Maven and Amazon Corretto 8

Connection DONE. This means your terminal has now entered into your EC2 instance and can use it like a computer that's right in front of you!

Now let's install two tools that are going to help us build Java web apps. Introducing Apache Maven and Amazon Corretto 8 🥁 






Install Apache Maven using the commands below:

wget https://archive.apache.org/dist/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz

sudo tar -xzf apache-maven-3.5.2-bin.tar.gz -C /opt

echo "export PATH=/opt/apache-maven-3.5.2/bin:$PATH" >> ~/.bashrc

source ~/.bashrc




💡 What is Apache Maven?
Apache Maven is a tool that helps developers build and organize Java software projects. It's also a package manager, which means it automatically download any external pieces of code your project depends on to work.

We're also using Maven today because it's really useful for kick-starting web projects! It uses something called archetypes, which are like templates, to lay out the foundations for different types of projects e.g. web apps.

We'll use Maven later on to help us set up all the necessary web files to create a web app structure, so we can jump straight into the fun part of developing the web app sooner.





Now we're going to install Java 8, or more specifically, Amazon Correto 8.

sudo dnf install -y java-1.8.0-amazon-corretto-devel

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64

export PATH=/usr/lib/jvm/java-1.8.0-amazon-corretto.x86_64/jre/bin/:$PATH







💡 What is Java? What is Amazon Correto 8?
Java is a popular programming language used to build different types of applications, from mobile apps to large enterprise systems.

Maven, which we just downloaded, is a tool that NEEDS Java to operate. So if we don't install Java, we won't be able to use Maven to generate/build our web app today

Amazon Corretto 8 is a version of Java that we're using for this project. It's free, reliable and provided by Amazon.


💡 Woah! What's all this text popping up in the terminal?
The text you see after these commands is the terminal keeping you updated about it's progress with installing Java. It shows the specific packages it's going to install, downloading status, and even verifying that everything was installed.





To verify that Maven is installed correctly, run mvn -v next. Make sure the output mentions a Maven version 3.5.x.



To verify that you've installed Java 8 correctly, run java -version.





💡 Important 
If the Java version command above doesn't return openjdk version 1.8 (=> Java 8), run the following command that allows you to choose the correct Java version: sudo alternatives --config java


🙋‍♀️ Seeing error messages while installing Maven/Java?
Share any errors/questions with the NextWork community!

Create the Application

We've assembled both Maven and Java into our EC2 instance. Now let's cut straight to generating the web app!





Use mvn to generate a Java web app. To do this, use these commands:

mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false




💡 Break down these commands for me... What is mvn? 
When you run mvn commands, you're asking Maven to perform tasks (like creating a new project or building an existing one). 

The mvn archetype:generate command specifically tells Maven to create a new project from a template (which Maven calls an archetype). This command sets up a basic structure for your project, so you don't have to start from scratch.

Extra for Experts: Some of the details you've specified in this command are...





-DartifactId=nextwork-web-project names your project



-DarchetypeArtifactId=maven-archetype-webapp specifies that you're creating a web application.



-DinteractiveMode=false runs the command without pausing for user input, so Maven will go ahead and install everything without waiting for your confirmation.





Watch out for a BUILD SUCCESS message in your terminal once your application is all set up.



Connect VS Code with your EC2 Instance

In this step, you'll connect VS Code to your EC2 instance so you can see and edit the web app you've just created.






If you don't have Remote - SSH installed in VS Code already, select the Extensions icon at the side of your VS Code window. Search for Remote - SSH and click Install for the extension.



💡 Why are we installing Remote - SSH?
The Remote - SSH extension in VS Code lets you connect directly via SSH to another computer securely over the internet. This lets you use VS Code to work on files or run programs on that server as if you were doing it on your own computer, which will come in handy when we edit the web app in your EC2 instance!





Click on the double arrow icon at the bottom left corner of your VS Code window. This button is a shortcut to use Remote - SSH.



Select Connect to Host...



Select + Add New SSH Host...



Enter the SSH command you used to connect to your EC2 instance: ssh -i [PATH TO YOUR .PEM FILE] ec2-user@[YOUR PUBLIC IPV4 DNS]



🙋‍♀️ I'm getting an error!
Ah, classic! Many students have run into an error at this step, and we'll get you unstuck. Make sure there are no spaces in your folder names (e.g. the DevOps folder cannot be titled Dev Ops).

Check out these community posts on SSH connection errors:





🎥 Windows video guide



SSH still loading after 10 min



"Permission denied" error



"Permission denied" error



"Cannot find path" error



“Connection timed out” error



"Could not establish connection" error



"Could not establish connection" error



Other errors


Still stuck? Share any other errors/questions with the NextWork community!





Select the configuration file at the top of your window. It should look similar to /Users/username/.ssh/config







A Host added! popup will confirm that you've set up your SSH Host - yay!



Select the blue Open Config button on that popup.



Confirm that all the details in your configuration file look correct:





Host should match up with your EC2 instance's IPv4 DNS.



IdentityFile should match up to nextwork-keypair.pem's location in your local computer.



User should say ec2-user







Now you’re ready to connect VS Code with your EC2 instance.



Click on the double arrow button on the bottom left corner and select Connect to Host again.



You should now see your EC2 instance listed at the top.







Select the EC2 instance and off we gooooooooooo to a new VS Code window ✈️



Check the bottom right hand corner of your new VS Code window - it should show your EC2 instance's IPV4 DNS.



Now that VS Code is connected to your EC2 instance, let's open up your web app's files.





From VS Code's left hand navigation bar, select the Explorer icon.



Select Open folder.



Enter /home/ec2-user/nextwork-web-project.



Press OK.







VS Code might show you a popup asking if you trust the authors of the files in this folder. If you see this popup, select Yes, I trust the authors.



Check your VS Code window's file explorer again - a folder called nextwork-web-project is here!







Try expanding all the subfolders in the file explorer. All folders have a > icon next to their name.



💡 What are all these files and subfolders?
All the files and subfolders you see under nextwork-web-project are parts of a web app! You can start working right away on the content you want to display on your web app, since Maven's taken care of the basic structuring and setup.  Let's get to know some of these web app files/folders:





The src (source) folder holds all the source code files that define how your web app looks and works.



src is further divided into webapp, which are the web app's files e.g. HTML, CSS, JavaScript, and JSP files, and resources, which are the configuration files a web app might need e.g. connection settings to a database.



pom.xml is a Maven Project Object Model file. It stores information and configuration details that Maven will use to build the project. We'll use pom.xml later in this project series!





From your file explorer, click into index.jsp.







Let's try modifying index.jsp by changing the placeholder code to the code snippet below. Don't forget to replace {YOUR NAME} from the following code with your name:

<html>

<body>

<h2>Hello </h2>

<p>This is my NextWork web application working!</p>

</body>

</html>








Save the changes you've made to index.jsp by selecting Command/Ctrl + S on your keyboard.



Now that your development environment is ready, the next step is to set up Git on your EC2 instance.




💡 What is Git? 
Git is like a time machine and filing system for your code. It tracks every change you make, which lets you go back to an earlier version of your work if something breaks.

You can also see who made specific changes and when they were made, which makes teamwork/collaboration a lot easier.


Extra for Experts: Git is often called a version control system since it tracks your changes by taking snapshots of what your files look like at specific moments, and each snapshot is considered a 'version'.

In this step, you're going to:





Install Git on your EC2 instance.









Open your EC2 instance's terminal.



In the terminal, run these commands to install Git:

sudo dnf update -y
sudo dnf install git -y






💡 What do these commands do?





sudo dnf update -y tells your EC2 instance to find all the latest updates of software it has (e.g. Java, Maven) and install them straight away.



sudo dnf install git -y installs Git on your EC2 instance.
It's best practice to update your existing software before installing new ones, just in case there are compatibility issues between new and old software.


Extra for Experts: -y is a shortcut for "yes," meaning you're giving your EC2 instance your approval in advance for any time the system might ask questions like "should I proceed with the installation?"





Verifiy the installation:

git --version













Git is installed woohoo! Next up, we'll set you up with GitHub.



💡 What is Github? 
GitHub is a place for engineers to store and share their code and projects online. It's called GitHub because it uses Git to manage your projects' version history.

In this step, you're going to:





Set up a GitHub account.



Create a GitHub repository.





Log in to GitHub





Do you have a GitHub account?






Woooo exciting - let's get you set up! Signing up is free and takes just 5 minutes.





Head to GitHub's signup page.



Follow the prompts to create your account by entering your email, creating a password, and choosing a username.







Complete one of their bot verification tasks. Switch the task type to Audio if the Visual task crashes your website.



Once your account is created, confirm your email address with a verification code sent to your inbox.







Log into your GitHub account once you've verified your email.



Welcome to your GitHub account!





Ahh too good!





Let's sign in to GitHub.



💡 What is the difference between Git & Github?
If Git is the tool for tracking changes, think of GitHub as a storage space for different version of your project that Git tracks. Since GitHub is a cloud service, it also lets you access your work from anywhere and collaborate with other developers over the internet.


💡 Why would I use Github? Isn't the code in my EC2 instance already in the cloud? 
Even though your code is on a cloud server like EC2, GitHub helps you use Git and see your file changes in a more user-friendly way. It's just like how using an IDE (VSCode) makes editing code easy.

GitHub is also especially useful in situation where you're working in teams and need to share your updates and reviews to a shared code base.





🗂️ Set up a new repository

Nice, you're ready to set up a new repository on GitHub!



💡 What is a repository?
To store your code using Git, you create repositories (aka 'repos'), which are folders that contain all your project files and their entire version history. Hosting a repo in the cloud, like on GitHub, means you can also collaborate with other engineers and access your work from anywhere.





After signing in to GitHub, click on the + icon next to your GitHub profile icon at the top right hand corner.



Select New repository.







Select Create repository.



This loads up a new page where you can create a repository.



Under Owner, click on the Choose an owner dropdown and select your GitHub username.



Under Repository name, enter nextwork-web-project



For the Description, enter Java web app set up on an EC2 instance.



Choose your visibility settings. We'd recommend selecting Public to make your repository available for the world to see.







Select Create repository.











So we now have a place in the cloud that will store our code and track the changes we make.

But... this storage folder (your GitHub repo) still doesn't know where your web app files are.

Lets connect our GitHub repo with our web app project stored in your EC2 instance. 


In this step, you're going to:





Set up a local git repo in your web app folder.



Connect your local repo with your GitHub repo.









Head back to your VSCode remote window. Make sure it's still SSH connected to your EC2 instance by checking the bottom left corner.



Check that you are in the right folder by running this command in your terminal: pwd





💡 What does pwd do?
pwd stands for print working directory, and this command asks your server "where am I right now?" The terminal will show you the exact location of the directory (folder) you're in.





If you're not in nextwork-web-project, use cd to navigate your terminal into your web app project. If you're stuck, ask the NextWork community!



Now let's tell Git that we'd like to track changes made inside this project folder.

git init




💡 What does git init do?
To start using Git for your project, you need to create a local repository on your computer.

When you run git init inside a directory e.g. nextwork-web-project, it sets up the directory as a local Git repository which means changes are now tracked for version control.


💡 What's a local repository?
The local repository is where you use Git directly on your own EC2 instance. The edits you make in your local repo is only visible to you and isn't shared with anyone else yet

This is different to the GitHub repository, which is the remote/cloud version of your repo that others can see.





💡 WOAH! I got a bunch of yellow text when I ran this command
This yellow text is just Git giving you a heads-up about naming your main branch master and suggesting that you can choose a different name like 'main' or 'development' if you want.


💡 What is a main branch?
You can think of Git branches as parallel versions or 'alternate universes' of the same project. For example, if you wanted to test a change to your code, you can set up a new branch that lets you diverge from the original/main version of your code (called master) so you can experiment with new features or test bug fixes safely. We won't create new branches in this project and we'll save all new changes directly to master, but it's best practice to make all changes in a separate branch and then merge them into master when they're ready.













Head back to your GitHub repository's page.



In the blue section of the page titled Quick setup - if you’ve done this kind of thing before, copy the HTTPS URL to your repository page. It will look like https://github.com/username/nextwork-web-project.git



Now let's connect your local project folder with your Github repo!





Head back to your terminal in VSCode.



Run this command. Don't forget to add link you've just copied.

git remote add origin 





💡 What does 'remote add origin' mean?
Your local and GitHub repositories aren't automatically linked, so you'll need to connect the two so that updates made in your local repo can also reflect in your GitHub repo.

When you set remote add origin, you're telling Git where your GitHub repository is located. Think of origin as a bookmark for your GitHub project's URL, so you don't have to type it out every time you want to send your changes there.

Next, we'll save our changes and push them into GitHub.





Run this command in your terminal:

git add . 




💡 What does this command do? 
git add . stages all (marked by the '.') files in nextwork-web-project to be saved in the next version of your project.

💡 What does staging mean? 
When you stage changes, you're telling Git to put together all your modified files for a final review before you commit them. This is incredibly handy because you get to see all your edits in one spot, which means its much easier to check if there were are mistakes or unwanted changes before you commit.

Pssttt... Want to see what changes are staged? Run git diff --staged to review your code changes.





Run this command next in your terminal:

git commit -m "Updated index.jsp with new content"




💡 What does this command do? 
git commit -m "Updated index.jsp with new content"saves the staged changes as a snapshot in your project’s history. This means your project's version control history has just saved your latest changes in a new version. -m flag lets you leave a message describing what the commit is about, making it easier to review what changed in this version.





Finally, run this command:

git push -u origin master




💡 What does this command do? 
git push -u origin master uploads i.e. 'pushes' your committed changes to origin, which you've bookmarked as your GitHub repo. 'master' tells Git that these updates should be pushed to the master branch of your GitHub repo. By using -u you're also setting an 'upstream' for your local branch, which means you're telling Git to remember to push to master by default. Next time, you can simply run git push without needing to define origin and master.













Ah we're so close, but Git can't push your work to the Github repository yet. It's now asking for a username!





💡 Why is Git asking for my username?
Git needs to double check that you have the right to push any changes to the remote origin your local repo is connected with. To do this, Git is now authenticating your identity by asking for your GitHub credentials.





Enter your Github username, and press Enter on your keyboard.



Next, enter your password. You'll notice that as you type this out, nothing shows on your terminal. This is totally expected - your terminal is hiding your input for your privacy. Press Enter on your keyboard when you've typed out your password, even if you don't see it printed out in your terminal.



Hmmmm, now Git is letting us know that it can't actually accept our password.





💡 What does this mean?
GitHub phased out password authentication to connect with repositories over HTTPS - there are too many security risks and passwords can get intercepted over the internet 🤺 You need to use a personal access token instead, which is a more secure method for logging in and interacting with your repos.

💡 What is a token?
A token in GitHub is a unique string of characters that looks like a random password. For example, a GitHub token might look like ghp_xHJNmL16GHSZSV88hjP5bQ24PRTg2s3Xk9ll. As you can imagine, tokens are great for security because they're unique and would be very hard to guess.











Now that we know passwords won't work for authentication, we'll have to find a replacement.

Let's generate an authentication token on GitHub! 


In this step, you're going to:





Set up a token on GitHub.



Use the generated token to access your GitHub repo from your local repo.









Head back into your browser with GitHub open.



Select your profile icon and select Settings.







Select Developer settings at the very bottom of the left hand navigation panel.







Select Personal access tokens.



Select Tokens (classic).



Select Generate new token.



Select Generate new token (classic).







Give your token a descriptive note, like Generated for EC2 Instance Access. This is a part of NextWork's 6 Day DevOps Challenge.



Lower the token expiration limit from 30 days to 7 days.



💡 What is a token expiration limit?
A token expiration limit is how long your personal access token would work for. After this time period, the token expires and no longer grants access, so you'll need to generate a new token.





Select the checkbox next to repo.



💡 What do all these scopes mean?
We use scopes to decide what kind of permissions your token will grant. Each scope you pick gives the token the ability to do even more things with your GitHub account. In our case, we picked the repo scope, which means the token can even access and control private repositories in your account.











Select Generate token.



Nice, a new token (a long string of random letters) is generated!



💡 I also see a banner at the top of the screen... what does this mean?
You might see a banner at the top of the page that says "Some of the scopes you've selected are included in other scopes. Only the minimum set of necessary scopes has been saved." This simply means the scope repo is the overarching scope for a broad range of permissions, so some of the smaller scopes you'be checked under repo overlaps with the main one.





Make sure to copy your token now. Keep it safe somewhere else, you won't be able to see your token once you close this tab.











Head to your VS Code terminal.



Run git push -u origin master again, which will trigger Git to ask for your GitHub username.



Enter your username again.



✋ PAUSE



Do you remember what the GitHub token was generated for?



When Git asks for your password, paste in your token instead. Your terminal won't show your password for privacy reasons, so press Enter on your keyboard once you've pasted your token (even if you don't see it on screen).



Well done! Looks like Github recognises your token and pushed your changes to your repository.





💡 What does the message in the terminal mean?
This message appears when you successfully push changes to a GitHub repository - nice work. It shows the progress of transferring objects (like files and commits), how many objects were processed, and tells you that your local branch is now tracking the remote branch after the push.





Head to your GitHub repository in your web browser.



Refresh the page, and you’ll see your web app files in the repository, along with the commit message you wrote.





🙋‍♀️ Don't see your web app files in GitHub?
It happens, and it's definitely fixable. Share any errors/questions with the NextWork community.

When you add, commit and push your changes, you might notice the terminal automatically sets two other things - your name and email address - before it asks for your GitHub username.





💡 Why does my terminal need my name and email?
Git needs author information for commits to track who made what change. If you don't set it manually, Git uses the system's default username, which might not accurately represent your identity in your project's version history.





Run git log to see your history of commits, which also mentions the commit author's name.















Hmmm EC2 Default User isn't really your name, and the EC2 instance's IPv4 DNS is not your email. Let's configure your local Git identity so Git isn't using these default values.



Run these commands in your terminal to manually set your name and email. Don't forget to replace with your name (keep the quote marks), and your email address.

git config --global user.name ""
git config --global user.email 



Nice work! You've set up your local Git identity, which means Git can associate your changes in the local repo to your name and email.

This setup is best practice for keeping a clear history of who made which changes ✅



Great sucess with getting your GitHub connection all set up.

So we've learnt how to link your EC2 instance's files with a cloud repo, now let's see what happens when you make new changes to your web app files.

In this step, we'll edit index.jsp again using VSCode, and run commands that pushes those changes to your GitHub repository too. 


In this step, you're going to:





Make changes to your web app.



Commit and push those changes.









Keep your GitHub page open, and switch back to your EC2 instance's VSCode window.



Find index.jsp in your file navigator on the left hand panel.



Find the line that says This is my NextWork web application working! and add this line below:

<p>If you see this line in Github, that means your latest changes are getting pushed to your cloud repo :o</p>









Save your changes by pressing Command/Ctrl + S on your keyboard while keeping your index.jsp editor open.



Head back to your GitHub tab and click into the src/main/webapp folders to find index.jsp.



Click into index.jsp - have there been any updates to index.jsp in your GitHub repo?





💡 Hmmm it's still looking the same...
You won't see your changes in GitHub yet, because saving changes in your VSCode environment only updates your local repository. Remember that the local repository in VSCode is separate from your GitHub repository in the cloud.

To make your changes visible in GitHub, you need to write commands that send (push) them from your local repository into your origin.





Head back to your VSCode window.



In the terminal, let's stage our changes: git add .



Ready to see what changes are staged? Run git diff --staged next.





💡 What does this command do?
git diff --staged shows you the exact changes that have been staged compared to the last commit. Now you get to review your modifications in your code that you are about to save into your local repo's version history!


💡 Extra for Experts: Did you know you can view these changes using VSCode too?






Select the Source Control icon on the side of your VSCode window.



Under the Saved Changes heading, select index.jsp.



You'll see your change in a new window that hightlights the new line you've added to index.jsp!







Nice, these changes are what we want to save and send to GitHub, lets do that with these commands:

git commit -m "Add new line to index.jsp"
git push




🙋‍♀️ Help! My terminal isn't letting me enter commands!
This doesn't apply to everyone, but your terminal might stay stuck in the previous step to show you your staged changes. Enter q into the terminal to quit this view and return to running commands.


Extra for Experts: Interesting, why would my terminal stay stuck?
When you run certain Git commands like git status, Git uses a pager to handle the output (by default, this is usually on most Unix-like systems so other operating systems might now show this). The pager lets you scroll through information that can't fit on a single terminal window. While in this mode, you can't enter new commands until you quit pager view. Your terminal will look like it's "stuck" because it's waiting for you to finish reviewing the output.





You might need to enter your username and token again to complete your push.





💡 I have to enter my username and password AGAIN?!
This is because we set up the connection to our GitHub repo using its HTTPS URL. Using HTTPS is straightforward compared to other options e.g. SSH, but it's also stateless, which means Git doesn't remember your credentials for security reasons. That's why Git asks for your GitHub credentials 👏 every time 👏 you pull from or push to your GitHub repo.


Top tip: right after you enter your username and token again, you can run git config --global credential.helper store to ask Git to remember your credential details for next time!





Head back to your GitHub tab and refresh it - do you see your changes now?





🙋‍♀️ index.jsp didn't update for you?
Hmmm let's solve this! Share any errors/questions with the NextWork community.











Welcome to your 🤫 exclusive 🤫 secret mission!

Your mission, should you choose to accept it, is to add shiny cherry on top to your GitHub repository - a README file.




💎 In this secret mission, get ready to:





Add a README file to your GitHub repo.



Showcase your secret mission in your project documentation.





💎 Congratulations - Secret Mission unlocked!









Back to VS Code, make sure you're still in your Remote - SSH window to your EC2 instance.



In the terminal, run a new command that will set up a README file for your repository.

touch README.md






💡 What does 'touch' do?
touch is Linux command for creating a new file. By running touch README.md, you've just created a new blank file with the name README.md.


💡 What is a README file?
A README is a document that introduces and explains your project, like what the project does, how to set it up, and how to use it.

Having a README is super common practice in software development (not just on GitHub).

When recruiters or potential collaborators look at your project, a well-organized README can really boost their impression of your work and showcase your documentation skills!


💡 Extra for Experts: Why is README in all caps?
"README" is written in all caps to make it stand out as an important file in a project directory.

Fun fact: Some teams organise all development files in lower case to tell which files actually contribute to the app's functionality (e.g. index.jsp) and which don't (e.g. README.md).









Paste this template into your README.md:

# Java Web App Deployment with AWS CI/CD

Welcome to this project combining Java web app development and AWS CI/CD tools!

<br>

## Table of Contents
- [Introduction](#introduction)
- [Technologies](#technologies)
- [Setup](#setup)
- [Contact](#contact)
- [Conclusion](#conclusion)

<br>

## Introduction
This project is used for an introduction to creating and deploying a Java-based web app using AWS, especially their CI/CD tools.

The deployment pipeline I'm building around the Java web app in this repository is invisible to the end-user, but makes a big impact by automating the software release processes.

<br>

## Technologies
Here’s what I’m using for this project:

- **Amazon EC2**: I'm developing my web app on Amazon EC2 virtual servers, so that software development and deployment happens entirely on the cloud.
- **VS Code**: For my IDE, I chose Visual Studio Code. It connects directly to my development EC2 instance, making it easy to edit code and manage files in the cloud.
- **GitHub**: All my web app code is stored and versioned in this GitHub repository.
- **[COMING SOON] AWS CodeArtifact**: Once it's rolled out, CodeArtifact will store my artifacts and dependencies, which is great for high availability and speeding up my project's build process.
- **[COMING SOON] AWS CodeBuild**: Once it's rolled out, CodeBuild will take over my build process. It'll compile the source code, run tests, and produce ready-to-deploy software packages automatically.
- **[COMING SOON] AWS CodeDeploy**: Once it's rolled out, CodeDeploy will automate my deployment process across EC2 instances.
- **[COMING SOON] AWS CodePipeline**: Once it's rolled out, CodePipeline will automate the entire process from GitHub to CodeDeploy, integrating build, test, and deployment steps into one efficient workflow.


<br>

## Setup
To get this project up and running on your local machine, follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/nextwork-web-project.git
    ```
2. Navigate to the project directory:
    ```bash
    cd nextwork-web-project
    ```
3. Install dependencies:
    ```bash
    mvn install
    ```

<br>

## Contact
If you have any questions or comments about the NextWork Web Project, please contact:
 - [Your Email](mailto:)

<br>

## Conclusion
Thank you for exploring this project! I'll continue to build this pipeline and apply my learnings to future projects.

A big shoutout to **[NextWork](https://learn.nextwork.org/app)** for their project guide and support. [You can get started with this DevOps series project too by clicking here.](https://learn.nextwork.org/projects/aws-devops-vscode?track=high)





💡 Woah! Is this... code?
Nope! Instead of code, this is Markdown, a text language that lets you format text that you'll display on a webpage. With Markdown, you can make words bold, create headers, add links, and use bullet points - all with simple symbols added to your text.

It’s useful for creating documents like README files that need to look clean and easy to read without complex software, making it a favorite for writing on platforms like GitHub.





💡 What do the different symbols mean?
Here's a quick Markdown cheatsheet!

Headers





# for largest header (H1)



## for second largest (H2)



### for third (H3), and so forth up to ###### for the smallest header (H6).


Text styling





**text** to make text bold



*text* to make text italic



~~text~~ to strike through text


Lists





- or * for unordered bullet lists



1., 2., etc., for ordered lists


Links





[link text](URL) to create a hyperlink



<br> for a line break (HTML style)


Images





![image captions](image_URL) to embed an image


Code





Put text inbetween `backticks` for inline code like this



Use triple backticks ``` for multi-line code blocks

Like this!


Blockquotes





Use > for block quotes



Like this one!









Complete this README file:





In the ## Contact section, replace Your Name with your name.



Replace Your Email and your.email@email.com with your email.







Make this README file your own by adding a few extra details. Here are a few ideas on what you could add...





## Introduction: Add two bulletpoints on why you're doing this project or how it fits into your career or personal growth goals.



## Technologies: Add any challenges you've faced and the solutions you've found while using these tools.



## Setup: Add troubleshooting tips for common setup issues.



## Contact: Add a link to your LinkedIn profile or professional websites, and add your professional profile photo.








Press Ctrl+S or Cmd+S on your keyboard to save your changes.



Woohoo README file all setup 💪



Now we'll push the README into your GitHub repo.



Do you remember the commands for saving and pushing changes into your GitHub repo?

git add .
git commit -m "create README"
git push








Head back to your GitHub repo and refresh the tab.



Tadaaaaaa! You should see a shiny new README file displayed for your project right away.













You MUST delete your resources to avoid charges to your AWS account.



🤫 If you're doing Day Three of the 6 Day DevOps Challenge tomorrow...
Did you know that Day Three of the 6 Day DevOps Challenge is going to pick up right where you left off here?

You don't have to delete your resources (so you won't have to repeat this project's steps) IF you're also doing Day Three's project in the next day. Just make sure to:





Complete all your tasks and



Download today's documentation before heading to Day Three.

✋ STOP

Before diving into the steps for deleting your resources, why not challenge yourself to delete everything on your own?

Keeping track of your resources, and deleting them at the end, is a key skill that will help you avoid charges to your account.




🛑 STEPS BELOW:

Here are the resources we'll delete:

EC2 instance

Key pair (optional)












In your AWS Management Console, head to Amazon EC2 to delete your EC2 instance.



Select Instances from the left hand navigation panel. Select the checkbox next to your instance.



Click on the Instance state dropdown and select Terminate (delete) instance.



Choose Terminate (delete).





Note: If you plan to continue this DevOps Challenge (totally recommend!), you can keep your key pair and use the same credentials for the rest of this series. AWS does not charge for key pairs. Store your key pair in a safe place.





Still in your EC2 console, select Key Pair from the left hand navigation panel.



Select the checkbox next to your key pair.



Select the Actions dropdown, and then Delete.



Type Delete in the text field, and select Delete.







Don't forget to delete your private key pair in your local computer - you can remove the entire DevOps foler!



VS Code and GitHub are absolutely free to install and use, we'd recommend keeping both. They're great tools for future projects and you'll need them again for the rest of this DevOps series.

For security best practice, we'd recommend deleting your Personal Access Token!













Now it's time to share and let people know just what an amazing job you've done.



1. Share it on LinkedIn 😎‍.

It's so easy to share your documentation - all you have to do is:





SelectMission Accomplished at the end of this page 👇







Download your documentation as a PDF.







Select the LinkedIn icon to open a pre-populated post, all ready to go!







Select the X at the bottom of the post - it's blocking you from uploading documentation.







Click on the plus icon at the bottom of the panel.







Then select the page icon, which helps you Add a document.







Voilà! Upload your document and give it a nice title.



Select Done and Post to share your progress!



2. Celebrate in the NextWork community!

Share your PDF in the NextWork community.

Completing a project is literally one of the biggest achievements and milestones that everyone celebrates. Show us your amazing work. 👀





That's Day TWO of this 6 Day DevOps Challenge all doneee!

Congratulations on seting up your web app project's very own Git repository with GitHub.



Ready to quiz yourself? You got this! 💪



You've learnt how to:





⚙️ Set up a GitHub repository: You created a new repository in AWS GitHub to securely store and manage the source code for your Java web app.



☁️ Configure Git and a local repository: You established your Git identity with your username and email. You also initialized a local repo with your GitHub repo as the remote origin.



🫸 Make Your first commit and push: You added all your files to the staging area, committed them, and pushed these changes to the master branch of your GitHub repository, making your code available in the cloud.



💎 Set up a README file for your repo:You gave your GitHub repo the ultimate cherry on top - an informative and welcoming README file that introduces your project and offers tips on how to use the code.




Next up, we need to find a way to store our web app's packages and dependencies, which are pieces of code your web app relies on in order to work. This is where AWS CodeArtifact comes into play 👀



It's amazing that all these learnings are packed in one project. We'll you in the next project of the 6 Day DevOps Challenge - Secure Packages with CodeArtifact!





🚀 p.s. Does it say "Still tasks to complete!" at the bottom of the screen?

This means you still have screenshots left to upload, or questions left to answer!





Press Ctrl+F (Windows) or Command+F (Mac) on your keyboard.



Search for the text Return to later.



Jump straight to your incomplete tasks!



🙋‍♀️ Still stuck? Ask the community!
