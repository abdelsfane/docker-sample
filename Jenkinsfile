node {
  checkout scm
  
  stage("Create Dockerfile") {
      sh '''
      +x
      mkdir myapp && cd myapp && touch Dockerfile
      cat > Dockerfile <<'endmsg'
    FROM ubuntu:18.04
    MAINTAINER Faithful <faithful@infused.io>
    RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
    ENV APACHE_RUN_USER  www-data
    ENV APACHE_RUN_GROUP www-data
    ENV APACHE_LOG_DIR   /var/log/apache2
    ENV APACHE_PID_FILE  /var/run/apache2/apache2.pid
    ENV APACHE_RUN_DIR   /var/run/apache2
    ENV APACHE_LOCK_DIR  /var/lock/apache2
    ENV APACHE_LOG_DIR   /var/log/apache2
    RUN mkdir -p $APACHE_RUN_DIR
    RUN mkdir -p $APACHE_LOCK_DIR
    RUN mkdir -p $APACHE_LOG_DIR
    COPY index.html /var/www/html
    EXPOSE 80
    CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
    endmsg
    '''
  }
stage("Create HTML file") {
    sh '''
    +x
    touch index.html
    cat > index.html <<'endmsg'
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>First APP</title>
    </head>
    <body>
        <h1>People becoming Humans Again</h1>
    </body>
    </html>
    endmsg
    '''
    }
      stage("Docker Build") {
      sh '''
      docker build -t ubuntuc .
        '''
  }
  stage("Docker Run Container") {
      sh '''
      docker run --name my_ubuntu_instance -i -t ubuntuc
      ls
      whoami
      
        '''
  }
}
