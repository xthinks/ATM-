# ATM-
一．课题内容和要求：
1．内容：ATM模拟程序
2．要求：
（1）登录：当输入的卡号和密码（初始密码为123456）后，与文本文件中已存放的卡号、密码匹配，若正确，登录自动提款机。
（2）自动提款机取款：每次取款金额为100的倍数，总额不超过5000元，支取金额不允许透支。
（3）自动提款机存款：不能出现负存款。
（4）修改密码：新密码长度不小于6位，不允许出现6位完全相同的情况，只有旧密码正确，新密码符合要求，且两次输入相同的情况下才可以成功修改密码。
（5）查询余额：初始余额为10000元。
（6）退出：退出时，需要将对帐户修改的数据存入文本文件中
3．实现语言：C++ 


二．需求分析：
本程序含有atm、users、main三个模块以及atm头文件。在atm头文件中定义两个类，在其余三个模块中分别实现两个类的变量定义和函数实现以及主函数。

三．概要设计：
本程序使用面向对象的方法，共定义两个类：Users类和ATM类，两者为友元类。Users类中定义名为bc的引用型变量。流程图见下：
 
类中的成员变量和成员函数见下：
public:
	friend class ATM;//将ATM类设置为Users类的友元类
	Users(char Name[],char Num[],int Money,char Password[]);
protected:
	char* getname();//取得银行卡姓名
	char* getnum();//取得银行卡号
	char* getpasswd();//取得银行卡密码
	int getmoney();//取得银行卡余额
	void setpasswd(char pwd[]);//设置银行卡密码
	void setmoney1(int m);
	void setmoney2(int m);//更新银行卡金额
private:
	char passwd[8];//存储用户密码
	char name[20];//存储用户姓名
	char num[20];//存储银行卡号
	int money;//存储银行卡金额
ATM类的成员变量及成员函数见下：
public:
		ATM(Users& bc):UsersAtATM(bc)//bc是Users类的引用型变量，
	{
		//因为ATM类中有Users类的私有数据成员，所以必须调用Users类的构造函数初始化变量bc
		totalmoney = 10000;
		oncemoney = 5000;
		leftmoney = 10000;
	}
	void welcome();//登陆界面
	bool checkpasswd(char n[],char pwd[]);//核对所输卡号，密码是否正确
	void changepasswd();//修改密码
	void fetchmoney();//取款
	void Insetmoney();//存款
	void information();//显示插入ATM机中的银行卡信息
	void exitATM();//退出系统
	void functionshow();//功能界面
	void lock();//锁卡，退出系统
	void Clear();//清屏
    private:
	int times;//记录密码次数
	int totalmoney;//记录本ATM机存款总额
	int leftmoney;//记录取款机剩余金额
	int oncemoney;//记录取款单笔最高金额
	Users& UsersAtATM;//插入ATM机的银行卡信息

