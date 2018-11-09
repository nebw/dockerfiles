# dockerfiles

# build example
```
docker build - -build-arg UID =$(id - u) - -build-arg GID =$(id - g) - -build-arg UNAME =`whoami` - t deep-arch .
```

# run example
```
docker run - -runtime = nvidia - -net = "host" - ti - v / home/: / home / --rm deep-arch jupyter notebook --port=45000
```
