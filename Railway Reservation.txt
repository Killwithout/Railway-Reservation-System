#include<fstream.h>
#include<time.h>
#include<conio.h>
#include<stdlib.h>
#include<stdio.h>
#include<string.h>
#include<iomanip.h>
#include<ctype.h>
void loading();
void loading()     //Function for loading
 {
 long int i;
 int h=1;
 cout<<"\n  Loading";
 do
 {
 for(i=0;i<60000000;i++);cout<<'.';
 for(i=0;i<60000000;i++);cout<<'.';
 for(i=0;i<60000000;i++);cout<<'.';
 for(i=0;i<60000000;i++);cout<<'.';
 cout<<"\b\b\b\b";
 h++ ;
 }
 while(h<3);
 cout<<"\b\b\b\b\b\b\b";
}

void timedelay(long int a);  //Time delay module.
void timedelay(long int a)
{
 long int i;
 for(i=0;i<a;i++);
}

char* validstrinput();  //Validation for string inputs.
char* validstrinput()
 {
  int flag;
  int i,len;
  while(1)
	{
	flag=1;
	char str[50];
	gets(str);
	len = strlen(str);
	for(i=0;i<len;i++)
	 {
	  if((isalpha(str[i])==0)&&(str[i]!=' '))
		flag=0;
	  }
	 if (flag==1)
	  {
	  return str;
		}
	 else
	  cout<<"\n Invalid input, Please Re-Enter : ";
	 }
  }

int validintinput();  //Validation function for integer inputs.
int validintinput()
 {
  int flag;
  int temp,i,len;
  while(1)
	{
	flag=1;
	char str[25]="";
	gets(str);
	len = strlen(str);
	for(i=0;i<len;i++)
	 {
	  if(isdigit(str[i])==0)
		flag=0;
	  }
	 if (flag==1)
	  {
	  temp=atoi(str);
	  return temp;
	  }
	 else
	  cout<<"\nInvalid input, Please Re-Enter : ";
	 }
 }

//Cancellation class :-

class canc
{
  public:
  int pnr;                 		// passenger no.
  int trainno;                 	// train no.
  char trainname[30];          	// train name
  char bp[30];             		// boarding point
  char destination[30];          // destination
  char pname[10][100];     		// passenger name
  int age[10];             		//age of passenger
  char clas[10];         		  	// type of class
  int nosc;                		// no. of seats cancelled
  int d,m,y;               		// date,month, year
  float amtr;              		// amount returned

 void getcancdet()             //cancellation inputs:-
  {
	 cout<<"\n Enter the details of the ticket(s) to be cancelled :";
	 cout<<"\n Enter the passenger number"<<"\n";
	 pnr=validintinput();
	 cout<<"\n Enter the train number"<<"\n";
	 trainno=validintinput();
	 cout<<"\n \t Enter date of cancellation"; // Entering date.
	 cout<<"  : ";
	 l7:
	 cout<<"\n\n \t Enter Date of the month - ";
	 d=validintinput();
	 if(d>31||d<1)
	  {
	  cout<<"\n\n\t Invalid Date, Please Re-Enter\n";
	  goto l7;
	  }
	 cout<<"\t\t\t\t";
	 cout<<"\n \t Enter Month - ";
	 m=validintinput();
	 if(m>12||m<1)
	{
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l7;
	}
  else if((m==2)||(m==4)||(m==6)||(m==9)||(m==11))
	{
		if(m==2)
		 {
			if(d>28||m<1)
			 {
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l7;
			 }
		 }

	 else
	  if(d>30||m<1)
		  {
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l7;
		  }
	}
  else
	{
	  if(d>31||m<1)
		{
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l7;
		}
	}
	l8:
	 cout<<"\t\t\t\t";
	 cout<<"\n \t Enter Year - ";
	 y=validintinput();
	if(y<1995||y>2020)
		{
		cout<<"\n\n \t  Invalid Year , Please Re-enter\n ";
		goto l8;
		}
  }
 void displaycancdet()        //cancellation output:-
  {
	 cout<<"\n Passenger names:";
		 for(int i=0;i<nosc;i++)
			 {
				cout<<pname[i]<<" ";
			 }
	 cout<<"\n Passenger number : "<<pnr;
	 cout<<"\n Train name : "<<trainname;
	 cout<<"\n Train number : "<<trainno;
	 cout<<"\n Type of the class of the ticket : "<<clas;
	 cout<<"\n Number of tickets cancelled : "<<nosc;
	 cout<<"\n Date : "<<d<<"/"<<m<<"/"<<y;
	 cout<<"\n Total amount returned : "<<amtr;
  }
};

//User class:-
class user
{ public :
  char uid[100];
  char pass[100];
  void getid()
  {
	 user s;
	 clrscr();
			cout<<"\n\t\tREGISTER PAGE :-";
					char newid[100];
					l1:
					int flag=0;
					cout<<"\n\t\t Enter your new username"<<endl;
					cout<<"\t\t";
					gets(newid);
					fstream f;
					f.open("id.dat",ios::in|ios::binary);
					while(f.read((char*)&s,sizeof(s)))
						{
							if(strcmp(newid,s.uid)==0)
								{
									flag++;
									break;
								}
						}
						f.close();

					if(flag!=0)
						{
							cout<<"\n User ID already exists.Please enter a new ID";
							goto l1;
						}
					else if(flag==0)
						{
							cout<<"\n\t\tUsername Available .";
							strcpy(uid,newid);
							cout<<"\n\t\t Enter your new password"<<endl;
							cout<<"\t\t";

							char z;
							for(int i=0;;i++)
							  {

								 pass[i]=getch();
								 z=pass[i];
								if(z==13)
							  {
								pass[i]='\0';
								break;
								}
							else if(z==8)
								{
								if(i>0)
								{
								cout<<"\b"<<" "<<"\b";
								i=i-2;
								}

								}
								else putch('*');
										 }
							}
						}
  void displayid()           //display function
  { cout<<"\n \t User id "<<" - "<<uid;
	 cout<<"\n \tPassword "<<" - "<<pass;
  }
};

//Train Class :-

class train
{ private :                 //Members
  int trainno;
  char trainname[100];
  char bp[100];
  char destination[100];
  char mode[10];
  int c1fare;
  int c2fare;
  int date,month,year;

  public :
 int c1,c2;



  // All the accessor functions :-

  int gettrainno()
	{
	 return trainno;
	 }

  char* gettrainname()
	{
	return trainname;
	}

	char* getbp()
	{
	return bp;
	}

	char* getdestination()
	{
	return destination;
	}

	char* getmode()
	{
	return mode;
	}

	int getc1fare()
	{
	return c1fare;
	}

	int getc2fare()
	{
	return c2fare;
	}

	int getdate()
	{
	return date;
	}

	int getmonth()
	{
	return month;
	}

	int getyear()
	{
	return year;
	}

  void getdetails() //To Enter trains' details (only admin)

  {
	 cout<<"\n \t Enter details \n";
	 cout<<"\n \t Enter train number "; //Entering the train number.
	 cout<<"   -   ";
	 trainno=validintinput();
	 cout<<"\n \t Enter train name ";  // Entering the train name.
	 cout<<"   -   ";
	 gets(trainname);
	 cout<<"\n \t Enter the boarding point "; // Entering the boarding point.
	 cout<<"   -   ";
	 strcpy((bp),(validstrinput()));
	 cout<<"\n \t Enter destination "; // Entering destination.
	 cout<<"   -   ";
	 strcpy((destination),(validstrinput()));
	 cout<<"\n \t Enter the number of c1 seats "; //Entering the number of c1 seats.
	 cout<<"   -   ";
	 c1=validintinput();
	 cout<<"\n \t Enter the price of each c1 seat "; // Entering the price of the c1 seats.
	 cout<<"   -   ";
	 c1fare=validintinput();
	 cout<<"\n \t Enter the number of c2 seats "; // Entering the number of c2 seats.
	 cout<<"   -   ";
	 c2=validintinput();
	 cout<<"\n \t Enter the price of each c2 seat "; // Entering the price of the c2 seats.
	 cout<<"   -   ";
	 c2fare=validintinput();
	 cout<<"\n \t Enter date of the next departure"; // Entering date.
	 cout<<"  : ";
	 l5:
	 cout<<"\n\n \t Enter Date of the month - ";
	 date=validintinput();
	 if(date>31||date<1)                                       //Date Validation
	  {
	  cout<<"\n\n\t Invalid Date, Please Re-Enter\n";
	  goto l5;
	  }
	 cout<<"\t\t\t\t";
	 cout<<"\n \t Enter Month - ";
	 month=validintinput();
	 if(month>12||month<1)
	{
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l5;
	}
  else if((month==2)||(month==4)||(month==6)||(month==9)||(month==11))
	{
		if(month==2)
		 {
			if(date>28||month<1)
			 {
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l5;
			 }
		 }

	 else
	  if(date>30||month<1)
		  {
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l5;
		  }
	}
  else
	{
	  if(date>31||month<1)
		{
	  cout<<"\n\n \t Invalid Date , Please Re-enter\n";
	  goto l5;
		}
	}
	l6:
	 cout<<"\t\t\t\t";
	 cout<<"\n \t Enter Year - ";
	 year=validintinput();
	if(year<1995||year>2020)
		{
		cout<<"\n\n \t  Invalid Year , Please Re-enter\n ";
		goto l6;
		}
  }
  void displaydetails()                         // Displaying all the details.
  { cout<<"\n \t Train number   -   "<<setw(10);
	 cout<<"\t"<<trainno;
	 cout<<"\n \t Train name   -    "<<setw(10);
	 cout<<"\t"<<trainname;
	 cout<<"\n \t Boarding point   -   "<<setw(10);
	 cout<<"\t"<<bp<<setw(10);
	 cout<<"\n \t Destination   -    "<<setw(10);
	 cout<<"\t"<<destination<<setw(10);
	 cout<<"\n \t Number of c1 seats   -   "<<setw(5);
	 cout<<"\t"<<c1<<setw(5);
	 cout<<"\n \t Price of each c1 seat   -"<<setw(5);
	 cout<<"\t"<<c1fare<<setw(1);
	 cout<<"\n \t Number of c2 seats   -"<<setw(5);
	 cout<<"\t"<<c2<<setw(5);
	 cout<<"\n \t Price of each c2 seat   -"<<setw(5);
	 cout<<"\t"<<c2fare<<setw(1);
	 cout<<"\n \t Date of the next departure  -  ";
	 cout<<date<<"/"<<month<<"/"<<year<<"\n";
  }
  };

class reser
{
public:
int pnr;                              //passenger no
int trainno;
char bp[10] ;                           //Boarding point
char  trainname[100];
char destination[100];
char pname[10][100];                  //passengers' name
int age[10];                          //passengers' age
char clas[10];                        //sleeper or seater class
int nosr;                             //no of seats reserved
int d,m,y;
float amc;                         //cost
void getresdet()
{

int temp,temp1,temp2;
fstream f1;
train a1;
int flag;
//input reservation details from the user
cout<<"\n Enter the Train Number for your desired Boarding and Destination point :\n" ;
trainno=validintinput();
cout<<"\n For sleeper class,enter code C1  :\n";
cout<<"\n For seater class,enter code C2   :\n";
cout<<"\n Enter your class of choice :   ";
gets(clas);
l3:
cout<<"\n Enter total number of passengers  :\n"<<endl;
temp=validintinput();
f1.open("t.dat",ios::in|ios::binary);
while(f1.read((char*)&a1,sizeof(a1)))
 {
  if(trainno==a1.gettrainno())
	{
	 temp1=a1.c1;
	 temp2=a1.c2;
	}
 }
  flag=1;
  if((strcmp(clas,"C1")==0)||(strcmp(clas,"c1")==0))
	 {
		  if(temp>temp1)
		  {
			  flag=0;
			  cout<<"Not enough seats available.";
			  cout<<"\n Please Re-enter ..\n\n";
		  }
		  else
			 nosr=temp;
	  }
 else if ((strcmp(clas,"C2")==0)||(strcmp(clas,"c2")==0))
	 {
		  if(temp>temp2)
		  {
			  flag=0;
			  cout<<"Not enough seats available.";
			  cout<<"\n Please Re-enter ..\n\n";
		  }
		  else
			 nosr=temp;
	  }
		  f1.close();
if(flag==0)
 goto l3;

for(int i=0;i<nosr;i++)
{
cout<<"\n Enter the name of passenger ";
cout<<(i+1)<<" : ";
cout<<" \n ";
strcpy((pname[i]),validstrinput()) ;
cout<<"\n Enter the age of passenger "<<(i+1)<<" :\n ";
age[i]=validintinput();
}
}
void displayresdet()        //to display reservation details
{
cout<<"\n Train number 	     : "<<trainno;
cout<<"\n Train name          : "<<trainname;
cout<<"\n Boarding            : "<<bp;
cout<<"\n Destination         : "<<destination;
if((strcmp(clas,"C1")==0)||(strcmp(clas,"c1")==0))
cout<<"\n Class               : SLEEPER";
else if((strcmp(clas,"C2")==0)||(strcmp(clas,"c2")==0))
cout<<"\n Class               : SEATER";
cout<<"\n Date of departure   : "<<d<<"/"<<m<<"/"<<y;
cout<<"\n Passenger no.       : "<<pnr;
cout<<"\n Amount              : "<<amc;
cout<<"\n Passengers :-";
for(int i=0;i<nosr;i++)
cout<<"\n\n"<<(i+1)<<')'<<"NAME : "<<(pname[i])<<"\t"<<"AGE   :"<<(age[i]);
cout<<"\n____________________________________________________________________\n";
}
};
void reserve();
void res();
void reserve()   //Navigation to reservation function
{
char ch;
do
{
cout<<"\n 1.Reserve";
cout<<"\n 2.Return to User menu";
cout<<"\n Enter your choice";
cin>>ch;
cout<<endl;
switch(ch)
{
case '1':
res();
break;

case '2':
 clrscr();
 return;

default :
 cout<<"\n\t\tInvalid Choice.";
 cout<<"\n\n Press any key to continue...";
 getche();
 clrscr();
}
}
while(1);
getch();
}
void res()      //function to  calculate cost and modify the number of seats
{
int amt;
int addr;
int ad;
int flag;
train a;
reser b;
fstream f1,f2;
time_t t;
f1.open("t.dat",ios::in|ios::out|ios::binary);
f2.open("p.dat",ios::in|ios::out|ios::binary|ios::app);
int ch;
b.getresdet();
while(f1.read((char*)&a,sizeof(a)))
{
if(a.gettrainno()==b.trainno)
{
if((strcmp(b.clas,"C1")==0)||(strcmp(b.clas,"c1")==0))
{
if(a.c1>=b.nosr)                      //deduction of seats from train database
{                                     //based on user's booking information
 amt=a.getc1fare();                   //for class C1
 addr=f1.tellg();
 ad=sizeof(a.c1);
 a.c1=a.c1-b.nosr;
 f1.seekp(addr-sizeof(a));
 f1.write((char*)&a,sizeof(a));
 srand((unsigned)time(&t));
 b.pnr=rand();
 b.amc=b.nosr*a.getc1fare();
 strcpy(b.trainname,a.gettrainname());
 strcpy(b.bp,a.getbp());
 strcpy(b.destination,a.getdestination());
 b.d=a.getdate();
 b.m=a.getmonth();
 b.y=a.getyear();
 f2.write((char*)&b,sizeof(b));
 b.displayresdet();
	cout<<"\n--------------------------------------------------------------------------------";
	cout<<"\n----------------------------The ticket is reserved------------------------------";
	cout<<"\n----------------------------End of reservation menu-----------------------------";
	cout<<"\nPress Enter to continue....";
}
else
{
cout<<"\n***********************SORRY,REQUIRED SEATS NOT AVAILABLE***********************";
}
}
else if((strcmp(b.clas,"C2")==0)||(strcmp(b.clas,"c2")==0))
{
if(a.c2>=b.nosr)
{
amt=a.getc2fare();                    //deduction of seats from train database
addr=f1.tellg();                      //based on user's booking information
ad=sizeof(a.c2);                      //in class C2
f1.seekp(addr-sizeof(a));
a.c2=a.c2-b.nosr;
f1.write((char*)&a,sizeof(a));
b.amc=b.nosr*a.getc2fare();
srand((unsigned)time(&t));
b.pnr=rand();
strcpy(b.trainname,a.gettrainname());
strcpy(b.bp,a.getbp());
strcpy(b.destination,a.getdestination());
b.d=a.getdate();
b.m=a.getmonth();
b.y=a.getyear();
f2.write((char*)&b,sizeof(b));
b.displayresdet();
cout<<"\n--------------------------------------------------------------------------------";
cout<<"\n----------------------------The ticket is reserved------------------------------";
cout<<"\n----------------------------End of reservation menu-----------------------------";
}
else
{
cout<<"\n***********************SORRY,REQUIRED SEATS NOT AVAILABLE***********************";
}
}
getch();
goto h;
}
else
{
flag=0;
}
}
if(flag==0)
{
cout<<"\n---------------------------WRONG TRAIN NUMBER---------------------------------";
cout<<"\n--------------------ENTER TRAIN NUMBER FROM DATABASE--------------------------";
}
f1.close();
f2.close();
getch();
h:
}
  void enquiry();
  void database();
  void manage();
  void displaypassdetails();
  void cancell();
  void userm();
  void can();
 void manage() //to display user login details,to enable admin to create new users
{
char ch;
fstream f;
char c;
user a;
cout<<"~*~*~*~*~*~*~*~*~*~* Welcome to the User Managment Menu *~*~*~*~*~*`*~*~*~*~ \n";
do
{
 cout<<" 1. Create ID database \n";
 cout<<" 2. Add details\n";
 cout<<" 3. Display Details \n";
 cout<<" 4. Return to the Admin menu \n";
 cout<<" \n Please enter your choice";
 cin>>ch;
 switch(ch)
 {
  case '1':
	f.open("id.dat",ios::out|ios::binary);
	do{
		 a.getid();
		 f.write((char*)&a,sizeof(a));
		 cout<<"\n Do you want to add one more record ?\n";
		 cout<<" Y - for yes \n";
		 cout<<" N - for no\n";
		 cin>>c;
	}
	while(c=='y' || c=='Y');
	f.close();
	break;

	case '2':
	f.open("id.dat",ios::binary|ios::app);
	a.getid();
	f.write((char*)&a,sizeof(a));
	f.close();
	break;

	case '3':
	f.open("id.dat",ios::in|ios::binary);
	f.seekg(0);
	while(f.read((char*)&a,sizeof(a)))
	{
	 a.displayid();
	 cout<<endl<<endl;
	 cout<<"______________________________________________________________________";
	 cout<<endl<<endl;
	}
	f.close();
	break;

	case '4' :
	 clrscr();
	 return;

	default :
	 cout<<"\n\n\t Invalid Choice";
	 cout<<"\n\n\t Press any key to continue..";
	 getche();
	 clrscr();
	}
  }while(1);
  getch();
 }
void database()     //to create train database ,to display the database
{
loading();
clrscr();
 char password[20];
 char pass[]="admin";
 cout<<"\n \t\t *^*^*^*^*^* ADMIN MODE *^*^*^*^*^* ";
 cout<<"\n\n \t\t Enter the admin exclusive password \n";
 cout<<endl<<endl;
 cout<<"    \t\t\t   ";

 char b;
 for(int i=0;;i++)
  {

		 password[i]=getch();
		 b=password[i];
		 if(b==13)
		 {
				password[i]='\0';
				break;
		 }
		 else if(b==8)
		 {
				if(i>0)
				{
						cout<<"\b"<<" "<<"\b";
						i=i-2;
				}

		 }
		 else putch('*');
		 }
 clrscr();
 train a;
 fstream f;
 char ch;
 char c;
 if(strcmp(password,pass)==0)       //admin menu
 {
  do
  {

	cout<<"\n\n \t    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~";
	cout<<"\n \t    .................... ADMIN MENU .....................\n";
	cout<<"\n \t    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~";
	cout<<"\n\n\n \t 1. Create train detail database \n";
	cout<<"\n \t 2. Add train details \n";
	cout<<"\n \t 3. Display train details \n";
	cout<<"\n \t 4. User managment \n";
	cout<<"\n \t 5. Display passenger details \n";
	cout<<"\n \t 6. Return to main menu \n";
	cout<<"\n\n \t    Enter your choice \n";
	cout<<"  \t   ";
	cin>>ch;
	clrscr();
	cout<<endl;
	switch(ch)
	{ case '1' :
	  f.open("t.dat",ios::out|ios::binary);
	  do
		{
		 a.getdetails();
		 f.write((char*)&a,sizeof(a));
		 cout<<"\n \t Do you want to add one more record ?? \n";
		 cout<<"\n \t y - for yes \n";
		 cout<<"\n \t n - for no";
		 cout<<" \t";
		 cin>>c;
		 }
		 while(c=='y'||c=='Y');
		 f.close();
		 break;

		case '2' :
		f.open("t.dat",ios::in|ios::app|ios::binary);
		do
		{
		a.getdetails();
		f.write((char*)&a,sizeof(a));
		cout<<"\n \t Do you want to add one more train?? \n";
		cout<<"\n \t y - for yes \n";
		cout<<"\n \t n - for no \n";
		cout<<"\t";
		cin>>c;
		}
		while(c=='y'||c=='Y');
		f.close();
		break;

	  case '3' :
	  f.open("t.dat",ios::in|ios::binary);
	  f.seekg(0);
	  while(f.read((char*)&a,sizeof(a)))
	  { a.displaydetails();
	  cout<<"\n~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~\n";
	  }
	  f.close();
	  cout<<"\n\n Enter any key to proceed..";
	  getche();
	  clrscr();
	  break;

	  case '4' :
	  manage();
	  break;

	  case '5' :
	  displaypassdetails();
	  break;

	  case '6' :
		 return;

	  default :
		 cout<<"\nInvalid Choice";
		 cout<<"\n Please enter any key to proceed..";
		 getche();
		 clrscr();
	  }
	}
	while(1);
	f.close();
	}
else if(strcmp(pass,password)!=0)
 {
 cout<<"\n \t Enter the correct password!!! \n";
 cout<<"\n \t You are not permitted to login in this mode!!! \n";
 goto h;
 }
	h :
	;
  }
void main()
	 {
		long int i;
		 cout<<"\n\n\n";
		 cout<<"*******************************************************************************\n";
		 cout<<setw(22)<<"W";
		 timedelay(8999999);
			 cout<<'E';
				 timedelay(8999999);
				cout<<'L';
					timedelay(8999999);
					cout<<'C';
						 timedelay(8999999);
						cout<<'O';
							 timedelay(8999999);
							cout<<'M';
								 timedelay(8999999);
								cout<<'E';
									 timedelay(8999999);
									cout<<' ';
									  timedelay(8999999);
									  cout<<'T';
										 timedelay(8999999);
										 cout<<'O';
											timedelay(8999999);
											cout<<' ';
											  timedelay(899999);
											  cout<<'T';
												 timedelay(8999999);
												 cout<<'H';
													timedelay(8999999);
													cout<<'E';
													 timedelay(8999999);
													  cout<<' ';
														timedelay(8999999);
														 cout<<'E';
															timedelay(8999999);
															cout<<'L';
															 timedelay(8999999);
															 cout<<'I';
																timedelay(8999999);
																cout<<'T';
																	timedelay(8999999);
																	cout<<'E';


																		 timedelay(8999999);
																		 cout<<' ';
																			timedelay(8999999);
																			cout<<'T';
																			  timedelay(8999999);
																			  cout<<'R';
																				 timedelay(8999999);
																				 cout<<'A';
																					timedelay(8999999);
																					cout<<'I';
																					  timedelay(8999999);
																					  cout<<'N';
																						 timedelay(8999999);
																						 cout<<' ';
																							timedelay(8999999);
																							cout<<'T';
																							  timedelay(8999999);
																							  cout<<'R';
																								 timedelay(8999999);
																								 cout<<'A';
																									timedelay(8999999);
																									cout<<'V';
																									  timedelay(8999999);
																									  cout<<'E';
																										 timedelay(8999999);
																										 cout<<'L';
																											timedelay(8999999);
																											cout<<'S';
																											  timedelay(8999999);
																											  cout<<"!\n\n\n";
				cout<<"\n \t\t           A PROJECT BY: \n";
				cout<<"\n \t\t       Eshwar, Akshaya, Reshmi and Abishek\n";

				cout<<"\n*******************************************************************************\n";
			  cout<<"\n \n \n Please press \'Enter\' to proceed..\n";
		getche();
		loading();
		clrscr();

		char ch;
		 //main menu
		 cout<<"\n\n  \t*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*";
		 cout<<"\n  \t*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*";
		 cout<<"\n  \t*                                                           *";
		 cout<<"\n  \t*           WELCOME TO RAILWAY RESERVATION SYSTEM           *";
		 cout<<"\n  \t*                                                           *";
		 cout<<"\n  \t*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*";
		 cout<<"\n  \t*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*";

		 do
	 {
		 cout<<"\n\n\n                     *~*~*~*~*~*~MAIN MENU~*~*~*~*~*~*";
		 cout<<"\n\n\n  1. Admin mode";
		 cout<<"\n  2. User mode";
		 cout<<"\n  3. Exit \n";
		 cout<<"\n \n \t \t Please enter your choice : ";
	 cin>>ch;
	 cout<<endl;
 switch(ch)
	{
	  case '1':
		database();
		 break;
	  case '2':
		userm();
		 break;
	  case '3':
		 clrscr();
		 cout<<"\n\n\n\n\n\n";

		 cout<<"<*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*>\n";
		 cout<<"\n******************************************************************************\n";
		 cout<<"______________________THANK YOU FOR USING ELITE TRAIN TRAVELS_________________\n";
		 cout<<"\n******************************************************************************\n";
		 cout<<"\n<*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*><*>";

		 exit(0);
	  default:
		 cout<<"\n Invalid Choice \n";
		 cout<<"\n Press any key to proceed";
		 getche();
		 clrscr();
		}
	}
 while(1);
	  getche();
	  clrscr();
	}
	void userm()   //function for user menu
	 {
	 loading();
	 int x=0;
	 int d;
	 user a;
	 char ch;
	 clrscr();
	 cout<<"\n       *~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*";
	 cout<<"\n       *  *~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*  *";
	 cout<<"\n       *  *                                                           *  *";
	 cout<<"\n       *  *           WELCOME TO RAILWAY RESERVATION SYSTEM           *  *";
	 cout<<"\n       *  *                                                           *  *";
	 cout<<"\n       *  *~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*  *";
	 cout<<"\n       *~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*~*";
	 fstream f1;
	 l4:

	 d=0;
	 cout<<"\n\t\t If you are a new user,to register,press 1.";
	 cout<<"\n\t\t If you are a registered user,to login,press 2.";
	 cout<<"\n\t\t";
	 char cho;
	 cin>>cho;
	 clrscr();
	 if(cho=='1')
		{
		clrscr();
		cout<<"\n\t\tREGISTER PAGE :-";
		f1.open("id.dat",ios::in|ios::binary|ios::out|ios::app);
					char newid[100];                                     //creating a new id
					u:
					int flag=0;
					cout<<"\n\t\t Enter your new username"<<endl;
					cout<<"\t\t";
					gets(newid);
					fstream f;
					f.open("id.dat",ios::in|ios::binary);
					while(f.read((char*)&a,sizeof(a)))          ///verifying if id already exists
						{
							if(strcmp(newid,a.uid)==0)
								{
									flag++;
									break;
								}
						}
						f.close();

					if(flag!=0)
						{
							cout<<"\n User ID already exists.Please enter a new ID";
							goto u;
						}
					else if(flag==0)
						{
							cout<<"\n\t\tUsername Available .";
							strcpy(a.uid,newid);
							cout<<"\n\t\t Enter your new password"<<endl;
							cout<<"\t\t";

							char z;
							for(int i=0;;i++)
							  {

								 a.pass[i]=getch();            //masking
								 z=a.pass[i];
								if(z==13)
							  {
								a.pass[i]='\0';
								break;
								}
							else if(z==8)
								{
								if(i>0)
								{
								cout<<"\b"<<" "<<"\b";
								i=i-2;
								}

								}
								else putch('*');
										 }

					  }
		f1.write((char*)&a,sizeof(a));
		f1.close();
		}
	 else if(cho=='2')
		{
		char password[20];
		 clrscr();
		 cout<<"\n\t\tLOGIN PAGE :-";
		 char id[100];
		 clrscr();
		 puts("\n\t\tEnter your id:");
		 cout<<"\n\t\t";
		 gets(id);
		 puts("\n\t\tEnter your password:");
		 cout<<"\n\t\t";


		 char y;
		  for(int i=0;;i++)
  {

		 password[i]=getch();
		 y=password[i];
		 if(y==13)
		 {
				password[i]='\0';
				break;
		 }
		 else if(y==8)
		 {
				if(i>0)
				{
						cout<<"\b"<<" "<<"\b";
						i=i-2;
				}

		 }
		 else putch('*');
		 }

	  f1.open("id.dat",ios::in|ios::binary);
	  f1.seekg(0);
  while(f1.read((char*)&a,sizeof(a)))
	 {
		if((strcmp(a.uid,id)==0)&&(strcmp(a.pass,password)==0))
		  {
			do
			  { cout<<"\n*****************************************************************************";
				 cout<<"\n\n";
				 cout<<"\n 1.Reservation Menu";
				 cout<<"\n 2.Cancellation Menu";
				 cout<<"\n 3.Enquiry";
				 cout<<"\n 4.Main menu";
				 cout<<"\n\n\n Enter your choice";
				 cin>>ch;
				 cout<<endl;
	 switch(ch)
	  {
		 case '1':
		 clrscr();
		  reserve();

			break;
		 case '2':
		  clrscr();
		  can();
			break;

		 case '3':
		  clrscr();
		  enquiry();
			break;

		 case '4':
			clrscr();
			loading();
			return;

		 default :
			 cout<<"\n Invalid Choice";
			 cout<<"\n\n Press any key to continue..";
			 getche();
			 clrscr();
	  }
	 }
  while(1);
	goto j;
  }
		else
		  {
			d=1;
		  }
		 }
if (d==1)
 {
  cout<<"\n Enter your correct user-id and password"<<"\n";
	 cout<<"\n\nPress enter to continue";
  f1.close();
  getche();
  clrscr();
  goto l4;
 }
 f1.close();
  j:
  }
	}

 void displaypassdetails()     //displaying passenger details
  {

	cout<<"\t\tPASSENGER DETAILS:- ";
	cout<<"\n_______________________________________________________________________ ";
	fstream f;
	 reser b;
	 f.open ("p.dat",ios::binary|ios::in|ios::out|ios::app);
	 f.seekg(0);
	while(f.read((char*)&b,sizeof(b)))
	 {
	  b.displayresdet();
	  cout<<"\n";
	 }
	f.close();
	cout<<"\n Enter any key to proceed..";
	getch();
  }
 void enquiry()
  {
	train a;
	fstream f;
	 f.open ("t.dat",ios::binary|ios::in|ios::out|ios::app);

	while(f.read((char*)&a, sizeof(a)))
	 {
	  a.displaydetails();
	  cout<<"\n**********************************************************\n";
	 }
	cout<<"\n\nPress Any Key To Proceed...";
	getch();
	clrscr();
  }
 void cancell()           //cancellation function
{
 int flag=0;
  int day,month,year;
  int addr;
	 int ad;
	 int tamt;
	 train a;
	 reser b;
	 canc c;
	fstream f,f2,f3,f4 ;
	  f.open("t.dat",ios::in|ios::out|ios::binary);
	  f2.open("p.dat",ios::in|ios::out|ios::binary|ios::app);
	  f3.open("cn.dat",ios::in|ios::out|ios::binary|ios::app);
	  f4.open("temp.dat",ios::out|ios::binary);
 cout<<"     *~*~*~*~*~*~*~*~*~*~*~*~*~CANCELLATION MENU~*~*~*~*~*~*~*~*~*~*~*~*~*\n";
 l9:
 c.getcancdet();
  while(f2.read((char*)&b,sizeof(b)))
  {
	 if(b.pnr!=c.pnr)
	  { f4.write((char*)&b,sizeof(b));
		 }
	else if (b.pnr==c.pnr)
	  {
		 flag=1;
		c.trainno=b.trainno;
		 strcpy(c.trainname,b.trainname);
		 strcpy(c.bp,b.bp);
		 strcpy(c.destination,b.destination);
		c.nosc=b.nosr;
		 for (int j=0;j<c.nosc;j++)
		  {
			strcpy(c.pname[j],b.pname[j]);
			c.age[j]=b.age[j];
		  }
  strcpy(c.clas,b.clas);
	if((strcmp(c.clas,"C1")==0)||(strcmp(c.clas,"c1")==0))
	 {
	  f.seekg(ios::beg);
	  f.seekp(ios::beg);
	  while(f.read((char*)&a,sizeof(a)))
		{
		 if (c.trainno==a.gettrainno())
		  {
			 day=a.getdate();                       //updating no of seats in train database
			 month=a.getmonth();
			 year=a.getyear();
			addr=f.tellg();
			a.c1=a.c1+c.nosc;
			f.seekp(addr-sizeof(a));
			f.write((char*)&a,sizeof(a));
			int tamt=b.amc;
			if((year>2014)&&(year<=2015))
				{
					if((c.d==day)&&(c.m==month))
						{
						cout<<"\n You are cancelling on the date of departure"<<"\n";
						c.amtr=(tamt*0.4);
						}
					else if(c.m==month)
						{
						cout<<"\n You are cancelling in the month of departure"<<"\n";
						c.amtr=(tamt/2);
						}
				  else if (month>c.m)
						{
					 cout<<"\n You are cancelling month(s) before the date of departure"<<"\n";
				 c.amtr=(tamt*0.8);
						}
				  else
						{
							cout<<"\n You are cancelling after the departure"<<"\n";
							cout<<"\n Sorry...your request cannot be completed"<<"\n";
							goto h;
							}
						}
				c.displaycancdet();
						  }
					 }
				}

 else if ((strcmp(c.clas,"C2")==0)||(strcmp(c.clas,"c2")==0))
	{
	 while(f.read((char*)&a,sizeof(a)))
	 {
		if(a.gettrainno()==c.trainno)
		{
				 day=a.getdate();                          //updating no of seats in train database
				 month=a.getmonth();
				 year=a.getyear();
				 addr=f.tellg();
				 a.c2=a.c2+c.nosc;
				 f.seekp(addr-sizeof(a));
				 f.write((char*)&a,sizeof(a));
				 int tamt=b.amc;
			if ((c.d==day)&&(c.m==month))
				{
				 cout<<"\n You are cancelling on the date of departure"<<"\n";
				 c.amtr=(tamt*0.4);
				}
		  else if (c.m==month)
				{
				  cout<<"\n You are cancelling in the month of departure"<<"\n";
				  c.amtr=(tamt/2);
				}
		  else if (month>c.m)
				{
				  cout<<"\n You are cancelling month(s) before the date of departure"<<"\n";
				  c.amtr=(tamt*0.8);
				 }
		  else
				{
				  cout<<"\n You are cancelling after the departure"<<"\n";
				  cout<<"\n Sorry...your request cannot be completed"<<"\n";
				  goto h;
				 }
		 c.displaycancdet();
		 cout<<"\n\n Please enter any key to proceed...";
		 getche();
		 clrscr();
		}
	  }
	}
  }
else
{
flag=0;
}
}
h:

remove("p.dat");
rename("temp.dat","p.dat");
f.close();
f2.close();
f3.close();
f4.close();
if(flag!=1)
			{
				 cout<<"\n Enter the correct pnr number"<<"\n";
				 cout<<"\n\n\n Please press 'Enter' to proceed\n\n";
				 getche();
				 clrscr();
				 goto l9;
			 }
}

void can()          //function for cancellation menu
{
clrscr();
char ch;
do
{
cout<<"\n\n*~*~*~*~*~*~*~*~*~*~*~*~*~CANCELLATION MENU~*~*~*~*~*~*~*~*~*~*~*~*~*";
cout<<"\n                      1.Cancel";
cout<<"\n                      2.Return to User menu";
cout<<"\n Enter your choice";
cin>>ch;
switch(ch)
{
case '1':
clrscr();
cancell();
break;

case '2':
 clrscr();
 return;

default :
 cout<<"\n\nInvalid Choice.";
 cout<<"\n\t\t Please press any key to proceed..\n";
 getche();
 clrscr();
}
}while(1);
getch();
}