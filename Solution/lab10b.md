# Solution to Lab10b

## 2. Getting started with Docker

### 2. Running an interactive container

1. "root"

2. No they are not, because their hash are different.

### 3. Dockerfiles

1. ```
   .___  ___.  __       _______.     _______. __   __       _______  __  
   |   \/   | |  |     /       |    /       ||  | |  |     |   ____||  | 
   |  \  /  | |  |    |   (----`   |   (----`|  | |  |     |  |__   |  | 
   |  |\/|  | |  |     \   \        \   \    |  | |  |     |   __|  |  | 
   |  |  |  | |  | .----)   |   .----)   |   |  | |  `----.|  |____ |__| 
   |__|  |__| |__| |_______/    |_______/    |__| |_______||_______|(__) 
   ```

2. ```dockerfile
   FROM ubuntu:bionic
   
   RUN apt-get update && apt-get install -y fortune fortunes-min
   
   CMD ["/usr/games/fortune"]
   ```

3. ```
   REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
   missile      latest    197623691695   3 minutes ago   562MB
   fortune      latest    4ab7fc53f760   13 hours ago    112MB
   ```

### 4. Dockerizing a Web Server

1. ```
   CONTAINER ID   IMAGE     COMMAND              CREATED              STATUS              PORTS                                   NAMES
   0d22c63ba061   httpd     "httpd-foreground"   18 seconds ago       Up 17 seconds       0.0.0.0:4002->80/tcp, :::4002->80/tcp   amazing_feistel
   9774e2d61064   httpd     "httpd-foreground"   23 seconds ago       Up 22 seconds       0.0.0.0:4001->80/tcp, :::4001->80/tcp   dreamy_johnson
   b2cb1bf8fe6a   httpd     "httpd-foreground"   About a minute ago   Up About a minute   0.0.0.0:4000->80/tcp, :::4000->80/tcp   epic_johnson
   ```

2. One image can be used to create multiple containers. Each container should have their own distinguished name.

3. `docker stop b2`

## 3. Getting started with Puppet (optional)

```
package { 'curl':
  ensure => present,
}

group { 'quotegather':
  ensure => 'present',
}

user { 'quotes':
  ensure => 'present',
  gid    => 'quotegather',
  home   => '/tmp',
  shell  => '/bin/false',
  require => Group['quotegather'],
}

cron { 'getquote':
  user    => 'quotes',
  command => "curl 'https://api.kanye.rest/?format=text' >> /tmp/quotes && echo >> /tmp/quotes",
  minute  => '*/2',
}
```

**Tip**: you may need to set envrionment vairable `"PATH=$PATH"` when executing the `puppet apply` command using `sudo env "PATH=$PATH" puppet apply quotes.pp`, since `sudo` overwrite `"$PATH"` to "secure_path" which may not include your `puppet` module directory. You can see your "secure_path" in `visudo` using `sudo visudo`.
