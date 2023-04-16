#include <stdio.h>
#include <math.h>

int p0 = 1.007;//单位是kp

float atmospheric()//输入气压的函数 返回的是gama
{
	float x, y, p1, p2, gama;
	printf("请输入p1~的数据和p2~的数据：");
	scanf_s("%f%f", &x, &y);
	p1 = 1.007 + (x / 2000);
	p2 = 1.007 + (y / 2000);
	gama = ((log(p1 / p0)) / (log(p1 / p2)));
	printf("%f\t", p1); printf("%f\t", p2); printf("%f\t", gama);
	return gama;
}

float Average_gama()//求出gama的平均值
{
	int i;
	float add = 0.00, average_gama;
	float gama[6];
	float* p = gama;
	for (i = 0; i < 6; i++)
	{
		*(p + i) = atmospheric();//获得每一个伽马
		add = add + *(p + i);//得到gama的总和
		printf("\n");
	}
	printf("%f", add);
	average_gama = add / 6;
	printf("伽马的平均值是：%f\n", average_gama);
	return average_gama;
}

float calculate_u()//计算u
{
	int i;
	float u, add = 0,average_gama;
	float gama[6];
	float* p = gama;
	for (i = 0; i<6; i++)
	{
		*(p + i) = atmospheric();//获得每一个伽马
		add = add + *(p + i);//得到gama的总和
		printf("\n");
	}
	average_gama = add / 6;//平均值
	for (i = 0; i < 6; i++)
	{
		add = add + (average_gama - *(p + i)) * (average_gama - *(p + i));
	}
	u = sqrt(add/5);
	return u;
}

int main()
{   
	float average_gama, i, u,u1;
	average_gama = Average_gama();//先求出gama的平均值
	//printf("伽马的平均值是：%f\n", average_gama);
	u = calculate_u();
	printf("u的值是：%f\t", u);    
	u1 = u / average_gama;
	printf("u1的值是：%f\n", u1);
	return 0;
}
