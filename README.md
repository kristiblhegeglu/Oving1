Sanntidsprosjekt_2014

Oving1
======

Python

# Python 3.3.3 and 2.7.6
# python helloworld_python.py

from threading import Thread, Lock

i = 0



def adder():
    global i
    for x in range(0, 1000000):
        i += 1

        
def subtractor():
	
    global i
    for x in range(0,1000000):
        i -= 1


def main():
    adder_thr = Thread(target = adder)
    subtractor_thr = Thread(target = subtractor)
    adder_thr.start()    
    subtractor_thr.start()
	    
    for x in range(0, 50):
        print(i)
        adder_thr.join()
        adder_thr.join()
	    
        print("Done: " + str(i))


main()


Go

package main

import (
    . "fmt" // Using '.' to avoid prefixing functions with their package names
    . "runtime" // This is probably not a good idea for large projects...
    . "time"
)

var i = 0

func adder() {
	for x := 0; x < 1000000; x++ {
		i++
		}
	}

func subtract() {
	for x := 0; x < 1000000; x++ {
		i++
		}
	}


func main() {
	GOMAXPROCS(NumCPU()) // I guess this is a hint to what GOMAXPROCS does...
	go adder() // This spawns adder() as a goroutine
	go subtract()
	for x := 0; x < 50; x++ {
	Println(i)
	}
    // No way to wait for the completion of a goroutine (without additional syncronization)
    // We'll come back to using channels in Exercise 2. For now: Sleep
	Sleep(100*Millisecond)
	Println("Done:", i);
}



C

#include <pthread.h>
#include <stdio.h>

int i = 0;

// Note the return type: void*
void* adder(){
    for(int x = 0; x < 1000000; x++){
        i++;
    }
    return NULL;
}

void* subtract(){
    for(int x = 0; x < 1000000; x++){
        i--;
    }
    return NULL;
}


int main(){
    pthread_t adder_thr;
    pthread_t subtract_thr;
    pthread_create(&adder_thr, NULL, adder, NULL);
    pthread_create(&subtract_thr, NULL, subtract, NULL);
    for(int x = 0; x < 50; x++){
        printf("%i\n", i);
    }

    
    pthread_join(adder_thr, NULL);
    pthread_join(subtract_thr, NULL);
    printf("Done: %i\n", i);
    return 0;
    
}

