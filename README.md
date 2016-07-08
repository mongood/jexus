# jexus/mono:latest
Just for automaked docker image - jexus/mono:latest

Usage(使用方法，注意数据卷的映射必须是绝对路径) :

    docker run -d -p hostport:80 -v /project-full-path:/var/www/default --restart always jexus/mono:latest

Example(示例，$(pwd)/project表示当前路径下的项目文件夹) :

    docker run -d -p 9527:80 -v $(pwd)/project:/var/www/default --restart always jexus/mono:latest

Dockerfile(替换jexus的默认配置文件) :

    FROM jexus/mono:latest
    MAINTAINER Mongo willem@xcloudbiz.com
    COPY default /usr/jexus/siteconf/default

Build image([:tag]标签可加可不加，不加则默认为latest。不要忘记结尾的“.”，其实是指Dockerfile文件的相对路径) :

    docker build -t new_image_name[:tag] .
Example(例如) :

    docker build -t new_jexus_mono:latest

The default file content,Edit the default file according to your own situation(jexus默认站点配置文件，请根据自己的情况进行修改) :

    ######################
    # Web Site: Default
    # 默认站点的配置，如果修改/var/www/default，那么在做数据卷映射的时候要同步修改。例如：
    # root=/ /var/www/example
    # docker run -d -p hostport:80 -v /project-full-path:/var/www/example--restart always jexus/mono:latest
    ########################################
    
    port=80
    root=/ /var/www/default
    hosts=*    #OR your.com,*.your.com
    
    # addr=0.0.0.0
    # CheckQuery=false
    NoLog=true
    # AppHost.Port=5000
    # NoFile=/index.aspx
    # Keep_Alive=false
    # UseGZIP=false
    # UseHttps=true
    # DenyFrom=192.168.0.233, 192.168.1.*, 192.168.2.0/24
    # AllowFrom=192.168.*.*
    # DenyDirs=~/cgi, ~/upfiles
    # indexes=myindex.aspx
    # rewrite=^/.+?\.(asp|php|cgi|pl|sh)$ /index.aspx
    # reproxy=/bbs/ http://192.168.1.112/bbs/
    # host.Redirect=abc.com www.abc.com  301
    # ResponseHandler.Add=myKey:myValue
    
    # Jexus php fastcgi address is '/var/run/jexus/phpsvr'
    #######################################################
    # fastcgi.add=php|socket:/var/run/jexus/phpsvr
    
    # php-fpm listen address is '127.0.0.1:9000'
    ############################################
    # fastcgi.add=php|tcp:127.0.0.1:9000
