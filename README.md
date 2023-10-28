# OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS

## AIM:
To write a program for the first come first serve method of disc scheduling.

## DESCRIPTION: 
Disk scheduling is schedule I/O requests arriving for the disk. 
It is important because: - 
Multiple I/O requests may arrive by different processes and only one I/O request can be served at a time 
by the disk controller. Thus other I/O requests need to wait in the waiting queue and need to be 
scheduled. 
Two or more request may be far from each other so can result in greater disk head movement. 
Hard drives are one of the slowest parts of the computer system and thus need to be accessed in an 
efficient manner 
 
FCFS is the simplest of all the Disk Scheduling Algorithms. In FCFS, the requests are addressed in the 
order they arrive in the disk queue. 
 
Example: Given the following queue -- 95, 180, 34, 119, 11, 123, 62, 64 with the Read-write head 
initially at the track 50 and the tail track being at 199. 

## PROGRAM:
```
#include <stdio.h> 
#include <stdlib.h> 
int main() 
{ 
int RQ[100],i,n,TotalHeadMoment=0,initial; 
printf ("Enter the number of Requests\n"); 
scanf("%d",&n); 
printf("Enter the Requests sequence\n");
for(i=0;i<n;i++) 
scanf("%d",&RQ[i]); 
printf("Enter initial head position\n"); 
scanf("%d",&initial); 
for(i=0;i<n;i++) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
 
printf("Total head moment is %d",TotalHeadMoment); 
return 0; 
 
}
```

## OUTPUT:
![fcfs](https://github.com/Divya110205/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/119404855/d8bcbdcf-c13d-451c-94de-60fdf5c7192a)

## RESULT:
Thus the implementation of the program for first come first serve disc scheduling has been 
successfully executed.

## AIM:
To write a program for the shortest seek time first method of disc scheduling.

## DESCRIPTION: 
Shortest seek time first (SSTF) algorithm 
 
Shortest seek time first (SSTF) algorithm selects the disk I/O request which requires the least disk arm 
movement from its current position regardless of the direction. It reduces the total seek time as compared 
to FCFS. 
 
Example:-: Given the following queue -- 95, 180, 34, 119, 11, 123, 62, 64 with the Read-write head 
initially at the track 50 and the tail track being at 199. 

## PROGRAM:
```
#include<stdio.h> 
#include<stdlib.h> 
int main() 
{ 
int RQ[100],i,n,TotalHeadMoment=0,initial,count=0; 
printf("Enter the number of Requests\n"); 
scanf("%d",&n); 
printf("Enter the Requests sequence\n"); 
for(i=0;i<n;i++) 
scanf("%d",&RQ[i]); 
printf("Enter initial head position\n"); 
scanf("%d",&initial); 
while(count!=n) 
{ 
int min=1000,d,index; 
for(i=0;i<n;i++) 
{ 
d=abs(RQ[i]-initial); 
if(min>d) 
{ 
min=d; 
index=i; 
} 
} 
TotalHeadMoment=TotalHeadMoment+min; 
initial=RQ[index]; 
RQ[index]=1000; 
count++; 
} 
printf("Total head movement is %d",TotalHeadMoment); 
return 0; 
}
```

## OUTPUT:
![sstf](https://github.com/Divya110205/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/119404855/ac9ccd4a-ce52-4705-87e7-d3f4492400ad)

## RESULT:
Thus the implementation of the program for shortest seek time first disc scheduling has been 
successfully executed. 

## AIM:
To write a program for the SCAN method of disc scheduling.

## DESCRIPTION: 
 
It is also called as Elevator Algorithm. In this algorithm, the disk arm moves into a particular direction 
till the end, satisfying all the requests coming in its path, and then it turns backend moves in the reverse 
direction satisfying requests coming in its path. 
 
It works in the way an elevator works, elevator moves in a direction completely till the last floor of that 
direction and then turns back. 
 
Example:- Given the following queue -- 95, 180, 34, 119, 11, 123, 62, 64 with the Read-write head 
initially at the track 50 and the tail track being at 199. head movement is towards low value. 

## PROGRAM:
```
#include<stdio.h> 
#include<stdlib.h> 
int main() 
{ 
int RQ[100],i,j,n,TotalHeadMoment=0,initial,size,move; 
printf("Enter the number of Requests\n"); 
scanf("%d",&n); 
printf("Enter the Requests sequence\n"); 
for(i=0;i<n;i++) 
scanf("%d",&RQ[i]); 
printf("Enter initial head position\n"); 
scanf("%d",&initial); 
printf("Enter total disk size\n");
scanf("%d",&size); 
printf("Enter the head movement direction for high 1 and for low 0\n"); 
scanf("%d",&move); 
for(i=0;i<n;i++) 
{ 
for(j=0;j<n-i-1;j++) 
{ 
if(RQ[j]>RQ[j+1]) 
{ 
int temp; 
temp=RQ[j]; 
RQ[j]=RQ[j+1]; 
RQ[j+1]=temp; 
} 
} 
} 
int index; 
for(i=0;i<n;i++) 
{ 
if(initial<RQ[i]) 
{ 
index=i; 
break; 
} 
} 
if(move==1) 
{ 
for(i=index;i<n;i++) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
// last movement for max size 
TotalHeadMoment=TotalHeadMoment+abs(size-RQ[i-1]-1); 
initial = size-1; 
for(i=index-1;i>=0;i--) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
} 
else 
{ 
for(i=index-1;i>=0;i--) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i+1]-0); 
initial =0; 
for(i=index;i<n;i++) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
} 
printf("Total head movement is %d",TotalHeadMoment); 
return 0; 
}
```

## OUTPUT:
![scan](https://github.com/Divya110205/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/119404855/efedf039-a53f-46f4-b0f8-604431e3beb8)

## RESULT:
Thus the implementation of the program for SCAN disc scheduling has been successfully executed. 

## AIM:
To write a program for the LOOK method of disc scheduling. 

## DESCRIPTION 

It is similar to the SCAN disk scheduling algorithm except for the difference that the disk arm in spite of 
going to the end of the disk goes only to the last request to be serviced in front of the head and then 
reverses its direction from there only. Thus, it prevents the extra delay which occurred due to unnecessary 
traversal to the end of the disk. 

## PROGRAM:
```
#include<stdio.h> 
#include<stdlib.h> 
int main() 
{ 
int RQ[100],i,j,n,TotalHeadMoment=0,initial,size,move; 
printf("Enter the number of Requests\n"); 
scanf("%d",&n); 
printf("Enter the Requests sequence\n"); 
for(i=0;i<n;i++) 
scanf("%d",&RQ[i]); 
printf("Enter initial head position\n"); 
scanf("%d",&initial); 
printf("Enter total disk size\n"); 
scanf("%d",&size); 
printf("Enter the head movement direction for high 1 and for low 0\n"); 
scanf("%d",&move); 
for(i=0;i<n;i++) 
{
    for(j=0;j<n-i-1;j++) 
{ 
if(RQ[j]>RQ[j+1]) 
{ 
int temp; 
temp=RQ[j]; 
RQ[j]=RQ[j+1]; 
RQ[j+1]=temp; 
} 
} 
} 
int index; 
for(i=0;i<n;i++) 
{ 
if(initial<RQ[i]) 
{ 
index=i; 
break; 
} 
} 
if(move==1) 
{ 
for(i=index;i<n;i++) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
for(i=index-1;i>=0;i--) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
} 
else 
{ 
for(i=index-1;i>=0;i--) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
for(i=index;i<n;i++) 
{ 
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial); 
initial=RQ[i]; 
} 
} 
printf("Total head movement is %d",TotalHeadMoment); 
return 0; 
} 
```
## OUTPUT:
![look](https://github.com/Divya110205/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/119404855/0f93f527-d446-4e25-9527-d554f1d84647)

## RESULT:
Thus the implementation of the program for LOOK disc scheduling has been successfully executed.
