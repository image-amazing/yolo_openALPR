
CPP=g++
CC=gcc
SOURCES=src/main.cpp src/post.cpp src/cJSON.c
OBJECTS=$(SOURCES:.cpp=.o)
EXECUTABLE=lprecognizer

OPTS=-Ofast
LDFLAGS= -lm -pthread -L../darknet -l:nn.so -l:libopenalpr.so
COMMON= -std=c++11
CFLAGS= -Wall -Wfatal-errors -Wno-unused-result -Wno-unknown-pragmas 
CFLAGS+=$(OPTS) 

#cURL
COMMON+= `pkg-config --cflags libcurl`
LDFLAGS+= `pkg-config --libs libcurl`

#OpenCV
CFLAGS+= -DOPENCV
LDFLAGS+= `pkg-config --libs opencv` 
COMMON+= `pkg-config --cflags opencv` 

DEPS = $(wildcard src/*.hpp) Makefile

CFLAGS+= -fPIC
LDFLAGS+= -Wl,-rpath='$$ORIGIN'
INCLUDES=-I /usr/include -I ../darknet/src -I ./src

all: $(SOURCES) $(EXECUTABLE)
	 
$(EXECUTABLE): $(OBJECTS) 
	$(CPP) $(OBJECTS) -o $@ $(COMMON) $(LDFLAGS)
	
src/cJSON.o: src/cJSON.c 
	$(CC) $(OPTS) -c src/cJSON.c -o $@ 
	
src/post.o: src/post.cpp 
	$(CPP) $(COMMON) $(CFLAGS) $(INCLUDES) -c src/post.cpp -o $@ 

src/main.o: src/main.cpp
	$(CPP) $(COMMON) $(CFLAGS) $(INCLUDES) -c src/main.cpp -o $@ 

clean:
	rm -rf src/*.o $(EXECUTABLE)