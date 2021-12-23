# operations-on-polynomials-using-single-linkedlists

#include<stdio.h>
#include<stdlib.h>
struct polynomial
{
        int coef,expo;
        struct polynomial *next;
};
typedef struct polynomial poly;
poly* addterm(poly *first,poly *new)
{
        poly *temp,*temp1;
        if (first==NULL)
        {
                first=new;
        }
        else if (first->expo < new->expo)
        {
                new->next=first;
                first=new;
        }
        else
        {
                temp1=first;
                temp=temp1->next;
                while (temp!=NULL && temp->expo > new->expo)
                {
                        temp1=temp;
                        temp=temp->next;
                }
                if (temp==NULL)
                {
                        temp1->next=new;
                }
                else if (temp->expo ==  new->expo)
                {
                        temp->coef=temp->coef+new->coef;
                }
                else
                {
                        temp1->next=new;
                        new->next=temp;
                }
        }
        return first;
}
poly* create()
{
        poly *first=NULL;
        poly *new;
        int k;
        do
        {
        new=(poly*)malloc(sizeof(poly));
        int c,e;
        printf("enter c value:");
        scanf("%d",&c);
        printf("enter e value:");
        scanf("%d",&e);
        new->coef=c;
        new->expo=e;
        new->next=NULL;
        first=addterm(first,new);
        scanf("%d",&k);
        } while (k!=-1);
          return first;
}
poly* add(poly *p1,poly *p2)
{
        poly *p3=NULL;
        poly *new;
        while (p1!=NULL && p2!=NULL)
        {
        new=(poly*)malloc(sizeof(poly));
        if (p1->expo > p2->expo)
        {
                new->expo=p1->expo;
                new->coef=p1->coef;
                new->next=NULL;
                p3=addterm(p3,new);
                p1=p1->next;
        }
        else if (p1->expo < p2->expo)
        {
                new->expo=p2->expo;
                new->coef=p2->coef;
                new->next=NULL;
                p3=addterm(p3,new);
                p2=p2->next;
        }
        else
        {
                new->expo=p1->expo;
                new->coef=p1->coef+p2->coef;
                new->next=NULL;
                p3=addterm(p3,new);
                p1=p1->next;
                p2=p2->next;
        }
        }
        if (p1==NULL)
        {
                while (p2!=NULL)
                {
                        poly *neww;
                        neww=(poly*)malloc(sizeof(poly));
                        neww->expo=p2->expo;
                        neww->coef=p2->coef;
                        neww->next=NULL;
                        p3=addterm(p3,neww);
                        p2=p2->next;
                }
        }
        if (p2=NULL)
        {
                while (p1!=NULL)
                {
                        poly* neww;
                        neww=(poly*)malloc(sizeof(poly));
                        neww->expo=p1->expo;
                        neww->coef=p1->coef;
                        neww->next=NULL;
                        p3=addterm(p3,neww);
                        p1=p1->next;
                }
        }
        return p3;
}
poly* multiply(poly *p1,poly *p2)
{
        poly *p3=NULL,*new;
        poly *temp=p2;
        while (p1!=NULL)
        {
                p2=temp;
                while (p2!=NULL)
                {
                        new=(poly*)malloc(sizeof(poly));
                        new->coef=p1->coef*p2->coef;
                        new->expo=p1->expo+p2->expo;
                        new->next=NULL;
                        p3=addterm(p3,new);
                        p2=p2->next;
                }
                p1=p1->next;
        }
        return p3;
}
void display(poly *p3)
{

        while (p3!=NULL)
        {
                printf("%d x^%d",p3->coef,p3->expo);
                p3=p3->next;
        }
}
void main()
{
        int l;
        poly *p3,*p1,*p2;
        p1=create();
        p2=create();
        while(1)
        {
                printf("enter choice value:");
                scanf("%d",&l);
                switch(l)
                {
                        case 1:p3=add(p1,p2);
                               break;
                        case 2:p3=multiply(p1,p2);
                               break;
                        case 3:display(p3);
                               break;
                        case 4:exit(0);
                }
        }
}







