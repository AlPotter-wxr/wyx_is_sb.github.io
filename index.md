# wxr之家

# P2835 刻录光盘
# 本人推荐使用图论+BFS
各位神犇都是用的~~并查集~~来做的
###### ~~有意思的题目~~

##### ~~本弱鸡的第一篇题解，不喜勿喷~~

 _关于强连通块他人已经讲得很清晰了，本人不再赘述。_ 
# 思路：先用BFS遍历，得到栈序列，再清空状态数组，倒序重新遍历，输出结果
### 设置p数组表示当前状态，G数组（二维）存储图的信息，f为栈。



------------
核心bfs：
```cpp
void bfs(int x){
    p[x]=true;//访问过了，标记
    for(int i=1;i<=n;i++)//以这个点为访问中介看其他点
        if(p[i]==0&&G[x][i]!=0)//判断
            bfs(i);
    t++;//设置t变量，用来标记栈
    f[t]=x;//入栈
}
```
```cpp
void bfs2(int x){//重新遍历
    p[x]=true;
    for(int i=1;i<=n;i++)
        if(p[i]==0&&G[x][i]!=0)
            bfs2(i);
}
```


------------
核心判断：
```cpp
for(int i=t;i>0;i--)
        if(p[f[i]]==0){//是强连通块
            ans++;
            bfs2(f[i]);//再遍历
        }
```


------------
### 不多bb，直接上代码
# Code
```cpp
#include <bits/stdc++.h>
using namespace std;
int n,x,t=0,ans=0,f[250];
bool p[250],G[250][250];
void bfs(int x){
    p[x]=true;
    for(int i=1;i<=n;i++)
        if(p[i]==0&&G[x][i]!=0)
            bfs(i);
    t++;
    f[t]=x;
}
void bfs2(int x){
    p[x]=true;
    for(int i=1;i<=n;i++)
        if(p[i]==0&&G[x][i]!=0)
            bfs2(i);
}
int main(){
    scanf("%d",&n);
    for(int i=1;i<=n;i++){//细节！叩细节！
        scanf("%d",&x);
        while(x!=0){
            G[i][x]=true;
            scanf("%d",&x);
        }
    }
    for(int i=1;i<=n;i++)//第一次遍历
        if(p[i]==0)
            bfs(i);
    fill(p,p+205,0);//数组清空~~   慎用memset 
    for(int i=t;i>0;i--)//倒序遍历，注意是>0，这玩意差点坑掉一次AC
        if(p[f[i]]==0){
            ans++;
            bfs2(f[i]);//二次遍历
        }
    printf("%d\n",ans);

    return 0;
}
```
##### AC代码，可食~~五~~毒
#### 你能看到这里，真的感谢！
