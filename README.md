# Assignment
First Upload
//Program to add first thousand Numbers using threads

#include<stdio.h>
#include<stdlib.h>
#include<pthread.h>


void* SumArray(void* arg);

int arr[1000];


int main()
{
	int TotalSum=0;

	for(int i=0 ; i<1000 ; i=i+1)
	{
		arr[i]=i+1;
	}

	pthread_t Thread[10];
	
	for(int i=0 ; i<10 ; i=i+1)
	{
		pthread_create(&Thread[i] , NULL , SumArray , (void*)(i*100));
		
	}

	void* temp;
	for(int i=0 ; i<10 ; i=i+1)
	{
		
		pthread_join(Thread[i],&temp);

		TotalSum = TotalSum + (int)temp;
	}

	printf("Sum of First 1000 Numbers : %d\n",TotalSum);

	return 0;
}

void* SumArray(void* arg)
{
	int n = (int) arg;
	int sum=0;



	for(int i=n ; i<n+100 ; i=i+1)
	{
		sum = sum + arr[i];
	}
	return (void*)sum;
}
