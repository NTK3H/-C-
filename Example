#include <stdio.h>
#include <stdlib.h>

typedef struct __Class_A{
	void *this;
	void (*func)();		//虚函数
	int v1;
	int v2;
	void *t;
} A;

void __Class_A_Func();

void Construct_A(int size, struct __Class_A *p)	//构造函数
{
	p->t = malloc(size);
	p->func = __Class_A_Func;
	p->v1 = 11;
	p->v2 = 12;
	p->this = p;
}

void __Class_A_Func()
{
	puts("This is class A");
}

typedef struct __Class_B{		//B继承了A
	union{
		struct __Class_A;
		int CA;
	};
	int v3;
} B;

void __Class_B_Func();

void Construct_B(int size, struct __Class_B *p, int e)	//构造函数
{
	if(e)
		Construct_A(size, (struct __Class_A*)p);	//先构造B类中的A类部分
	else
		p->CA=0;
	p->func = __Class_B_Func;
	p->v1 = 21;
	p->v2 = 22;
	p->v3 = 23;
	p->this = p;
}

void __Class_B_Func()
{
	puts("This is class B");
}

typedef struct __Class_C{
	struct __Class_A *a;
} C;

void __Class_C_Func();

void Construct_C(int size, struct __Class_C *p, int e)	//构造函数
{
	if(e)
	{
		p->a = (struct __Class_A*)malloc(sizeof(struct __Class_A));
		Construct_A(size, (struct __Class_A*)p->a);
	}
	p->a->t = malloc(size);
	p->a->func = __Class_C_Func;
	p->a->v1 = 31;
	p->a->v2 = 32;
	p->a->this = p;
}

void __Class_C_Func()
{
	puts("This is class C");
}

typedef struct __Class_D{
	struct __Class_B;
	struct __Class_C;
} D;

void __Class_D_Func();

void Construct_D(int size, struct __Class_D *p)	//构造函数
{
	p->t = malloc(size);
	p->func = __Class_D_Func;
	p->v1 = 11;
	p->v2 = 12;
}

void __Class_D_Func()
{
	puts("This is class D");
}

int main(int argc, char *argv[])
{
	A a,*a2;
	B b;
	Construct_A(sizeof(float),&a);		//泛型构造
	Construct_B(sizeof(int),&b,1);
	*(float*)a.t = 3.14;
	*(int*)b.t = 6;
	printf("a.t type = float* | value = %g\n",*(float*)a.t);
	printf("b.t type = int*   | value = %d\n",*(int*)b.t);
	a.func();
	b.func();

	a2 = (A*)&b;	//多态
	a2->func();
	printf("a2->v1 = %d\n",a2->v1);
	printf("a2->v2 = %d\n",a2->v2);
	printf("*a2->t = %d\n",*(int*)a2->t);
}
