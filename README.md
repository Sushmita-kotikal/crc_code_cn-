#include<stdio.h>
#include<string.h>
#define n strlen(g)

char t[28],cs[28],g[]="10001000000100001";
int a,e,c;

void xor(){
    for(c=1;c<n;c++)
        cs[c]=((cs[c]==g[c]?'0':'1'));
}

void crc(){
    for(e=0;e<n;e++)
        cs[e]=t[e];
    do{
        if(cs[0]=='1')
            xor();
        for(c=0;c<n-1;c++)
            cs[c]=cs[c+1];
        cs[c]=t[e++];
    }while(e<a+n-1);
}
int main(){
    printf("enter the data:");
    scanf("%s",&t);
    printf("\n--------------------------");
    printf("\ngenerating polynomial:%s",g);
    a=strlen(t);
    for(e=a;e<a+n-1;e++)
        t[e]='0';
    printf("\n--------------------------");
    printf("\nmodified data:%s",t);
    printf("\n--------------------------");
    crc();
    printf("\nchesksum %s",cs);
    for(e=a;e<a+n-1;e++)
        t[e]=cs[e-a];
    printf("\n--------------------------");
    printf("\nfined codeword:%s",t);
    printf("\n--------------------------");
    printf("\ntest error detection 0(yes) 1(no)? : ");
    scanf("%d",&e);
    if(e==0){
        do{
            printf("enter pod where error is to be inserted:");
            scanf("%d",&e);
        }while(e==0 || e>a+n-1);
        t[e-1]=(t[e-1]=='0')?'1':'0';
        printf("\n--------------------------");
        printf("\nerronous data:%s",t);
    }
    crc();
    for(e=a;(e<n-1) && (cs[e]!='1');e++);
        if(e<n-1)
           printf("\nerror detected");
        else
           printf("\nno error");
    return 0;
}
