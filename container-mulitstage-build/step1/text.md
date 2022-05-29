




## Mulitstage Docker file
The  multistage dockerfile combines 2 in one. 
The second part uses the assets from the first by in a COPY --from directive.
This helps executable keep the image small.

### Create the dockerfile
Execute the following, to create the dockerfile, the hello world programm was 
prepared for you before.

```
cat > Dockerfile << EOF
FROM golang:1.16 as builder
WORKDIR /go/src/
RUN go mod init main
COPY main.go ./
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /go/src/app ./
CMD ["./app"]  

EOF
```{{exec}}


### Build file
Now let's build our image
`docker build -t hurzelpurzel/hello-world:latest .`{{exec}}

### Check size
You should see the tiny size of our already built image, compared to the golang image containing all the build tools, when you list the images.

`docker images `{{exec}}

### Run the image
Check the Hello World out put
`docker run hurzelpurzel/hello-world:latest`