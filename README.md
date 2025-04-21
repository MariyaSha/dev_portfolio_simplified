# dev_portfolio_simplified
Customizable Professional Developer Portfolio for Beginners with Docker Stack

## Video Tutorial
This repository was created as a resource for my <a href="https://youtu.be/RZpMevjnLR8">YouTube tutorial</a>.
<a href="https://youtu.be/RZpMevjnLR8"><img src="https://github.com/user-attachments/assets/d32f32b1-a656-41ab-affd-5d58415d5023" width=600px></a>

## Instructions
### 🏠 Develop Locally 🏠
1. Run your app and view it in your browser @ `localhost` or `localhost:80`:
```
cd dev_portfolio_simplified
docker compose up
```
2. update `init_db.py` with your personal information and projects.
3. update `static/style.css` with your favourite styling.
4. update `static/script.js` with your JavaScript browser intercations. 
5. saving each of the above files, and refreshing the web page - will automatically update your website locally.

### 🚀 Publish on a Remote Server 🚀
1. switch to a production server like Green Unicorn, by updating your Dockerfile:
```
FROM python:3.12-slim
WORKDIR /app
RUN pip install flask
RUN pip install gunicorn
COPY . .
CMD ["gunicorn", "--workers=5", "--bind", "0.0.0.0:5000", "main:app"]
```
2. pre-build a Docker image, to later specify it in your docker-compose file:
```
docker build -t my-portfolio .
```
3. update docker-compose file with the pre-build image:
```
services:
  web:
    image: my-portfolio:latest
    ports:
      - "80:5000"
    volumes:
      - ./:/app
    deploy:
      restart_policy:
        condition: any

  updater:
    image: my-portfolio:latest
    command: ["tail", "-f", "/dev/null"]
    volumes:
      - ./:/app
    deploy:
      restart_policy:
        condition: any
```
4. activate swarm more and deploy the GUI and database services in a stack:
```
docker build -t my-portfolio .
docker swarm init
docker stack deploy -c docker-compose.yml my-portfolio
```
5. update `init_db.py` and save it.
6. find container id of the database updater service with: `docker ps`
7. update database service without collapsing the application
```
docker exec [CONTAINER ID GOES HERE] python3 /app/init_db.py
```
## 💵 Coupon Code 💵
For 10% off on your VPS plan please navigate to: 
<br>
http://hostinger.com/pythonsimplified
<br>
And enter the coupon code: 
<br>
PYTHONSIMPLIFIED

## Further Learning
If you're not sure what Flask is, or why do we need Docker, or how on earth do we work with SQLite, please checkout the following learning resources on YouTube to get you up to speed:
<br>
<br>
⭐ Simple Hello World Web App with Flask:
    <br>    https://youtu.be/6plVs_ytIH8
    <br>
⭐ Introduction to SQLite:
    <br>    https://youtu.be/Ohj-CqALrwk
    <br>
⭐ Advanced Web App with Flask, and SQLite:
    <br>    https://youtu.be/v3CSQkPJtAc
    <br>
⭐ Introduction to Docker:
    <br>    https://youtu.be/-l7YocEQtA0
