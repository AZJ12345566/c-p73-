# c-p73-
c语言学习记录-p74文件操作（5）
//二进制的输入（fread）与输出（fwrite）
#include<stdio.h>
struct S
{
      char name[20];
      int age;
      double score;
};

int main()
{
      struct S s=("张三“，20，55.6）；
      
      FILE* pf=fopen("test.txt","wb");//wb是为了输出数据，打开一个二进制文件
      if(pf==NULL)
      {
            return 0;
      }
      //二进制的形式写文件
      fwrite(&s,sizeof(struct S),1,pf);
      
      fclose(pf);
      pf=NULL;
      return 0;
}



struct S
{
      char name[20];
      int age;
      double score;
};

int main()
{
      struct S tmp=(0）；
      
      FILE* pf=fopen("test.txt","rb");//rb是为了输入数据，打开一个二进制文件
      if(pf==NULL)
      {
            return 0;
      }
      //二进制的形式读文件
      fread(&tmp,sizeof(struct S),1,pf);
      printf("%s %d %lf\n",tmp.name,tmp.age, tmp.score);
      fclose(pf);
      pf=NULL;
      return 0;
}


//学习C语言操作MySQI数据库
//文件的随机读写
int main()
//文件的随机读写
{
      FILE* pf=fopen("test.txt","r");
      if(pf==NULL)
      {
          return 0;
      }
      //1.定位文件指针
      //格式：int fseek(FILE *stream, long offset(偏移量），int origin（文件指针的当前位置）);
      fseek(pf,2,SEEK_CUR);//起始位置有三种：SEEK_CUR(文件当前位置)，SEEK_END(文件末尾位置)，SEEK_SET(文件的起始位置）
      //2.读取文件
      int ch=fgetc(pf);
      printf("%c\n",ch);
      fclose(pf);
      pf=NULL;
      return 0;
}


//ftell:返回文件指针相对于起始位置的偏移量
int main()
{
      FILE* pf=fopen("test.txt","r");
      if(pf==NULL)
      {
          return 0;
      }
      //1.定位文件指针
      fseek(pf,-2,SEEK_END);
      int pos=ftell(pf);
      printf("%d\n",pos);
      fclose(pf);
      pf=NULL;
      return 0;
}


//rewind:让文件的位置回到文件的起始位置
void rewind(FILE *stream);


注：在文件的读取过程中，不能用feof函数的返回值直接用来判断文件的是否结束，而是应用于当文件读取结束的时候，判断是读取文件失败结束，还是遇到文件结尾结束
1.文件读取是否结束，判断返回值是否为EOF（fgetc)，或者NULL(fgets),若返回EOF则用feof来判断
2.二进制文件读取结束判断，判断返回值是否小于实际要读的个数
如fread
int main()
{
      FILE* pf=fopen("test.txt","r");
      if(pf==NULL)
          return 0;
      int ch=fgetc(pf);
      printf("%d\n",ch);//-1
      fclose(pf);
      pf=NULL;
      return 0;
}


int main()
{
      //strerror-把错误码对应的错误信息的字符串地址返回
      printf("%s\n",strerror(errno));
      
      //perror
      FILE* pf=fopen("test2.txt","r");
      if(pf=NULL)
      {
            perror("hehe");//输出结果为hehe：No such。。。，基本可以替代strerror函数，不需要引头文件
            return 0;
      }
      //读文件
      fclose(pf);
      pf=NULL;
      return 0;
}


int main()
{
      FILE* pf=fopen("test.txt","r");
      if(pf==NULL)
      {
            perror("hehe");//输出结果为hehe：No such。。。，基本可以替代strerror函数，不需要引头文件
            return 0;
      }
      //读文件
      int ch=0;
      while((ch=fgetc(pf))!=EOF)
      {
            putchar(ch);
      }
      if(ferror(pf))
      {
            printf("error\n");
      }
      else if(feof(pf))
      {
            printf("end of file\n");
      }
      fclose(pf);
      pf=NULL;
      return 0;
}


