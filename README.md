#include<stdio.h>
#include<conio.h>
//global variable declaration
int bt[20],p[20],waitingtime[20],turnaroundtime[20],count[20],at[20],no_of_process,flagat,temp,temp1,temp2,sum=0,i,j,u;
float priority,avgwt=0,avgtt=0;
//sorting of process with their burstime(bt) and arrivaltime(at) using arrivaltime(at)
void sortingat()
{
	for(i=1;i<no_of_process;i++)
    {
    	//arrivaltime sorting(at)
    	int temp=at[i];
    	int j=i-1;
    	while((temp<at[j])&&(j>=0))
    	{
    		at[j+1]=at[j];
    		j=j-1;
		}
		at[j+1]=temp;
	}
	//bursttime sorting(bt) but using arrival time
	for(i=1;i<no_of_process;i++)
    {
    	temp=bt[i];
    	j=i-1;
    	while((temp<bt[j])&&(j>=0))
    	{
    		bt[j+1]=bt[j];
    		j=j-1;
		}
		bt[j+1]=temp;
	}
	//process sorting wrt arrivaltime(at)
	for(i=1;i<no_of_process;i++)
    {
    	temp=p[i];
    	j=i-1;
    	while((temp<p[j])&&(j>=0))
    	{
    		p[j+1]=p[j];
    		j=j-1;
		}
		p[j+1]=temp;
	}
}

int main()
{
	//taking userinput for no of process and bursttime,arrival time for the same
 	printf("Enter number of processes:");
 	scanf("%d",&no_of_process);
 	for(i=0;i<no_of_process;i++)
 		{
 			printf("\nenter burst time of process %d:",i+1);
 			scanf("%d",&bt[i]);
 			printf("enter arrival time t of process %d:",i+1);
 			scanf("%d",&at[i]); 
 			count[i]=0;
 			sum+=bt[i];
		}
	//calling sorting fncn
	sortingat();
	
	printf("\narrival time\tBurst time\tWaiting time\tTurnaround time ");
  	for(flagat=at[0];flagat<sum;)
  		{
   			float r=-1;
   			int u;
  			for(i=0;i<no_of_process;i++)
  				{

   					if(at[i]<=flagat && count[i]!=1)
    					{
              				priority=(bt[i] + (flagat-at[i]))/bt[i];
              				if(r < priority)
               					{
                					r=priority;
                 					u=i;
               					}
          				}
  				}		
  
  
   			flagat+=bt[u]; 
    
   			waitingtime[u]=flagat-at[u]-bt[u];
   			turnaroundtime[u]=flagat-at[u];
    		count[u]=1;
   			avgwt+=waitingtime[u];
  			avgtt+=turnaroundtime[u];
			printf("\n%d\t\t%d\t\t%d\t\t%d",at[u],bt[u],waitingtime[u],turnaroundtime[u]);
  		}

	printf("\nAverage waiting time:%f\n",avgwt/no_of_process);
	printf("\nAverage turn around time:%f\n",avgtt/no_of_process);
	return 0;
}
