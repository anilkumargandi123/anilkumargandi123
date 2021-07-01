
#include<bits/stdc++.h>
using namespace std;
class Polynomial {
    
    public:
    int *a;      
    int cap;
    
    Polynomial(){
        this->a=new int[6];
        this->cap=5;
    }

    Polynomial (int cap){
        this->a=new int[cap+1];
        this->cap=cap;
    }
    
    Polynomial (Polynomial const &p){
        int *newdeg=new int[p.cap+1];
            
        for(int i=0;i<=p.cap;i++)
            newdeg[i]=p.a[i];
            
        this->a=newdeg;
        
        this->cap=p.cap;
    }
    
    void setCoefficient(int deg,int coef){
        if(deg>cap){
            int newcap=deg;
            int *newdeg=new int[newcap+1];
            
            for(int i=0;i<=cap;i++)
                newdeg[i]=a[i];
            
            this->a=newdeg;
            this->cap=newcap;
         
            a[deg]=coef;
        }
        else{
            a[deg]=coef;
        }
    }
    
    Polynomial operator+(Polynomial const &P2){
        
        int newcap=std::max(this->cap,P2.cap);
        
        Polynomial P3(newcap);
        
        for(int i=0;i<=newcap;i++){
            if(i<=cap && i<=P2.cap)
                P3.a[i]=this->a[i]+P2.a[i];
            else if(i<=cap)
                P3.a[i]=this->a[i];
            else 
                P3.a[i]=P2.a[i];
        }
        
        return P3;
    }
    
    Polynomial operator-(Polynomial const &P2){
        
        int newcap=std::max(this->cap,P2.cap);
        Polynomial P3(newcap);
        
        for(int i=0;i<=newcap;i++){
            if(i<=cap && i<=P2.cap)
                P3.a[i]=this->a[i]-P2.a[i];
            else if(i<=cap)
                P3.a[i]=this->a[i];
            else 
                P3.a[i]=-P2.a[i];
        }
        
        return P3;
    }
    
    Polynomial operator*(Polynomial const &P2){
        
        int newcap=this->cap+P2.cap;
        Polynomial P3(newcap);
        
        for(int i=0;i<=this->cap;i++){
            
            for(int j=0;j<=P2.cap;j++){
                P3.a[i+j]+=this->a[i]*P2.a[j];
            }
        }
        return P3;
    }
    
    void operator=(Polynomial const &p){
        int *newdeg=new int[p.cap+1];
        //Copy the contents
        for(int i=0;i<p.cap;i++)
            newdeg[i]=p.a[i];
            
        
        this->a=newdeg;
        
        this->cap=p.cap;
    }
    
    void print(){
        
        for(int i=0;i<=this->cap;i++){
            if(a[i]!=0)
                cout<<a[i]<<"x"<<i<<" ";
        }
        cout<<endl;
    }
           
};

int main()
{
    int c,c1,c2;
    cin >> c1;
    
    int *d1 = new int[c1];
    int *coe = new int[c1];
    
    for(int i=0;i < c1; i++) {
        cin >> d1[i];
    }
    
    for(int i=0;i < c1; i++) {
        cin >> coe[i];
    }
    
    Polynomial first;
    for(int i = 0; i < c1; i++){
        first.setCoefficient(d1[i],coe[i]);
    }
    
    cin >> c2;
    
    int *d2 = new int[c2];
    int *coe2 = new int[c2];
    
    for(int i=0;i < c2; i++) {
        cin >> d2[i];
    }
    
    for(int i=0;i < c2; i++) {
        cin >> coe2[i];
    }
    
    Polynomial second;
    for(int i = 0; i < c2; i++){
        second.setCoefficient(d2[i],coe2[i]);
    }
    
    cin >> c;
    
    switch(c){
        
        case 1:
        {
            Polynomial r1 = first + second;
            r1.print();
            break;
        }
        
        case 2 :
        {
            Polynomial r2 = first - second;
            r2.print();
            break;
        }
            
        case 3 :
        {
            Polynomial r3 = first * second;
            r3.print();
            break;
        }
        case 4 : 
        {
            Polynomial third(first);
            if(third.a == first.a) {
                cout << "false" << endl;
            }
            else {
                cout << "true" << endl;
            }
            break;
        }
            
        case 5 :
        {
            Polynomial fourth(first);
            if(fourth.a == first.a) {
                cout << "false" << endl;
            }
            else {
                cout << "true" << endl;
            }
            break;
        }
            
    }
    
    return 0;
}
