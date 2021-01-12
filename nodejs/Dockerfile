FROM node:13
WORKDIR /usr/src/app
RUN npm config set package-lock false
RUN npm install express express-handlebars mongoose body-parser mysql mysql2 ejs --save
RUN npm install -g nodemon
RUN npm init -y
COPY . /usr/src/app
CMD ["node", "index.js"]
EXPOSE 3000