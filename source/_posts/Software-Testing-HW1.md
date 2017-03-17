---
title: Software Testing HW1
date: 2017-02-27 22:55:07
tags: 软件测试作业
---
# Software Testing HW1
My blog: 	shifengmin.com
My Github: 	https://github.com/shifengmin

The error which impress me most is that when I want to scan a std::set which is similar to the following statement:
```
	for(set<int>::iterator it = myset.begin(); it!= myset.end(); it++){
		…
		if(*it==a||*it==b){
			myset.erase(balabala);	
		}
		…
	}
```
but the changes of the set is less than I hoped. It impress me a lot because I realized that I should think more about what will happen in STL. That is, I can't modify std::set while go through it because the structure will change after the modifications. I read some references of C++ language and made some inferences then I found the error.

