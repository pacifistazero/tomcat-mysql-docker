# tomcat-mysql-docker

This Docker Compose is use to build MYSQL and TOMCAT
Each folder contains a Dockerfile for each docker image

# Folder structure 
.
├── README
├── docker-compose.yml
├── mysql
│   ├── Dockerfile
│   ├── mysql-datadir
│   ├── setup-mysql.sh
│   └── start-mysqld.sh
└── tomcat
    ├── Dockerfile
    └── tomcat-users.xml

# How to build
docker-compose up -d