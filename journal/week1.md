# Week 1 — App Containerization

Homework Requirements:

Required Work
BACKEND: I ran these separately.

I installed pip3 and FLASK so as to avoid any tampering 

pip install -r requirements.txt
flask run

Image: 

npm install
npm start


1a-I created a backend end point for notifications page

[[backend-flask/app.py]](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/backend-flask/app.py)
1b- I created a frontend end point for notifications page

[[frontend-react-js/src/pages/NotificationPage.js]](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/frontend-react-js/src/pages/NotificationsFeedPage.js)


2-I created a Dockerfile for frontend and backend

docker for frontend

[frontend-react-js/Dockerfile](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/frontend-react-js/Dockerfile)

docker for backend

[backend-flask/Dockerfile](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/backend-flask/Dockerfile)

I built an image and ran containers of apps separate

docker run for frontend

docker build -t aws-bootcamp-cruddur-2023-frontend /frontend-react-js
docker run --rm -d -p 3000:3000/tcp aws-bootcamp-cruddur-2023-frontend-react-js:latest

docker run for frontend

docker build -t aws-bootcamp-cruddur-2023-backend /backend-flask
docker run --rm -d  aws-bootcamp-cruddur-2023-backend-flask:latest

I created a docker- compose file to combine two images created as well as added postgres and dynamoDB service docker-compose file

[docker-compose.yml](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/docker-compose.yml)

I ran the docker-compose file to ensure both apps run and can talk to each other

docker compose -f "docker-compose.yml" up -d --build 


I also added persistent data storage in docker-compose file by adding volumes for backend

volumes:
      - ./backend-flask:/backend-flask
