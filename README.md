# test
test
#include<stdio.h>
#include<math.h>
#include<stdlib.h>
#define max 32

void addition(int a[max][max],int b[max][max],int n,int c[max][max]);
void mul(int a[max][max],int b[max][max],int c[max][max],int n);
void strassen(int a[max][max],int b[max][max],int c[max][max],int n);

void strassen2(int a[max][max],int b[max][max],int c[max][max]);
void substraction(int a[max][max],int b[max][max],int n,int c[max][max]);
int count1,count2;


void main()
{
 int n,a[max][max],b[max][max],c[max][max],a1,a2,a3,a4,b1,b2,b3,b4,m1[max][max],m2[max][max],m3[max][max],m4[max][max],m5[max][max],m6[max][max],m7[max]   [max],i,j,k,temp1[max][max],temp2[max][max],n1,s;

 printf("\nPlease Enter size  square martix A (n) : ");
 scanf("%d",&n1);

s=1;i=0;
while(1)
{
	s*=2;
	i++;
	if(s>=n1)
	break;
}
n=s;


for(i=0;i<n;i++)
{
	for(j=0;j<n;j++)
		a[i][j]=0;
  	printf("\n");
}

 printf("\nPlease Enter Elements of %d*%d matrix A  : ",n1,n1);

 for(i=0;i<n1;i++)
   for(j=0;j<n1;j++)
	 {
	 	scanf(" %d",&a[i][j]);
	 }//for

 printf("\nMatrix A  :: \n");
 for(i=0;i<n;i++)
  {
 	for(j=0;j<n;j++)
	{
		printf(" %d ",a[i][j]);
	}//for
   printf("\n");
  }

 printf("\nPlease Enter Elements of %d*%d matrix B  : ",n1,n1);

 for(i=0;i<n1;i++)
	for(j=0;j<n1;j++)
	{
		scanf(" %d",&b[i][j]);
	}//for


 printf("\nMatrix B  :: \n");

 for(i=0;i<n;i++)
 {
	for(j=0;j<n;j++)
	{
		printf(" %d ",b[i][j]);
	}//for
 printf("\n");
 }

 mul(a,b,c,n);
 printf("\nMultipication By Bruteforce Method ::  \n");
 for(i=0;i<n;i++)
 {
	for(j=0;j<n;j++)
	{
		printf(" %d ",c[i][j]);
	 }//for
  printf("\n");
 }//for
 printf("\nNumber Of Basic Operations Performed In Bruteforce Method ::  %d",count1);



 strassen(a,b,c,n);
 printf("\nMultipication By Strassen's  Method ::   \n");
 for(i=0;i<n1;i++)
 {
	for(j=0;j<n1;j++)
	{
		printf(" %d ",c[i][j]);
	 }//for
  printf("\n");
 }//for
printf("\nNumber Of Basic Operations Performed In Strssen's Method::  %d",count2);

}//main


void addition(int a[max][max],int b[max][max],int n,int c[max][max])
{
 int i,j,k;
 	for(i=0;i<n;i++)
 	{
 		for(j=0;j<n;j++)
 		{
 			c[i][j]=a[i][j]+b[i][j];
		}
 	}
}//add

void substraction(int a[max][max],int b[max][max],int n,int c[max][max])
{
 int i,j,k;

 for(i=0;i<n;i++)
 {
 	for(j=0;j<n;j++)
 	{
 		c[i][j]=a[i][j]-b[i][j];
	}
 }
}//add

void mul(int a[max][max],int b[max][max],int c[max][max],int n)
{
 int i,j,k;

 for(i=0;i<n;i++)
	for(j=0;j<n;j++)
 	{
	 	c[i][j]=0;
		for(k=0;k<n;k++)
		{			
			c[i][j]+=a[i][k]*b[k][j];
			count1++;
		}        
	}
}

void strassen(int a[max][max],int b[max][max],int c[max][max],int n)
{
int i,j,k,c1[max][max],c2[max][max],c3[max][max],c4[max][max],temp1[max][max],temp2[max][max],m1[max][max],m2[max][max],m3[max][max],m4[max][max],m5[max][max],m6[max][max],m7[max][max];
int a00[max][max],a01[max][max],a10[max][max],a11[max][max],b00[max][max],b01[max][max],b10[max][max],b11[max][max];
count2++;

if(n==1)
{
	c[0][0]=a[0][0]*b[0][0];
	return;
}

else
{

	for(i=0;i<n/2;i++)
	{
		for(j=0;j<n/2;j++)
		{
			a00[i][j]= a[i][j];
			a01[i][j]= a[i][j+n/2];
			a10[i][j]= a[i+n/2][j];
			a11[i][j]= a[i+n/2][j+n/2];
			b00[i][j]= b[i][j];
			b01[i][j]= b[i][j+n/2];
			b10[i][j]= b[i+n/2][j];
			b11[i][j]= b[i+n/2][j+n/2];
		}
	}

	//m1			
	addition(a00,a11,n/2,temp1);
	addition(b00,b11,n/2,temp2);
	strassen(temp1,temp2,m1,n/2);
	
	//printf("\n m1=%d",m1[0][0]);
	//m2
	addition(a10,a11,n/2,temp1);
	strassen(temp1,b00,m2,n/2);
	
	//printf("\n m2=%d",m2[0][0]);
	
	//m3
	substraction(b01,b11,n/2,temp1);
	strassen(a00,temp1,m3,n/2);
	
	//printf("\n m3=%d",m3[0][0]);
	//m4
	substraction(b10,b00,n/2,temp1);
	strassen(a11,temp1,m4,n/2);
	//printf("\n m4=%d",m4[0][0]);
	
	//m5
	addition(a00,a01,n/2,temp1);
	strassen(temp1,b11,m5,n/2);
	//printf("\n m5=%d",m5[0][0]);
	
	//m6
	substraction(a10,a00,n/2,temp1);
	addition(b00,b01,n/2,temp2);
	strassen(temp1,temp2,m6,n/2);
	
	//printf("\n m6=%d",m6[0][0]);
	
	//m7
	substraction(a01,a11,n/2,temp1);
	addition(b10,b11,n/2,temp2);
	strassen(temp1,temp2,m7,n/2);
	
	//c00
	addition(m1,m4,n/2,temp1);
	substraction(temp1,m5,n/2,temp2);
	addition(temp2,m7,n/2,c1);
	
	//cmax
	addition(m2,m4,n/2,c2);
	

	//c01
	addition(m3,m5,n/2,c3);
	
	
	//c11
	addition(m1,m3,n/2,temp1);
	substraction(temp1,m2,n/2,temp2);
	addition(temp2,m6,n/2,c4);
	

	for(i=0;i<n/2;i++)
	{
		for(j=0;j<n/2;j++)
		{
			c[i][j]=c1[i][j];
			c[i+n/2][j]=c2[i][j];
			c[i][j+n/2]=c3[i][j];
			c[i+n/2][j+n/2]=c4[i][j];
		}
	}
	
}//else

 return;
}//strassen




