## 问题5：[NOIP2008 普及组] ISBN 号码

**题目描述**
每一本正式出版的图书都有一个ISBN号码与之对应，ISBN码包括99位数字、11位识别码和33位分隔符，其规定格式如x-xxx-xxxxx-x，其中符号-就是分隔符（键盘上的减号），最后一位是识别码，例如0-670-82162-4就是一个标准的ISBN码。ISBN码的首位数字表示书籍的出版语言，例如00代表英语；第一个分隔符-之后的三位数字代表出版社，例如670670代表维京出版社；第二个分隔符后的五位数字代表该书在该出版社的编号；最后一位为识别码。

识别码的计算方法如下：

首位数字乘以1加上次位数字乘以2……以此类推，用所得的结果mod11，所得的余数即为识别码，如果余数为10，则识别码为大写字母X。例如ISBN号码0-670-82162-4中的识别码4是这样得到的：对067082162这99个数字，从左至右，分别乘以1,2,...,9再求和，即0×1+6×2+……+2×9=158，然后取158mod11的结果4作为识别码。

你的任务是编写程序判断输入的ISBN号码中识别码是否正确，如果正确，则仅输出Right；如果错误，则输出你认为是正确的ISBN号码。

**输入格式**
一个字符序列，表示一本书的ISBN号码（保证输入符合ISBN号码的格式要求）。

**输出格式**
一行，假如输入的ISBN号码的识别码正确，那么输出Right，否则，按照规定的格式，输出正确的ISBN号码（包括分隔符-）。

**输入输出样例**

| 输入 #1       | 输出 #1 | 输入 #2       | 输出 #2       |
| ------------- | ------- | ------------- | ------------- |
| 0-670-82162-4 | Right   | 0-670-82162-0 | 0-670-82162-4 |

**题解**

算法二（我的版本）：

```C
#include <stdio.h>

int main() {
	char number[14];
	char letter[12] = "0123456789X";
	int i;
	int sum=0;
	int count = 1;
	scanf("%s", &number); 
	
	number[13] = '\0';
	
	for(i=0;i<11;i++) {
		if(number[i] == '-') continue;
		sum += (number[i]-48)*count;//这里的话不用加else了，因为只要上面的一旦执行就会跳过这次循环了
	    count++;
	}
	
	if(letter[sum%11]==number[12]) {
		printf("Right");
	} else {
		number[12] = letter[sum%11];
		printf("%s", number);
	}
	return 0;
}
```



算法一：

```C
//1.读入字符串
//2.自己建立一个数组用来包含0123456789X用于对照
//3.利用ASCII码的差值来计算字符数字对应的实际数字
#include <stdio.h>

int main(){
    char a[14];
    char mod[12]="0123456789X";
    gets(a);
    int i=0;
    int j=1;
    int t=0;
    for(i=0;i<12;i++){
        if(a[i]=='-' ) continue;
            t+=(a[i]-'0')*j;
            j++;
    }
    if(mod[t%11]==(a[12])){
        printf("Right");
    }else{
        a[12]=mod[t%11];
        puts(a);
    }
    return 0;
}
```



算法三

```C
#include<stdio.h>	
char num[15];
int main(){
	int i,j,flag,in;
	flag=j=0;
	for(i=0;;i++) {
		if(j==3) {
			break;
		}
        
		scanf("%c",&num[i]);
        
		if(num[i]=='-') {
			i--;
			j++;
		} else if(num[i]!='-') {
			flag=(num[i]-'0')*(i+1)+flag;
		}
	}
	
    flag=flag%11;
	scanf("%c",&num[14]);
    
	if(flag==10) {
		if(num[14]=='X') printf("Right");
		else printf("%c-%c%c%c-%c%c%c%c%c-X",num[0],num[1],num[2],num[3],num[4],num[5],num[6],num[7],num[8]);
	} else {
		if(flag==num[14]-'0') printf("Right");
		else if(flag!=10) printf("%c-%c%c%c-%c%c%c%c%c-%d",num[0],num[1],num[2],num[3],num[4],num[5],num[6],num[7],num[8],flag);
		else if(flag==10) printf("%c-%c%c%c-%c%c%c%c%c-%d",num[0],num[1],num[2],num[3],num[4],num[5],num[6],num[7],num[8],flag);
	}
	return 0;
}
```



算法四

```C
#include <stdio.h>//代码简洁明了（个人观点）
int main(void){
  char a[14], mod[12] = "0123456789X"; //先将mod11后的十一个字符存入数组
  gets(a); //输入字符串
  int i, j = 1, t = 0;
  for(i = 0; i < 12; i++) {
        if(a[i] == '-') continue; //字符串为分隔符‘-’时跳过此次循环进入下一次循环
    t += (a[i]-'0')*j++; //t储存 第j个  数字  * j 的和
  }
  if(mod[t%11] == a[12]) printf("Right");
  else {
      a[12] = mod[t%11]; //若识别码错误，则赋正确的识别码，然后输出
      puts(a);
  }
  return 0;
}
```





## 问题6：【深基3.例8】三位数排序

**题目描述**
给出三个整数a,b,c(0≤a,b,c≤100)，要求把这三位整数从小到大排序。

**输入格式**
无

**输出格式**
无

**输入输出样例**

| 输入 #1 | 输出 #1 | 输入 #2 | 输出 #2 |
| ------- | ------- | ------- | ------- |
| 1 14 5  | 1 5 14  | 2 2 2   | 2 2 2   |



题解

```C
#include<stdio.h>
int main(){
	int a[3];
	scanf("%d%d%d",&a[0],&a[1],&a[2]);
	for(int i=0;i<3;i++) {
		for(int j=i+1;j<3;j++) {
			if(a[i]>a[j]) {
				int t=a[i];
				a[i]=a[j];
				a[j]=t;
			}
		}
		printf("%d ",a[i]);
	}
	return 0;
}
```
