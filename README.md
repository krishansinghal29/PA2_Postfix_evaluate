/*
// Sample code to perform I/O:

#include <iostream>

using namespace std;

int main() {
	int num;
	cin >> num;										// Reading input from STDIN
	cout << "Input number is " << num << endl;		// Writing output to STDOUT
}

// Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
*/

// Write your code here
#include <iostream>
#include <stdio.h>
using namespace std;

class stackk 
{
   public:
      int top=-1; 
      //vector<int> st;  
      int st[1000000];
      int empty(){
         if(top==-1){
             return 1;
         }
         else{
             return 0;
         }
      }
      int pop(){
          if(top==-1){
             printf("Error"); 
          }
          else{
              top=top-1;
              int out=st[top+1];
              //st.resize(top+1);
              return out;
          }
      }
      void push(int i){
          top=top+1;
          st[top]=i;
          //st.push_back(i);
          return ;
      }
};

int power(int a,int b){
    int ans=1;
    while(b!=0){
        ans=ans*a;
        b--;
    }
    return ans;
}

int precedence(char l){
    int asci=(int)(l);
    //int a=(int)('^'); int b=(int)('/');  int c=(int)('%');  int d=(int)('*');  int e=(int)('+');  int f=(int)('-');
    int ans;
    switch (asci) 
   { 
       case (int)('~'): ans=4;
               break; 
       case (int)('^'): ans=3;
               break; 
       case (int)('/'): ans=2; 
                break; 
       case (int)('%'): ans=2; 
               break; 
       case (int)('*'): ans=1;
               break; 
       case (int)('+'): ans=0; 
                break; 
       case (int)('-'): ans=0; 
               break; 
       default: ans=-1; 
               break;   
   } 
   return ans;
}
int evaluate(int a, int b, char inte){
    int asci=(int)(inte);
    //int a=(int)('^'); int b=(int)('/');  int c=(int)('%');  int d=(int)('*');  int e=(int)('+');  int f=(int)('-');
    int ans;
    switch (asci) 
   { 
       case (int)('^'): ans=power(a,b);
               break; 
       case (int)('/'): ans=a/b; 
                break; 
       case (int)('%'): ans=a%b; 
               break; 
       case (int)('*'): ans=a*b;
               break; 
       case (int)('+'): ans=a+b; 
                break; 
       case (int)('-'): ans=a-b; 
               break; 
       default: printf("Error"); 
               break;   
   } 
   return ans;
}
int main(){
    int cases;
    scanf("%d\n",&cases);
    for(int j=0;j<cases;j++){
        stackk S;
        //string input;
        char input[1000000];
        //getline(cin,input);
        scanf("%[^\n]",input);
        int lens=0;
        while(input[lens]!='\0'){
            lens++;
        }
        int indx=0;
        //printf("%s\n",input);
        while(indx<lens){
            char inpt=input[indx];
            if(precedence(inpt)==-1){
                int inte=0;
                while(((int)(input[indx]-'0'))<10&&((int)(input[indx]-'0'))>-1&&(indx<lens)){
                    inte=10*inte+(int)(input[indx]-'0');
                    indx++;
                }
                indx--;
                //printf("%d\n",inte);
                S.push(inte);
            }
            else{
                if(precedence(inpt)==4){
                    int a=-1*S.pop();
                    S.push(a);
                }
                else{
                    int a=S.pop();
                    int b=S.pop();
                    int c=evaluate(b,a,inpt);
                    //printf("%d %d\n",a,b);
                    S.push(c);
                }
            }
            indx=indx+2;
        }
        printf("%d\n",S.pop());
    }
    return 0;
}
