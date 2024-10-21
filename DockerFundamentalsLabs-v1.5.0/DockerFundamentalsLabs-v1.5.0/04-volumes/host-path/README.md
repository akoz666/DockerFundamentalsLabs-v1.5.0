## Docker Fundamentals labs v1.5.0

#####
---- Lab use Host mounted volume
---- Hello World

##HelloWorld.js
console.log(‘Hello World’);

$ docker run –v “$PWD”:/usr/src/app  –w /usr/src/app node node HelloWorld.js