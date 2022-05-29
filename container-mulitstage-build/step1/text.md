




### Mulitstage Docker file
The  multistage dockerfile combines 2 in one. 
The second part uses the assets from the first by in a COPY --from directive.
This helps executable keep the image small.

```
cat > Dockerfile << EOF
FROM golang:1.16 as builder
WORKDIR /go/src/
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
`docker build -t hurzelpurzel/hello-world:latest .`{{exec}}