启动：
`docker run -it --rm --name pintos --mount type=bind,source=D:\VSCodeProject\pintos,target=/home/PKUOS/pintos pkuflyingpig/pintos bash`

`cd pintos/src/threads/build`

gdb启动pintos：
`pintos --gdb`

新shell：
`docker exec -it pintos bash`
`cd pintos/src/threads/build`
`pintos-gdb kernel.o`
`debugpintos`