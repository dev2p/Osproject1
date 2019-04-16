#include<stdio.h>
#include<stdbool.h>
const n_p;
const n_re;
    int need(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re]);
    void display(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re]);
    bool check(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re],int available[n_re]);
int main()
{
    int n_p,n_re,m,i,j;
    printf("how many number of process and no. of resource for each process = ");
    scanf("%d %d",&n_p,&n_re);
    int res[n_p][n_re],maxres[n_p][n_re],needres[n_p][n_re],available[n_re];
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
    int res_for_need;
    for(i=0;i<n_p;i++)
    {
        printf("value for P%d procces = ",i);
        for(j=0;j<n_re;j++)
        {
            scanf("%d",&res_for_need);
            maxres[i][j]=res_for_need;
        }
        printf("\n");
    }
    printf("enter the available  instances of resource =");
 
 for(i=0;i<n_re;i++)
 {
 	scanf("%d",&available[i]);
 }
    need(n_p,n_re,needres,maxres,res);
    display(n_p,n_re,needres,maxres,res);
    check(n_p,n_re,needres,maxres,res,available);
    request(n_p,n_re,needres,maxres,res,available);
}
void display(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re])
{
	int i,j;
	 printf("===========================================================================================\n");
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
    printf("==============================================================================================\n");
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
bool check(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re],int available[n_re]) 
{  
  need(n_p,n_re,needres,maxres,res); 
    bool end[n_p];
    int i;
    for(i=0;i<n_p;i++)
    {
    	end[i]=0;
	}
    int S[n_p]; 
    int work[n_re];
    for (i = 0; i < n_re ; i++)
	{ 
        work[i] = available[i]; 
}
    int cnt = 0; 
    printf("Intially Available Resources = ");
     for (i = 0; i < n_re ; i++)
	{ 
        printf("%d ",available[i]); 
}
printf("\n");
    while (cnt < n_p) 
    { 
        bool found = false; 
        int p;
        for (i = 0; i < n_p; i++) 
        { 
            if (end[i] == 0) 
            {
                int j; 
                for(j = 0;j< n_re; j++)
				 
                    if (needres[i][j] > work[j]) 
                        break;
                if (j == n_re) 
                { 
                    int k;
                    printf("Available resources after P%d process executed\n ",p);
                    for (k = 0 ; k < n_re ; k++) 
                    {
                        work[k] += res[i][k];
                        printf("%d ",work[k]);
                        }
					printf("\n");	 
                    S[cnt++] = i; 
                    end[i] = 1; 
                    found = true; 
                } 
            } 
        }
        if (found == false) 
        { 
            printf("System is  in Deadlock"); 
            return false;
            
        } 
    } 
    printf("System is not in Deadlock.\nSafe sequence is: ");	 
    for (i = 0; i < n_p; i++) 
    {
      printf(" %d ",S[i]); 
    }
        return true;
} 
int request(int n_p,int n_re,int needres[n_p][n_re],int maxres[n_p][n_re],int res[n_p][n_re],int available[n_re])
{
	char ch;
	int p_id;
	printf("Want to make request?[y/n]\n");
	scanf("%s",&ch);
	
	int i;
	while(ch!='n')
	{
	printf("Enter process number = ");
	scanf("%d",&p_id);
	printf("enter number of instance request for P%d",p_id);
	for(i=0;i<n_re;i++)
	{
		int r;
		scanf("%d",&r);
		res[p_id][i]=res[p_id][i]+r;
		available[i]=available[i]-r;
		needres[p_id][i]=needres[p_id][i]-r;
		
	}
	printf("you want more request = [y/n]");
	scanf("%s",&ch);
 }
	printf("process after request \n");
	display(n_p,n_re,needres,maxres,res);
    check(n_p,n_re,needres,maxres,res,available);
}
