# face-attendance-web-app-react-python

<p align="center">
<a href="https://www.youtube.com/watch?v=yWmW5uEtNws">
    <img width="600" src="https://utils-computervisiondeveloper.s3.amazonaws.com/thumbnails/with_play_button/face_attendance_web_app_react_python.jpg" alt="Watch the video">
    </br>Watch on YouTube: Face attendance + face recognition web app with React and Python !
</a>
</p>

## deployment

### backend

#### setup server

Log into your AWS account and launch a t2.2xlarge EC2 instance, using the latest stable Ubuntu image.

SSH into the instance and run these commands to update the software repository and install the dependencies.

    sudo apt-get update
    sudo apt install -y python3-pip nginx

    sudo nano /etc/nginx/sites-enabled/fastapi_nginx

And put this config into the file (replace the IP address with your EC2 instance's public IP):

    server {
        listen 80;   
        server_name <YOUR_EC2_IP>;    
        location / {        
            proxy_pass http://127.0.0.1:8000;    
        }
    }

    sudo service nginx restart
    
 Update EC2 security-group settings for your instance to allow HTTP traffic to port 80.
    
 #### Launch API endpoints
 
 Clone repository.
 
    git clone https://github.com/computervisiondeveloper/face-attendance-web-app-react-python.git
   
    cd face-attendance-web-app-react-python
    
Install Python 3.8, create a virtual environment and install requirements.

    sudo apt update

    sudo apt install software-properties-common

    sudo add-apt-repository ppa:deadsnakes/ppa

    sudo apt install python3.8

    sudo apt install python3.8-dev

    sudo apt install python3.8-distutils

    sudo apt install python3-virtualenv
    
    cd backend

    virtualenv venv --python=python3.8

    source venv/bin/activate
    
    pip install cmake==3.25.0

    pip install -r requirements.txt
    
Launch app.

    python3 -m uvicorn main:app
    
    
### frontend

You can host the frontend locally (localhost) or on a server. These are instructions in case you decide to do it on a server.

#### setup server

The process is similar as in the previous case.
  
Launch a t2.large instance from AWS.

SSH into the instance and run the same commands as in the backend section to install nginx.

The app will be launched in the port 3000, so you need to make a small adjustment in the config file.

    server {
        listen 80;   
        server_name <YOUR_EC2_IP>;    
        location / {        
            proxy_pass http://127.0.0.1:3000;    
        }
    }


    sudo service nginx restart
    
Update EC2 security-group settings for your instance to allow HTTP traffic to port 80.
 
#### Launch App
 
    git clone https://github.com/computervisiondeveloper/face-attendance-web-app-react-python.git
   
    cd face-attendance-web-app-react-python
    
    cd frontend/face-attendance-web-app-front/
    
    sudo apt-get install npm
    
    npm install
    
    npm start

Edit the value of __API_BASE_URL__ in src/API.js with the ip of the backend server.

You may need to adjust your browser to allow access to your webcam through an unsecure conection from the EC2 ip address. In chrome this setting is adjusted here __chrome://flags/#unsafely-treat-insecure-origin-as-secure__.
