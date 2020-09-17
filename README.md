# largest-rectangle
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define ld long double

vector<int> rlen(vector<int> &H){

    stack<int> st;
    vector<int> length(H.size());
    st.push(0);
    for(int i=1;i<H.size();i++){
        if(H[st.top()]<=H[i]){
            st.push(i);
        }else{
            while(!st.empty() && H[i]<H[st.top()]){
                length[st.top()]=i-st.top()-1;
                st.pop();
            }
            st.push(i);
        }
    }
    while(!st.empty()){
        length[st.top()]=H.size()-st.top()-1;
        st.pop();
    }
    return length;
}
vector<int> llen(vector<int> H){

    reverse(H.begin(),H.end());
    H=rlen(H);
    reverse(H.begin(),H.end());
    return H;
}

int main(){

   int n;
   cin>>n;
   vector<int> H(n);
   for(int i=0;i<n;i++){
        cin>>H[i];
   }
   vector<int> A=rlen(H);
   vector<int> B=llen(H);
   vector<long> C(n);
   for(int i=0;i<n;i++){
        C[i]=(long)H[i]*(A[i]+B[i]+1);
   }
    cout<<*max_element(C.begin(),C.end());

}





