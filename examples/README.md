## buildah

dnf -y install buildah passt podman

buildah rm -all  

buildah from centos  
buildah images  
buildah containers  

buildah run centos-working-container yum install httpd -y  
echo "Hello from Red Hat" > index.html  
buildah copy centos-working-container index.html /var/www/html/index.html  
buildah config --entrypoint "/usr/sbin/httpd -DFOREGROUND" centos-working-container  
buildah config --port 8080 centos-working-container  
buildah commit centos-working-container httpd-one
buildah inspect <image> | jq '.OCIv1.config'  

podman run --name httpd-one -d -p 8080:80 localhost/httpd-one  

```
$ cat containerfile

FROM centos:latest
RUN dnf -y install httpd
COPY index.html /var/www/html/index.html
EXPOSE 8080
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]


$ buildah bud -f containerfile -t httpd-one

```



