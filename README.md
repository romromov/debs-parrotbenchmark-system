# ACM DEBS Grand Challenge tutorial system

It is able to  pass DEBSParrotBenchmark. In order to do that it receives messages on `inputQueue` and sends all of them
except `TERMINATION_MESSAGE` to `outputQueue`. Receiving of the `TERMINATION_MESSAGE` on `inputQueue`
means no more followed messages. After the system has processed all the messages it must send `TERMINATION_MESSAGE` to
`outputQueue`. The termination message is just a value of string "\~~Termination Message\~~" encoded to bytes with UTF-8.

## Uploading system to the HOBBIT platform
In order to upload this system to the HOBBIT platfrom you need to do a few steps described below.

1. **Compile this code and build jar file.** Probably, the easiest way to do it is to exeute corresponding Maven taks
of this project.
2. **Build Docker image.** Put your jar file to the directory where you have Dockerfile. In my case, jar file is named
*debs-parrotbenchmark-system-1.0-SNAPSHOT.jar* and located under *[projcect root]/deploy* directory. Navigate to that
directory and execute the following command to buld Docker image: `docker build -t git.project-hobbit.eu:4567/<user name>/<image name> .`
In my case the command is `docker build -t git.project-hobbit.eu:4567/rkaterinenko/debsparrotsystemexample .` **Note! The last comma is required it is path to your current directory.**
3. **Upload the image to HOBBIT's gitlab.**  Login to gitlab: `docker login git.project-hobbit.eu:4567` and upload:
`docker push git.project-hobbit.eu:4567/rkaterinenko/debsparrotsystemexample`, in my case.
4. Put *system.ttl* directly to the root of you gitlab project.

You may have different names or steps, but the result should be docker image and 'system.ttl' uploaded to HOBBIT's gitlab.
These two things are enough for the HOBBIT platform to instatiate and run your system. In this repository under
you can find *[projcect root]/deploy* directory you can find example files that I use but you don't have to stick to them.

## Running the system locally

If you need to run your system locally then after you started HOBBIT platform and Rabbit MQ locally, you need to do
something like this:

`docker run --network="hobbit" --network="hobbit-core" --env-file ./env --name cont_name_debsparrotsystemexample git.project-hobbit.eu:4567/rkaterinenko/debsparrotsystemexample`
It does what the platform does with your image when instantiates Docker container from it:
- Attach to *hobbit* and *hobbit-core* networks
- Supply environment variables (in this example from *env* file.)
Supply of that environment variables is platform responcibility. You don't have to supply
them yourself. But if you want to run the system locally then you need to do that
because the system code check for their existence. In this case you can specify any valid
values to mentioned environment variables.
