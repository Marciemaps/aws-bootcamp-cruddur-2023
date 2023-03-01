# Week 1 — App Containerization

Homework Requirements:

I added a dockerfile

pip install -r requirements.txt
flask run

![Download Pip3](https://user-images.githubusercontent.com/95619710/222173436-78907378-09f2-49e4-915b-1c15b4df719a.png)


![Flask install](https://user-images.githubusercontent.com/95619710/222173535-4d6b0ce5-fea5-4656-9d48-ef573a2f60f6.png)


![Build Docker Files and Show Images](https://user-images.githubusercontent.com/95619710/222173670-47941497-08ff-4535-b647-11336374b26d.png)


npm install
npm start


I created a backend end point for notifications page

[[backend-flask/app.py]](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/backend-flask/app.py)

![Backend-Crudder](https://user-images.githubusercontent.com/95619710/222173874-819e6b72-6192-4fda-bbb5-7f50c0d8d896.png)


I created a frontend end point for notifications page

[[frontend-react-js/src/pages/NotificationPage.js]](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/frontend-react-js/src/pages/NotificationsFeedPage.js)


I created a Dockerfile for frontend and backend

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

I managed to create a docker-compose file to combine two images created as well as added postgres and dynamoDB service docker-compose file

[docker-compose.yml](https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/blob/main/docker-compose.yml)

I ran the docker-compose file to ensure both apps run and can talk to each other

![Crudder Notifications](https://user-images.githubusercontent.com/95619710/222174056-19d85c4c-cb2e-4390-8648-816480084843.png)


docker compose -f "docker-compose.yml" up -d --build 


I also added persistent data storage in docker-compose file by adding volumes for backend

volumes:
      - ./backend-flask:/backend-flask

https://github.com/Marciemaps/aws-bootcamp-cruddur-2023/issues/21#issue-1604941860    

![Database Connect](https://user-images.githubusercontent.com/95619710/222174117-9e560d54-8024-4f56-9e85-150e07bea057.png)

      
