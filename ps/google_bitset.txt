#include<bits/stdc++.h>
using namespace std;
 
int n;
vector<long> a;
long long dp[20][1<<20];
 
long long mi(int i, bitset<20>b)
{
    if(i==n)return 0;
    long long &ret = dp[i][b.to_ulong()];
    if(ret!=-1)return ret;
    if(b[i])ret = mi(i+1,b);
    else{
        b[i]=1;
        ret = LONG_LONG_MAX;
        for(int j=0;j<n;j++)
        {
            if(i==j||b[j])continue;
            b[j]=1;
            ret = min(ret,mi(i+1,b)+(a[i]^a[j]));
            b[j]=0;
        }
    }
    return ret;
}
 
long long mx(int i, bitset<20>b)
{
    if(i==n)return 0;
    long long &ret = dp[i][b.to_ulong()];
    if(ret!=-1)return ret;
    if(b[i])ret = mx(i+1,b);
    else{
        b[i]=1;
        ret = -LONG_LONG_MAX;
        for(int j=0;j<n;j++)
        {
            if(i==j||b[j])continue;
            b[j]=1;
            ret = max(ret,mx(i+1,b)+(a[i]^a[j]));
            b[j]=0;
        }
    }
    return ret;
}
 
vector<long long> Min_and_Max (int m,vector<long> A) {
      
   vector<long long> r;
   n = m;
   a = A;
    bitset<20>b;
     memset(dp, -1,  sizeof(dp));
  
      r.push_back(mi(0,b));
     memset(dp, -1,  sizeof(dp));
      r.push_back(mx(0,b));
 
   
   
   return r;
  
}
 
int main() {
 
    ios::sync_with_stdio(0);
    cin.tie(0);
    int n;
    cin >> n;
    vector<long> Arr;
    long A;
    for(int i_Arr=0; i_Arr<n; i_Arr++)
    {
        cin>>A;
        Arr.push_back(A);
    }
 
    vector<long long> out_;
    out_ = Min_and_Max(n,Arr);
    cout << out_[0];
    for(int i_out_=1; i_out_<out_.size(); i_out_++)
    {
        cout << " " << out_[i_out_];
    }
    return 0;
}
