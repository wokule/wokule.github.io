---
layout:     post
title:      密码学笔记
subtitle:   维吉尼亚密码实现
date:       2021-01-03
author:     X2
header-img: img/post-bg.jpg
catalog: true
tags:
    - 密码学
    - 维吉尼亚密码
    
---

# 维吉尼亚密码实现
  

## Vigenère密码简介
**维吉尼亚密码**是一种是最简单的多表替换密钥，由多个凯撒替换表循环构成 。

 - **密钥**：
 ◦K＝K0 K1 … Kd-1
◦ 第i位密钥 Ki 表示采用 K=Ki 的凯撒替换表
◦ 密钥重复使用
 - **加密算法**：Ci = E(K, Pi) = (Pi + Ki mod d) mod 26
 - **解密算法**：pi = D(K, Ci) = (Ci - Ki mod d) mod 26
 - **举一个简单的栗子**：
 -密钥：***yier***
 -明文：vige nere cyph er
 -密钥：***yier  yier yier yi***
 -密文：tqkv lmvv agty cz
 
## 代码示范
注：本代码要求输入的明文、密文、密钥均为无空格的英文小写字符串。
```c
#include <stdio.h>
#include <stdlib.h>
#include <string>
int main()
{
	char mingwen[1000]="/0";
	char miwen[1000]="/0";
	char key1[100]="/0";
	int num=0,keynum=0;
	int signal = 1;
	printf("加密还是解密？加密1，解密0\n");
	scanf_s("%d", &signal);
	getchar();//吞掉前面scanf剩下的一个回车，若没有此句，下面的gets语句直接读取回车就会结束
	if (signal) {
		printf("请输入密钥：（要求小写英文字母且无空格，输入结束按回车键）\n");
		
		gets_s(key1);
		keynum = strlen(key1);//密钥长度

		printf("请输入明文：\n");
		gets_s(mingwen);
		int mingnum;
		mingnum = strlen(mingwen);//明文长度

		//加密
		int i = 0;
		for (i = 0; i < mingnum; i++)
		{
			miwen[i] = (mingwen[i] - 'a' + key1[i % keynum] - 'a') % 26 + 'a';

		}
		printf("密文是: %s \n", miwen);
	}
	else {
		printf("请输入密钥：（要求小写英文字母且无空格，输入结束按回车键）\n");

		gets_s(key1);
		keynum = strlen(key1);//密钥长度

		printf("请输入密文：\n");//agtycz
		gets_s(miwen);
		int minum;
		minum = strlen(miwen);//明文长度

		//加密
		int i = 0;
		for (i = 0; i < minum; i++)
		{
			mingwen[i] = (miwen[i] - key1[i % keynum] + 26 ) % 26 + 'a';

		}
		printf("明文是: %s \n", mingwen);
	}
	
	system("pause");	

} 
```

如果本篇博客对你有帮助，可不可以给我点个赞留个言，第一次写博客，还是希望看到的小伙伴给我点个赞的嘿嘿~
（首发自csdn）
