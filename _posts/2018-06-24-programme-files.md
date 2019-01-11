---
layout: article
title: C++文件操作
tags: 编程 C++
key: code1
category: 编程
date: 2018-06-24 10:00:00
modify_date: 2019-01-11 17:13:00
---

总结一下利用**C++**进行文件操作的方法，包括文件的**读**、**写**以及**遍历文件目录**。

<!--more-->

## 写文件

```c++
std::ofstream f2;
std::string dsoposefile = "./data/"+savefile_tail+"_dsopose.txt";
f2.open(dsoposefile,ios::out);
for(int i=0;i<100;++i){
    f2<<std::fixed<<std::setprecision(9)<<time_ref[i]<<" "<<i*3.3<<std::endl;//保留9位小数
}
f2.close();
```

- `ios::out`写：文件不存在，则建立新文件，文件存在则直接清空文件内容。
- `ios::out|ios::app`写追加：文件不存在，则建立新文件，文件存在则保留内容继续在末尾追加。

## 读文件

```c++
std::ifstream inf;
inf.open(timestampPath);
std::string sline;
std::getline(inf,sline);
while(std::getline(inf,sline)){
    std::istringstream ss(sline);
    double to_read;
    ss>>to_read;
}
inf.close();
```

上述代码实现读取文件的功能，`ss>>to_read`跟`cin`的效果一样。

## 遍历文件目录

需要头文件：dirent.h

```c++
inline int getdir (std::string dir, std::vector<std::string> &files)
{
    DIR *dp;
    struct dirent *dirp;
    if((dp  = opendir(dir.c_str())) == NULL)
    {
        return -1;
    }
    while ((dirp = readdir(dp)) != NULL) {
    	std::string name = std::string(dirp->d_name);

    	if(name != "." && name != "..")
    		files.push_back(name);
    }
    closedir(dp);

    std::sort(files.begin(), files.end());

    if(dir.at( dir.length() - 1 ) != '/') dir = dir+"/";
	for(unsigned int i=0;i<files.size();i++)
	{
		if(files[i].at(0) != '/')
			files[i] = dir + files[i];
	}
    return files.size();
}
```

函数调用和可得到目录`dir`下的全部文件名，保存在数组`files`中，可根据需要进行后续操作。