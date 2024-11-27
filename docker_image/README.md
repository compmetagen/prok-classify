# Update dockerfile of gtdbtk

#### Enter docker image and test for presence of skani
```
docker run -it anitagat/gtdbtk:2.4.0
which skani
```
**update Dockerfile: ENV PATH="/root/.cargo/bin:${PATH}"**

#### Now build docker image from Dockerfile
```
docker build -t anitagat/gtdbtk:2.4.0 .
```

#### Load docker image on Dockerhub
```docker login
docker tag anitagat/gtdbtk:2.4.0 anitagat/gtdbtk:2.4.0
docker push anitagat/gtdbtk:2.4.0
```

#### Pull image with singularity to make singularity img
```
singularity pull docker://anitagat/gtdbtk:2.4.0
```

#### Check that skani is within singularity image
```
singularity exec gtdb_2.4.0.img which skani
```

#### Once image is cached, it can be used by nextflow, when referenced in the process.config file. 
