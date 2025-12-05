# Docker 

- Going through the iamtimcorey Docker course



# Installation

- download from docker website
- wait for install
- Update Windows Subsystem for Linux
  - `wsl --update`
- log in with GitHub account
- check that docker is installed
  - Open powershell
  - run `docker --version`



# Terms

- Image
  - Blueprint
  - Read only operating system
  - can be modified
  - starting point for creating the application starting container
  - In C# terms, it is a class file
- Container
  - The actual house, build from the Image blueprint
- DockerFile
  - a set of instructions to tell the image how to build
  - Use the instructions to build an image, a set of steps



# Docker Commands

- Open Powershell
- List Images currently on machine
  - `docker images`
- List all containers on the machine
  - `docker ps -a`
  - the `-a` means to include all containers, even the ones not running



# Hello World Docker Container

- shortcut creation method
  - run: `docker run hello-world`
  - sample image for testing that docker is running end-to-end
  - will first check for local container, will then download the image if it is not found
  - Should return "Hello from Docker!" and additional texts. Means Docker is working correctly
  - Can run `docker ps -a` and it should show the hello-world container



# Building a Image & Container

- `cd` into where you want your container
- Create a project structure
  - "html" directory
  - within that directory, simple `index.html` file that just has a header
  - test file for creating the container
- Create a docker file
  - create a file called "dockerfile" with no file type: `dockerfile`
  - edit file with Notepad
- Create `FROM` line
  - Find on docker hub <u>https://hub.docker.com</u>
  - Search for "httpd"
  - Select "The Apache HTTP Server Project"
- Copy line
  - `COPY ./html/`
  - Take everything from the file path ./html and copy it
  - Pasted to `/usr/local/apache2/htdocs/`
    - File path located in docker hub documents
- Final DockerFile:
```
FROM httpd:alpine
COPY ./html/ /usr/local/apache2/htdocs/
```
- Build the file
  - `docker build -t hello-docker:1.0.0 .`
  - the `-t` creates the file name
  - After the colon `:` is created the tag or version
  - DON'T FORGET THE `.` AT THE END
    - instructions the command where to find the docker file (input the path)
    - `.` is just the current directory
- Image is now created, can be seen with `docker images`
- Create the container
  - `docker run --name hello-docker-container -p 8080:80 hello-docker:1.0.0`
  - `--name` sets the name
  - `-p` sets the port mapping
    - First number is local port
    - Second number is where it should be mapped to internally
  - Last item is the name of the image
- Can test if the container is running by going to the localhost in the web browser
  - `http://localhost:8080/`
- Stop the server container with `CTRL + C`


















































