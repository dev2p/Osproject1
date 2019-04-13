# Osproject1
#include<stdio.h>
    int need(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re]);
    int available(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re]);
int main()
{
    int n_p,n_re,m,i,j;
    printf("how many number of process and no. of resource for each process = ");
    scanf("%d %d",&n_p,&n_re);
    int res[n_p][n_re],maxres[n_p][n_re],needres[n_p][n_re];
    printf("enter the no. of instances allocated for process : ");
    printf("\n");
    for(i=0;i<n_p;i++)
    {
        printf("enter the value for P%d procces = ",i);
        for(j=0;j<n_re;j++)
        {
            scanf("%d",&m);
            res[i][j]=m;
        }
        printf("\n");
    }
    printf("enter the maximum no. of resource can allocate");
    printf("\n");
    for(i=0;i<n_p;i++)
    {
        printf("value for P%d procces = ",i);
        for(j=0;j<n_re;j++)
        {
            scanf("%d",&m);
            maxres[i][j]=m;
        }
        printf("\n");
    }
    need(n_p,n_re,needres,maxres,res);
 
     printf("                         aloocate\t maximum\t need");
     printf("\n");
        for(i=0;i<n_p;i++)
    {  
        printf("value for P%d procces = ",i);
        for(j=0;j<n_re;j++)
        {
        printf(" %d ",res[i][j]);
            }
        printf("\t");
        for(j=0;j<n_re;j++)
        {
            printf(" %d ",maxres[i][j]);
        }
        printf("\t");
            for(j=0;j<n_re;j++)
        {
            printf(" %d ",needres[i][j]);
        }
        printf("\n");
    }
}
int need(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re])
{
	int i=0,j=0;
   for(i=0;i<n_p;i++)
    {
        for(j=0;j<n_re;j++)
        {
            needres[i][j]=maxres[i][j]-res[i][j];
        }
    }
}
int available(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re])
{
 need(n_p,n_re,needres,maxres,res);
 printf("enter the available  instances of resource =");
 int avail[n_p],i;
 for(i=0;i<n_re;i++);
 {
 	scanf("%d",&avail[i]);
 }
 int get[n_p],cnt=0,j,k,f[n_p];
 for(i=0;i<n_p;i++)
 {
 	f[i]=0;
 }
 for(i=0;i<n_p;i++)
 {
 	for(j=0;j<n_re;j++)
 	{
 		if(f[i] == 0)
 		{
 			int flag =0;
 			if(avail[j]<needres[i][j])
 			{
 				flag =1;
 				break;
			 }
			 if(flag == 0)
			 {
			 	get[cnt++]=i;
			 	for(k=0;k<n_re;k++)
			 	{
			 		avail[k]=avail[k]+res[i][k];
			
				 }
				 f[i]=1;
			 }
		 }
	 }
 }
 if(cnt != n_p+1)
 {
 	printf("it is in deadlock");
 }
 for(i=0;i<n_p;i++)
 {
 	printf("P%d ->",get[i]);
 }
 	
}
request()
{
	char c;
	cout()
}
