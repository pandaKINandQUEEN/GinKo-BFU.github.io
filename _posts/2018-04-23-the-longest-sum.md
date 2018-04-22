---
layout:     post
title:      "最长连续和"
subtitle:   ""
date:       2018-04-23
author:     "JinTao"
header-img: "img/Headers/racing.jpg"
catalog: true
tags:
- 二分
- dp
---


![img](https://m.qpic.cn/psb?/V11fBiPq0ilfbD/OCcusDkQRnqlyT2rTQiv14EstTvpYdQ2.XmJSThINgk!/b/dEIBAAAAAAAA&bo=FQdGAwAAAAADB3U!&rf=viewer_4)




### 二分
``` cpp
#include<iostream>

#include<cstring>

#include<algorithm>

using namespace std;
long long a[100005];
long long merge_max(int l,int r)
{
	if(l==r) return a[l];
	int mid=(l+r)/2;
	long long lmax=merge_max(l,mid);
	long long rmax=merge_max(mid+1,r);
	
	long long s=0;long long lef=a[mid],rig=a[mid+1];
	for(int i=mid;i>=l;i--)
	{
		s+=a[i];
		if(s>lef)
		{
			lef=s;
		}
	}
	s=0;
	for(int i=mid+1;i<=r;++i)
	{
		s+=a[i];
		if(s>rig)
		{
			rig=s;	
		}	
	}
	return max(lef+rig,max(lmax,rmax));	
} 
int main()
{
	int T;
	cin>>T;
	while(T--)
	{
		int n;cin>>n;
		for(int i=0;i<n;++i)
		{
			scanf("%lld",&a[i]);
		}
		cout<<merge_max(0,n-1)<<endl;
	}
	return 0;
}
```

### dp
```cpp
#include<iostream>
using namespace std;
long long zero=0;
int main()
{
	int T;cin>>T;
	while(T--)
	{
		long long ans;
		int n;cin>>n;
		long long last_max;
		scanf("%lld",&last_max);
		ans=last_max;
		long long t;
		for(int i=1;i<n;++i)
		{
			scanf("%lld",&t);
			last_max=max(zero,last_max)+t;
			if(last_max>ans)
				ans=last_max;
		}
		cout<<ans<<endl;
	}
	return 0;
}
```

