# What is ROSE Compiler Infrastructure ?
>"ROSE is an open source compiler infrastructure to build source-to-source program transformation and analysis tools for large-scale C (C89 and C98), C++ (C++98 and C++11), UPC, Fortran (77/95/2003), OpenMP, Java, Python and PHP applications. [(***http://rosecompiler.org/***)](http://rosecompiler.org/)"

---

# about this image
* CentOS 6.9 where ROSE compiler Framework installed  
* ROSE compiler installed @ `/opt/rose`  
* Boost installed @ `/opt/boost-1.54`  
* Environment variable setting file @ `/opt/rose/setPATH.sh`
* Common server environment variable setting file @ `/etc/profile.d/rose.sh`  

###### /opt/rose/setPATH.sh  
```
   export JAVA_HOME=`readlink /etc/alternatives/java_sdk_openjdk`
   export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/rose/lib:/opt/boost-1.54/lib:${JAVA_HOME}/lib:${JAVA_HOME}/jre/lib/amd64/server
   export C_INCLUDE_PATH=$C_INCLUDE_PATH:/opt/rose/include/rose:/opt/boost-1.54/include
   export CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:/opt/rose/include/rose:/opt/boost-1.54/include
   export PATH=$PATH:/opt/rose/bin
```

###### /etc/profile.d/rose.sh
```
   source /opt/rose/setPATH.sh  
```  

---

# Notes
## At build from Dockerfile
* RAM：8 GB or more (required)  
* Virtual storage area：20GB or more (recommendation)
* Required time：About 1 - 2 hours  

## build  
```sh:console
 sudo docker build -t sin1/rose_compiler .  
```

## run
```sh:console
 sudo docker run -itd --name rose sin1/rose_compiler
```

## Expansion of virtual storage area
 The following operations are required before "docker build"  

##### console
```sh:console
 sudo service docker stop
 vi /etc/sysconfig/docker
 sudo service docker start
```

##### /etc/sysconfig/docker
```sh:/etc/sysconfig/docker
# Modify these options if you want to change the way the docker daemon runs
OPTIONS=--storage-opt dm.basesize=20G --selinux-enabled -H fd://
```

---

# Software dependencies
| Software component | version |
|:-----------|:------------|
|rose compiler |    xevolver/rose-xev  (based ROSE ver.0.9.7.20) <br> [commit e4bd48887e23a8f0f8910f1f6fb88dc6d7302b56](https://github.com/xevolver/rose-xev/commit/e4bd48887e23a8f0f8910f1f6fb88dc6d7302b56) |
|git           |  1.7.1|
|wget       |     1.12|
|gcc        |     4.4.7|
|autoconf   |     2.69|
|automake |       1.15.1|
|libtool        | 2.4.6|
|flex           | 2.5.35|
|bison        |   2.4.1|
|yacc         |   1.9|
|jdk            |java-1.7.0-openjdk-1.7.0.141.x86_64|
|python      |    2.6.6|
|boost        |   1_54_0|
|bzip2        |   1.0.6|
|zlib           | 1.2.11|
|ghostscript |    8.70|
|doxygen     |    1.6.1 |
|graphviz     |   2.26 |
|CentOS | Mounted from [library/centos:6.9](https://github.com/CentOS/sig-cloud-instance-images/blob/4f329fe087b0152df26344cecee9ba30b03b1a7b/docker/Dockerfile) |

---

# References
* ROSE compiler infrastructure -- http://rosecompiler.org/
* Boost C++ Libraries -- http://www.boost.org/
