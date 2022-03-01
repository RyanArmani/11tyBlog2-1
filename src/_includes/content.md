Twelvety is a pre-configured Eleventy starter project built to be fast. It includes:

## Docker Introduction
Docker is an extraordinarily popular open source containerization platform among developers. Docker enables developers to develop, ship, and run applications through its implementation of containers. Containers are a piece of software that packages up any code and its dependencies, enabling applications to run on various computing environments regardless of differences between system requirements from one computer to another. This popular method of running and delivering apps opens a world of possibilities, with a common use being businesses rolling out updates to existing software, and reverting back to older stages of a software if any errors arise.

## Starting with Docker
Docker utilizes a special file called a Dockerfile. a Dockerfile is a file that automatically runs a set amount of code within an application to assemble an image (an image is a set of code that creates a container within docker). One such example of a Dockerfile is included below, which is used to run the NewsAPI app from our class' project. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vcjtivtzet4d3or69bwr.png)An example of a fully functional application, the NewsAPI, is included below as well to demonstrate the full capabilities of docker. This includes a series of links to news articles 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bi0bu1pf2jqsnkvym7fh.png) One can utilize a query to find specific key terms 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/18v62me8an1gqux2qegs.png) 



## Create a docker file
To create a docker file for your own web app, you will need to clone a copy of your git repository (repo). One way to acquire the link to your repo is by navigating to your repo on github.com. Using my own repo as an example, navigate to the `Code` tab
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b56b1wd5lqrusw3dn7ve.png), and select the `https` icon. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qbdxuh8dcraoi34pm3af.png)You will see a link to your repo. Copy this link, as we will be utilizing it in the docker environment. Navigate to "play with docker" (https://www.docker.com/play-with-docker), and scroll down until you find the "Lab Environment" tab. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sy4j3rrh8qipg8agaq01.png)Select "Get Started, and sign into Docker if prompted. Once signed in, select the "Start" button. You are now ready to set up your web app!

Inside the docker playground, on the left hand side of the screen, click the "+ Add New Instance" option. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1cc0m1sybis0bbi3ga77.png)In a moment, you should see a terminal-like sandbox environment appear in docker playground. We can input commands here! For our purposes, we will clone our git repo. Use the command `git clone <your-repo-link-here>`. For my web app, I used the command `git clone https://github.com/IST402GroupB/ip-project.git`. 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t6vzwfjau2v316xywdi9.png)We will now create a temporary file within our web app. Type in the command touch dockerfile. This command creates an image of a file within docker named dockerfile, which is a file that can be edited within the Docker Editor provided, and can be viewed by the `ls -la` command. s
See the [GitHub repository](https://github.com/gregives/twelvety) for documentation.

Made and used by [Greg Ives](https://gregives.co.uk)

<!-- Markdown images will automatically use the responsive picture shortcode -->
![Time-lapse of a blue and white train moving fast through a station](train.jpg)
