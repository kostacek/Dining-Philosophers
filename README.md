# Dining-Philosophers
a Graphical User Interface - showing which philosopher is eating, and which is waiting/thinking at any given time. Show the forks. Use Java programming language for this project. 
class philosopher extends Thread
{
public void run()
{
diningps.count++;
philosopher(diningps.count);
}
public void philosopher(int i)
{
take_forks(i);
System.out.println(i+"philosopher Eating");
put_forks(i);
}
public void take_forks(int i)
{
while(diningps.mutex<=0)
{
System.out.println(i+"philosopher has to be wait while other philosopher in testing");
}
diningps.state[i]="HUNGRY";
test(i);
diningps.mutex=1;
while(diningps.S[i]<=0)
{
System.out.println(i+"philosopher has to be wait while his left or right side philosopher eating.");
}
}
public void put_forks(int i)
{
while(diningps.mutex<=0)
{
System.out.println(i+"philosopher has to be wait while other philosopher in testing");
}
diningps.state[i]="THINK";
test((i+4)%5);
test((i+1)%5);
diningps.mutex=1;
}
public void test(int i)
{
if(diningps.state[i]=="HUNGRY" && diningps.state[(i+4)%5]!="EAT" && diningps.state[(i+1)%5]!="EAT")
{
diningps.state[i]="EAT";
diningps.S[i]=1;
}
}
}
class diningps
{
static int mutex=1;
static int S[]={0,0,0,0,0};
static String state[]={"THINK","THINK","THINK","THINK","THINK"};
static int count=-1;
public static void main(String ar[])
{
philosopher ob=new philosopher();
philosopher ob1=new philosopher();
philosopher ob2=new philosopher();
philosopher ob3=new philosopher();
philosopher ob4=new philosopher();
ob.start();
ob1.start();
ob2.start();
ob3.start();
ob4.start();
}
}
