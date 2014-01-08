RUBIKS-CUBE-SOLVER
==================

rubiks cube solver create in cpp

/*
* RUBIKS CUBE SOLVER
* create By :- Moses Gangipogu(location:India)
* Contact: mosesgangipogu@gmail.com
*/
/** GOD BLESS ALL **/

#include<iostream.h>
#include<conio.h>
#include<string.h>
#include<graphics.h>
#include<stdlib.h>
#include<time.h>
int opstring[500];
int demoopstring[500];
int n=0;
int redcount=0;
int redchknum=1;
enum color
{
white,
blue,
green,
red,
yellow,
orange,
};

enum pos
{
tp=1,
bm=2,
ft=3,
rr=4,
lt=5,
rt=6,
};

class rubik
{
int top[3][3],front[3][3],bottom[3][3],rear[3][3],left[3][3],right[3][3];
int scr;
int back_stak[5],t;
public:
rubik::rubik();
int search(int col1,int col2);
long search(int col1,int col2,int col3);
void callcountermove(int move);
void callmove(int move);
void display();
void draw();
void drawface(int face[3][3],int x,int y);
void topright();
void topleft();
void bottomright();
void bottomleft();
void rightup();
void rightdown();
void leftup();
void leftdown();
void rear_clk();
void rear_anticlk();
void front_clk();
void front_anticlk();
void face_change_anti(int face[3][3]);
void face_change(int face[3][3]);
void solve(int pos);
void LastLayerCross();
void LastLayerCrossCorrespondingSideEdges();
void LastLayerCornerEdgesSettling();
void LastLayerCornerEdgesFliping();
void SettlingOfBottomLayer();
void scrumble();
void outputstringredudandancycheak();
void displayoutput();
void toprightnew();
void topleftnew();
void bottomrightnew();
void bottomleftnew();
void rightupnew();
void rightdownnew();
void leftupnew();
void leftdownnew();
void rear_clknew();
void rear_anticlknew();
void front_clknew();
void front_anticlknew();
void copyopstrong();
};

rubik::rubik()
{
//int k=1;
t=0;
for(int m=0;m<5;m++)
back_stak[m]=0;
scr=0;
for(int i=0;i<3;i++)
{
for(int j=0;j<3;j++)
{
top[i][j]=green;
front[i][j]=white;
left[i][j]=red;
right[i][j]=orange;
bottom[i][j]=blue;
rear[i][j]=yellow;
}
}
/*
for(int i=0;i<3;i++)
{
for(int j=0;j<3;j++,k++)
{
top[i][j]=k;
bottom[i][j]=k;
front[i][j]=k;
rear[i][j]=k;
left[i][j]=k;
right[i][j]=k;
}

}
*/
}

/*
tp=1,
bm=2,
ft=3,
rr=4,
lt=5,
rt=6;
*/

/*int rubik::search(int col1,int col2)
{
if(col1==0 && col2==4 || col1==1 && col2==2 || col1==3 || col2==5)
return 0;
if(top[0][1]==col1 && rear[0][1]==col2)
return 1000*tp+100*col1+10*rr+col2;
else if(top[1][0]==col1 && left[0][1]==col2)
return 1000*tp+100*col1+10*lt+col2;
else if(top[1][2]==col1 && right[0][1]==col2)
return 1000*tp+100*col1+10*rt+col2;
else if(top[2][1]==col1 && front[0][1]==col2)
return 1000*tp+100*col1+10*ft+col2;
else if(bottom[0][1]==col1 && front[2][1]==col2)
return 1000*bm+100*col1+10*ft+col2;
else if(bottom[1][0]==col1 && left[2][1]==col2)
return 1000*bm+100*col1+10*lt+col2;
else if(bottom[1][2]==col1 && right[2][1]==col2)
return 1000*bm+100*col1+10*rt+col2;
else if(bottom[2][1]==col1 && rear[2][1]==col2)
return 1000*bm+100*col1+10*rr+col2;
else if(front[1][0]==col1 && left[1][2]==col2)
return 1000*ft+100*col1+10*lt+col2;
else if(front[1][2]==col1 && right[1][0]==col2)
return 1000*ft+100*col1+10*rt+col2;
else if(rear[1][0]==col1 && right[1][2]==col2)
return 1000*rr+100*col1+10*rt+col2;
else if(rear[1][2]==col1 && left[1][0]==col2)
return 1000*rr+100*col1+10*lt+col2;
else
{
int r=search(col2,col1);
return r;
}
} */

int rubik::search(int col1,int col2)
{
static int f=0;
//if(col1==0 && col2==4 || col1==1 && col2==2 || col1==3 || col2==5)
//return 0;
if(top[0][1]==col1 && rear[0][1]==col2)
f=1000*tp+100*col1+10*rr+col2;
else if(top[1][0]==col1 && left[0][1]==col2)
f=1000*tp+100*col1+10*lt+col2;
else if(top[1][2]==col1 && right[0][1]==col2)
f=1000*tp+100*col1+10*rt+col2;
else if(top[2][1]==col1 && front[0][1]==col2)
f=1000*tp+100*col1+10*ft+col2;
else if(bottom[0][1]==col1 && front[2][1]==col2)
f=1000*bm+100*col1+10*ft+col2;
else if(bottom[1][0]==col1 && left[2][1]==col2)
f=1000*bm+100*col1+10*lt+col2;
else if(bottom[1][2]==col1 && right[2][1]==col2)
f=1000*bm+100*col1+10*rt+col2;
else if(bottom[2][1]==col1 && rear[2][1]==col2)
f=1000*bm+100*col1+10*rr+col2;
else if(front[1][0]==col1 && left[1][2]==col2)
f=1000*ft+100*col1+10*lt+col2;
else if(front[1][2]==col1 && right[1][0]==col2)
f=1000*ft+100*col1+10*rt+col2;
else if(rear[1][0]==col1 && right[1][2]==col2)
f=1000*rr+100*col1+10*rt+col2;
else if(rear[1][2]==col1 && left[1][0]==col2)
f=1000*rr+100*col1+10*lt+col2;
else
{
if(++f==1)
f=search(col2,col1);
else
f=0;
}
int pos=f;
f=0;
return pos;
}





/*long rubik::search(int col1,int col2,int col3)
{
static long f=0;
cout<<" "<<f<<" "<<col1<<" "<<col2<<" "<<col3<<endl;
if(front[0][0]==col1 && top[2][0]==col2 && left[0][2]==col3)
{
cout<<ft<<" "<<col1<<" "<<tp<<" "<<col2<<" "<<lt<<" "<<col3<<endl;
f=100000*ft+10000*col1+1000*tp+100*col2+10*lt+col3;
cout<<f<<endl;
}

else if(front[0][2]==col1 && right[0][0]==col2 && top[2][2]==col3)
{
cout<<ft<<" "<<col1<<" "<<tp<<" "<<col2<<" "<<rt<<" "<<col3<<endl;
f=100000*ft+10000*col1+1000*tp+100*col2+10*rt+col3;
cout<<f<<endl;
}
else if(front[2][0]==col1 && left[2][2]==col2 && bottom[0][0]==col3)
{
cout<<ft<<" "<<col1<<" "<<bm<<" "<<col2<<" "<<lt<<" "<<col3<<endl;
f=100000*ft+10000*col1+1000*bm+100*col2+10*lt+col3;
cout<<f<<endl;
}
else if(front[2][2]==col1 && bottom[0][2]==col2 && right[2][0]==col3)
{
cout<<ft<<" "<<col1<<" "<<bm<<" "<<col2<<" "<<rt<<" "<<col3<<endl;
f=100000*ft+10000*col1+1000*bm+100*col2+10*rt+col3;
cout<<f<<endl;
}
else if(top[0][2]==col1 && right[0][2]==col2 && rear[0][0]==col3)
{
cout<<rr<<" "<<col1<<" "<<tp<<" "<<col2<<" "<<rt<<" "<<col3<<endl;
f=100000*rr+10000*col1+1000*tp+100*col2+10*rt+col3;
cout<<f<<endl;
}
else if(top[0][0]==col1 && rear[0][2]==col2 && left[0][0]==col3)
{
cout<<rr<<" "<<col1<<" "<<tp<<" "<<col2<<" "<<lt<<" "<<col3<<endl;
f=100000*rr+10000*col1+1000*tp+100*col2+10*lt+col3;
cout<<f<<endl;
}
else if(rear[2][0]==col1 && right[2][2]==col2 && bottom[2][2]==col3)
{
cout<<rr<<" "<<col1<<" "<<bm<<" "<<col2<<" "<<rt<<" "<<col3<<endl;
f=100000*rr+10000*col1+1000*bm+100*col2+10*rt+col3;
cout<<f<<endl;
}
else if(rear[2][2]==col1 && bottom[2][0]==col2 && left[2][0]==col3)
{
cout<<rr<<" "<<col1<<" "<<bm<<" "<<col2<<" "<<lt<<" "<<col3<<endl;
f=100000*rr+10000*col1+1000*bm+100*col2+10*lt+col3;
cout<<f<<endl;
}
else
{
if(++f==1)
{
cout<<" "<<f<<endl;
f=search(col3,col1,col2);
}
else if(++f==2)
{
cout<<" "<<f<<endl;
f=search(col2,col3,col1);
}
else
f=0;
}
return f;
}*/

long rubik::search(int col1,int col2,int col3)
{
static long f=0l;

if(front[0][0]==col1 && (top[2][0]==col2 || top[2][0]==col3) && (left[0][2]==col2 || left[0][2]==col3))
{
if(top[2][0]==col2 && left[0][2]==col3)
{f=100000l*ft+10000l*col1+1000l*tp+100l*col2+10l*lt+col3;
//cout<<f<<endl;
}
if(top[2][0]==col3 && left[0][2]==col2)
{f=100000l*ft+10000l*col1+1000l*tp+100l*col3+10l*lt+col2;
//cout<<f<<endl;
}
}
else if(front[0][2]==col1 && (top[2][2]==col2 || top[2][2]==col3) && (right[0][0]==col2 || right[0][0]==col3))
{
if(top[2][2]==col2 && right[0][0]==col3)
{f=100000l*ft+10000l*col1+1000l*tp+100l*col2+10l*rt+col3;
//cout<<f<<endl;
}
if(top[2][2]==col3 && right[0][0]==col2)
{f=100000l*ft+10000l*col1+1000l*tp+100l*col3+10l*rt+col2;
//cout<<f<<endl;
}
}
else if(front[2][0]==col1 && (bottom[0][0]==col2 || bottom[0][0]==col3) && (left[2][2]==col2 || left[2][2]==col3))
{
if(bottom[0][0]==col2 && left[2][2]==col3)
{f=100000l*ft+10000l*col1+1000l*bm+100l*col2+10l*lt+col3;
//cout<<f<<endl;
}
if(bottom[0][0]==col3 && left[2][2]==col2)
{f=100000l*ft+10000l*col1+1000l*bm+100l*col3+10l*lt+col2;
//cout<<f<<endl;
}
}
else if(front[2][2]==col1 && (bottom[0][2]==col2 || bottom[0][2]==col3) && (right[2][0]==col2 || right[2][0]==col3))
{
if(bottom[0][2]==col2 && right[2][0]==col3)
{f=100000l*ft+10000l*col1+1000l*bm+100l*col2+10l*rt+col3;
//cout<<f<<endl;
}
if(bottom[0][2]==col3 && right[2][0]==col2)
{f=100000l*ft+10000l*col1+1000l*bm+100l*col3+10l*rt+col2;
//cout<<f<<endl;
}
}
else if(rear[0][0]==col1 && (top[0][2]==col2 || top[0][2]==col3) && (right[0][2]==col2 || right[0][2]==col3))
{
if(top[0][2]==col2 && right[0][2]==col3)
{f=100000l*rr+10000l*col1+1000l*tp+100l*col2+10l*rt+col3;
//cout<<f<<endl;
}
if(top[0][2]==col3 && right[0][2]==col2)
{f=100000l*rr+10000l*col1+1000l*tp+100l*col3+10l*rt+col2;
//cout<<f<<endl;
}
}
else if(rear[0][2]==col1 && (top[0][0]==col2 || top[0][0]==col3) && (left[0][0]==col2 || left[0][0]==col3))
{
if(top[0][0]==col2 && left[0][0]==col3)
{f=100000l*rr+10000l*col1+1000l*tp+100l*col2+10l*lt+col3;
//cout<<f<<endl;
}
if(top[0][0]==col3 && left[0][0]==col2)
{f=100000l*rr+10000l*col1+1000l*tp+100l*col3+10l*lt+col2;
//cout<<f<<endl;
}
}
else if(rear[2][0]==col1 && (bottom[2][2]==col2 || bottom[2][2]==col3) && (right[2][2]==col2 || right[2][2]==col3))
{
if(bottom[2][2]==col2 && right[2][2]==col3)
{f=100000l*rr+10000l*col1+1000l*bm+100l*col2+10l*rt+col3;
//cout<<f<<endl;
}
if(bottom[2][2]==col3 && right[2][2]==col2)
{f=100000l*rr+10000l*col1+1000l*bm+100l*col3+10l*rt+col2;
//cout<<f<<endl;
}
}
else if(rear[2][2]==col1 && (bottom[2][0]==col2 || bottom[2][0]==col3) && (left[2][0]==col2 || left[2][0]==col3))
{
if(bottom[2][0]==col2 && left[2][0]==col3)
{f=100000l*rr+10000l*col1+1000l*bm+100l*col2+10l*lt+col3;
//cout<<f<<endl;
}
if(bottom[2][0]==col3 && left[2][0]==col2)
{f=100000l*rr+10000l*col1+1000l*bm+100l*col3+10l*lt+col2;
//cout<<f<<endl;
}
}

else
{
if(++f==1l)
//cout<<f<<" ser 3 1 2 ";
f=search(col3,col1,col2);
else if(f==2l)
//cout<<f<<" ser 2 3 1 ";
f=search(col2,col3,col1);
else if(f==3l)
f=search(col2,col1,col3);
/*else if(f==4l)
{
cout<<" ser 1 3 2 ";
f=search(col1,col3,col2);
}
/*else if(f==5l)
{
cout<<" ser 3 2 1 ";
f=search(col1,col3,col2);
}*/
else
f=0l;
}
long pos=f;
f=0l;
return pos;
}


void rubik::callmove(int move)
{
switch(move)
{
case 1:topright();break;
case 2:topleft();break;
case 3:bottomright();break;
case 4:bottomleft();break;
case 5:rightup();break;
case 6:rightdown();break;
case 7:leftup();break;
case 8:leftdown();break;
case 9:rear_clk();break;
case 10:rear_anticlk();break;
case 11:front_clk();break;
case 12:front_anticlk();break;
default:break;
}
}

void rubik::callcountermove(int move)
{
if(move%2==0)
callmove(move-1);
else
callmove(move+1);
}

void rubik::display()
{

for(int i=0;i<3;i++)
{
for(int j=0;j<3;j++)
cout<<top[i][j];
cout<<endl;
}
cout<<endl;
for(i=0;i<3;i++)
{
for(int j=0;j<3;j++)
cout<<front[i][j];
cout<<endl;
}
cout<<endl;
for(i=0;i<3;i++)
{
for(int j=0;j<3;j++)
cout<<left[i][j];
cout<<endl;
}
cout<<endl;
for(i=0;i<3;i++)
{
for(int j=0;j<3;j++)
cout<<right[i][j];
cout<<endl;
}
cout<<endl;
for(i=0;i<3;i++)
{
for(int j=0;j<3;j++)
cout<<bottom[i][j];
cout<<endl;
}
cout<<endl;
for(i=0;i<3;i++)
{
for(int j=0;j<3;j++)
cout<<rear[i][j];
cout<<endl;
}
cout<<endl;
}

void rubik::topright()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[0][i];
front[0][i]=left[0][i];
left[0][i]=rear[0][i];
rear[0][i]=right[0][i];
right[0][i]=temp;
}
face_change_anti(top);
//face_change(top);
/*outtextxy(500,10,"top right");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::topleft()
{
int temp;
for(int i=0;i<3;i++)
{
temp=left[0][i];
left[0][i]=front[0][i];
front[0][i]=right[0][i];
right[0][i]=rear[0][i];
rear[0][i]=temp;
}
//face_change_anti(top);
face_change(top);
/*outtextxy(500,10,"top left");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::bottomleft()
{
int temp;
for(int i=0;i<3;i++)
{
temp=left[2][i];
left[2][i]=front[2][i];
front[2][i]=right[2][i];
right[2][i]=rear[2][i];
rear[2][i]=temp;
}
face_change_anti(bottom);
//face_change(top);
/*outtextxy(500,10,"bottom left");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::bottomright()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[2][i];
front[2][i]=left[2][i];
left[2][i]=rear[2][i];
rear[2][i]=right[2][i];
right[2][i]=temp;
}
//face_change_anti(top);
face_change(bottom);
/*outtextxy(500,10,"bottom right");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::rightup()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][2];
front[i][2]=bottom[i][2];
bottom[i][2]=rear[2-i][0];
rear[2-i][0]=top[i][2];
top[i][2]=temp;
}
//face_change_anti(top);
face_change(right);
/*outtextxy(500,10,"right up");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::rightdown()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][2];
front[i][2]=top[i][2];
top[i][2]=rear[2-i][0];
rear[2-i][0]=bottom[i][2];
bottom[i][2]=temp;
}
face_change_anti(right);
//face_change(right);
/*outtextxy(500,10,"right down");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::leftup()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][0];
front[i][0]=bottom[i][0];
bottom[i][0]=rear[2-i][2];
rear[2-i][2]=top[i][0];
top[i][0]=temp;
}
face_change_anti(left);
//face_change(right);
/*outtextxy(500,10,"left up");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::leftdown()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][0];
front[i][0]=top[i][0];
top[i][0]=rear[2-i][2];
rear[2-i][2]=bottom[i][0];
bottom[i][0]=temp;
}
//face_change_anti(top);
face_change(left);
/*outtextxy(500,10,"left down");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::face_change(int face[3][3])
{
int temp;
temp=face[0][0];
face[0][0]=face[2][0];
face[2][0]=face[2][2];
face[2][2]=face[0][2];
face[0][2]=temp;
temp=face[0][1];
face[0][1]=face[1][0];
face[1][0]=face[2][1];
face[2][1]=face[1][2];
face[1][2]=temp;
}

void rubik::face_change_anti(int face[3][3])
{
int temp;
temp=face[0][0];
face[0][0]=face[0][2];
face[0][2]=face[2][2];
face[2][2]=face[2][0];
face[2][0]=temp;
temp=face[0][1];
face[0][1]=face[1][2];
face[1][2]=face[2][1];
face[2][1]=face[1][0];
face[1][0]=temp;
}

void rubik::rear_clk()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[0][i];
top[0][i]=left[2-i][0];
left[2-i][0]=bottom[2][2-i];
bottom[2][2-i]=right[i][2];
right[i][2]=temp;
}
face_change_anti(rear);
//face_change(left);
/*outtextxy(500,10,"rear clk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::rear_anticlk()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[0][i];
top[0][i]=right[i][2];
right[i][2]=bottom[2][2-i];
bottom[2][2-i]=left[2-i][0];
left[2-i][0]=temp;
}
//face_change_anti(rear);
face_change(rear);
/*outtextxy(500,10,"rear anticlk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::front_clk()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[2][i];
top[2][i]=left[2-i][2];
left[2-i][2]=bottom[0][2-i];
bottom[0][2-i]=right[i][0];
right[i][0]=temp;
}
//face_change_anti(rear);
face_change(front);
/*outtextxy(500,10,"front clk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}

void rubik::front_anticlk()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[2][i];
top[2][i]=right[i][0];
right[i][0]=bottom[0][2-i];
bottom[0][2-i]=left[2-i][2];
left[2-i][2]=temp;
}
face_change_anti(front);
//face_change(left);
/*outtextxy(500,10,"front anticlk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);*/
}


void rubik::drawface(int face[3][3],int x,int y)
{
int temp=y;
for(int i=0;i<3;i++,x+=40)
{
y=temp;
for(int j=0;j<3;j++,y+=40)
{
switch(face[i][j])
{
case 0:setfillstyle(1,15);break;
case 1:setfillstyle(1,1);break;
case 2:setfillstyle(1,2);break;
case 3:setfillstyle(1,4);break;
case 4:setfillstyle(1,14);break;
case 5:setfillstyle(1,6);break;
default:break;
}
bar(y+2,x+2,y+38,x+38);
}
}
}

void rubik::draw()  //40
{
drawface(top,10,130);
drawface(front,130,130);
drawface(bottom,250,130);
drawface(left,130,10);
drawface(right,130,250);
drawface(rear,130,370);
}

void setboard()
{
int gd=DETECT,gm;
initgraph(&gd,&gm,"C:\\TC\\BGI\\");
outtextxy(25,25,"Top");

//full
/*
setlinestyle(0,0,3);
rectangle(175,25,325,475);
rectangle(25,175,625,325);
line(475,175,475,325);

setlinestyle(0,0,1);
for(int i=25;i<475;i+=50)
{
if(i==225 || i==275)
line(25,i,625,i);
line(175,i,325,i);
}
for(i=25;i<625;i+=50)
{
if(i==225 || i==275)
line(i,25,i,475);
line(i,175,i,325);
}*/

//half
setlinestyle(0,0,3);
rectangle(130,10,250,370);
rectangle(10,130,490,250);
line(370,130,370,250);

setlinestyle(0,0,1);
for(int i=10;i<=370;i+=40)
{
if(i==170 || i==210)
line(10,i,490,i);
line(130,i,250,i);
}
for(i=10;i<=490;i+=40)
{
if(i==170 || i==210)
line(i,10,i,370);
line(i,130,i,250);
}
getch();
}

void rubik::scrumble()
{
scr=1;
randomize();
for(int i=0;i<12;i++)
callmove(random(12)+1);
scr=0;
getch();
}

void rubik::solve(int pos)
{
gotoxy(25,25);
switch(pos)
{
case 0:break;
case 1031:break;
case 1041://cout<<"\nrrclk.rrclk.br.ld.rranti.lu.br.br";
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 1051://cout<<"\nlu.rranti.ld.br.br";
leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 1061://cout<<"\nru.rrclk.rd.br.br";
rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 2031://cout<<"\nbl.ld.rranti.lu.br.br";
bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 2041://cout<<"\nbr.ld.rranti.lu.br.br";
bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 2051://cout<<"\nld.rranti.lu.br.br";
leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 2061://cout<<"\nbl.bl.ld.rranti.lu.br.br";
bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 4051://cout<<"\nrranti.br.br";
rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 4061://cout<<"\nrrclk.br.br";
rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;


case 1032://cout<<"\ntl"<<"ld"<<"fclk";
topleft();opstring[n]=6;n++;leftdown();opstring[n]=2;n++;front_clk();opstring[n]=9;n++;break;
case 1042://cout<<"\ntl"<<"rd"<<"fanti";
topleft();opstring[n]=6;n++;rightdown();opstring[n]=4;n++;front_anticlk();opstring[n]=10;n++;break;
case 1052://cout<<"\nld"<<"fclk";
leftdown();opstring[n]=2;n++;front_clk();opstring[n]=9;n++;break;
case 1062://cout<<"\nrd"<<"fanti";
rightdown();opstring[n]=4;n++;front_anticlk();opstring[n]=10;n++;break;
case 2032://cout<<"\nbr"<<"ru"<<"fanti";
bottomright();opstring[n]=7;n++;rightup();opstring[n]=3;n++;front_anticlk();opstring[n]=10;n++;break;
case 2042://cout<<"\nrrclk"<<"ld"<<"tr";
rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;topright();opstring[n]=5;n++;break;
case 2052://cout<<"\nlu"<<"fclk";
leftup();opstring[n]=1;n++;front_clk();opstring[n]=9;n++;break;
case 2062://cout<<"\nru"<<"fanti";
rightup();opstring[n]=3;n++;front_anticlk();opstring[n]=10;n++;break;
case 3052://cout<<"\nfclk";
front_clk();opstring[n]=9;n++;break;
case 3062://cout<<"\nfanti";
front_anticlk();opstring[n]=10;n++;break;
case 4052://cout<<"\nld"<<"ld"<<"fclk";
leftdown();opstring[n]=2;n++;leftdown();opstring[n]=2;n++;front_clk();opstring[n]=9;n++;break;
case 4062://cout<<"\nrranti"<<"tl"<<"tl";
rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;topleft();opstring[n]=6;n++;break;



case 1043://cout<<"\nrranti"<<"rranti"<<"br"<<"lu";
rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 1053://cout<<"\nld";
leftdown();opstring[n]=2;n++;break;
case 1063://cout<<"\nrd"<<"rd"<<"bl"<<"bl"<<"lu";
rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftup();opstring[n]=1;n++;break;
case 2033://cout<<"\nbl"<<"lu";
bottomleft();opstring[n]=8;n++;leftup();opstring[n]=1;n++;break;
case 2043://cout<<"\nbr"<<"lu";
bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 2053://cout<<"\nlu";
leftup();opstring[n]=1;n++;break;
case 2063://cout<<"\nbl.bl.lu";
bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftup();opstring[n]=1;n++;break;
case 3053://cout<<"\nno change";
break;
case 3063://cout<<"\nrd.bl.bl.lu";
rightdown();opstring[n]=4;n++;bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftup();opstring[n]=1;n++;break;
case 4053://cout<<"\nld.ld";
leftdown();opstring[n]=2;n++;leftdown();opstring[n]=2;n++;break;
case 4063://cout<<"\nru.bl.bl.lu";
rightup();opstring[n]=3;n++;bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftup();opstring[n]=1;n++;break;



case 1045://cout<<"\nrrclk.rrclk.bl.ru";
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 1055://cout<<"\ntl.rrclk.tr.rrclk.bl.ru";
topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 1065://cout<<"\nrd";
rightdown();opstring[n]=4;n++;break;
case 2035://cout<<"\nbr.ru";
bottomright();opstring[n]=7;n++;rightup();opstring[n]=3;n++;break;
case 2045://cout<<"\nbl.ru";
bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 2055://cout<<"\nbr.br.ru";
bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;rightup();opstring[n]=3;n++;break;
case 2065://cout<<"\nru";
rightup();opstring[n]=3;n++;break;

case 3065://cout<<"\nno change";
break;
case 4055://cout<<"\nrrclk.rrclk.rd.rd";
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;break;
case 4065://cout<<"\nrd.rd";
rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;break;


case 1140://cout<<"\nrrclk.rrclk.br.br";
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 1150://cout<<"\nlu.rranti.ld.br.ld.rranti.lu.br.br";
leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 1160://cout<<"\nru.rrclk.rd.br.ld.rranti.lu.br.br";
rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 2130://cout<<"\nNo change";
break;
case 2140://cout<<"\nbr.br";
bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 2150://cout<<"\nbr";
bottomright();opstring[n]=7;n++;break;
case 2160://cout<<"\nbl";
bottomleft();opstring[n]=8;n++;break;
case 4150://cout<<"\nrranti.br.ld.rranti.lu.br.br";
rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;
case 4160://cout<<"\nrrclk.br.ld.rranti.lu.br.br";
rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;break;




case 1230://cout<<"\nno change";
break;
case 1240://cout<<"\ntl"<<"tl";
topleft();opstring[n]=6;n++;topleft();opstring[n]=6;n++;break;
case 1250://cout<<"\ntr";
topright();opstring[n]=5;n++;break;
case 1260://cout<<"\ntl";
topleft();opstring[n]=6;n++;break;
case 2230://cout<<"\nfanti"<<"fanti";
front_anticlk();opstring[n]=10;n++;front_anticlk();opstring[n]=10;n++;break;
case 2240://cout<<"\nrrclk"<<"ld"<<"ld"<<"fclk";
rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;leftdown();opstring[n]=2;n++;front_clk();opstring[n]=9;n++;break;
case 2250://cout<<"\nlu"<<"lu"<<"tr";
leftup();opstring[n]=1;n++;leftup();opstring[n]=1;n++;topright();opstring[n]=5;n++;break;
case 2260://cout<<"\nru"<<"ru"<<"tl";
rightup();opstring[n]=3;n++;rightup();opstring[n]=3;n++;topleft();opstring[n]=6;n++;break;
case 3250://cout<<"\nlu"<<"tr";
leftup();opstring[n]=1;n++;topright();opstring[n]=5;n++;break;
case 3260://cout<<"\nru"<<"tl";
rightup();opstring[n]=3;n++;topleft();opstring[n]=6;n++;break;
case 4250://cout<<"\nld"<<"tr";
leftdown();opstring[n]=2;n++;topright();opstring[n]=5;n++;break;
case 4260://cout<<"\nrranti"<<"tl"<<"rd"<<"fanti";
rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rightdown();opstring[n]=4;n++;front_anticlk();opstring[n]=10;n++;break;



case 1340://cout<<"\nrranti.ld.ld";
rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;leftdown();opstring[n]=2;n++;break;
case 1350://cout<<"\nlu.rranti.br.lu";
leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;

case 1360://cout<<"\nrd.rd.bl.bl.ld.rranti.br.lu";
rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 2330://cout<<"\nbl.ld.rranti.br.lu";
bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 2340://cout<<"\nbr.ld.rranti.br.lu";
bottomright();opstring[n]=7;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 2350://cout<<"\nld.rranti.br.lu";
leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 2360://cout<<"\nbl.bl.ld.rranti.br.lu";
bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 3350://cout<<"\nlu.lu.rranti.br.lu";
leftup();opstring[n]=1;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 3360://cout<<"\nrd.bl.bl.ld.rranti.br.lu";
rightdown();opstring[n]=4;n++;bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 4350://cout<<"\nrranti.br.lu";
rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;
case 4360://cout<<"\nru.bl.bl.ld.rranti.br.lu";
rightup();opstring[n]=3;n++;bottomleft();opstring[n]=8;n++;bottomleft();opstring[n]=8;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;leftup();opstring[n]=1;n++;break;

case 1540://cout<<"\nrrclk.rd.rd";
rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;break;
case 1550://cout<<"\ntl.rrclk.tr.rd.rd";
topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;break;
case 1560://cout<<"\nru.rrclk.bl.ru";
rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 2530://cout<<"\nbr.rd.rrclk.bl.ru";
bottomright();opstring[n]=7;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 2540://cout<<"\nrranti.rd.rd";
rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rightdown();opstring[n]=4;n++;break;
case 2550://cout<<"\nbr.br.rd.rrclk.bl.ru";
bottomright();opstring[n]=7;n++;bottomright();opstring[n]=7;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 2560://cout<<"\nrd.rrclk.bl.ru";
rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 3560://cout<<"\nru.ru.rrclk.bl.ru";
rightup();opstring[n]=3;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 4550://cout<<"\nrranti.bl.ru";
rear_anticlk();opstring[n]=12;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;
case 4560://cout<<"\nrrclk.bl.ru";
rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rightup();opstring[n]=3;n++;break;



//green red (top4 left2)
case 1253://cout<<"no change";
break;
case 1352://cout<<"lu.reanti.ld.reanti.tl.reclk.tr";

leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;
solve(search(green,red));break;
case 1243://cout<<"reclk.lu.reanti.ld.reanti.tl.reclk.tr";
 
rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;
solve(search(green,red));
break;
case 1342: //cout<<"reanti.reanti.tl.reclk.tr.reclk.lu.reanti.ld";

rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;
break;
case 4352: //cout<<"reclk.reclk.lu.reanti.ld.reanti.tl.reclk.tr";
 
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;
break;
case 4253: //cout<<"reanti.tl.reclk.tr.reclk.lu.reanti.ld";

rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;
break;
case 2342:
case 2243: //cout<<"reclk";
 
rear_clk();opstring[n]=11;n++;
solve(search(green,red));
break;
case 4263:
case 4362: //cout<<"reanti.";
 
rear_anticlk();opstring[n]=12;n++;
solve(search(green,red));
break;
case 1263:
case 1362: //cout<<"ru.reclk.rd.reclk.tr.reanti.tl";
 
rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;
solve(search(green,red));
break;
case 2362:
case 2263: //cout<<"rd.reanti.ru.reanti.br.reclk.bl";
 
rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;
solve(search(green,red));
break;
case 2253:
case 2352: //cout<<"ld.reclk.lu.reclk.bl.reanti.br";
 
leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;
solve(search(green,red));
break;


//green orange (top6 right2)

case 1265: //cout<<"nochange";
break;
case 1562: //cout<<"ru.reclk.rd.reclk.tr.reanti.tl";

rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;
solve(search(green,orange));
break;
case 1245: //cout<<"reanti.ru.reclk.rd.reclk.tr.reanti.tl";

rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;
break;
case 1542: //cout<<"reclk.reclk.tr.reanti.tl.reanti.ru.reclk.rd";

rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;
break;
case 4562: //cout<<"reanti.reanti.ru.reclk.rd.reclk.tr.reanti.tl";

rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;
break;
case 4265: //cout<<"reanti.reclk.reclk.tr.reanti.tl.reanti.ru.reclk.rd";

rear_anticlk();opstring[n]=12;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;
break;
case 4255:
case 4552: //cout<<"reclk";

rear_clk();opstring[n]=11;n++;
solve(search(green,orange));
break;
case 2542:
case 2245: //cout<<"reclk.reclk";

rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;
solve(search(green,orange));
break;
case 2562:
case 2265: //cout<<"rd.reanti.ru.reanti.br.reclk.bl";

rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;
solve(search(green,orange));
break;
case 2255:
case 2552: //cout<<"ld.reclk.lu.reclk.bl.reanti.br";

leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;
solve(search(green,orange));
break;



//red blue (left8 bottom4)

case 2153: //cout<<"no change";
break;
case 2351: //cout<<"ld.reclk.lu.reclk.bl.reanti.br";

leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;
solve(search(red,blue));
break;
case 2143: //cout<<"reanti.ld.reclk.lu.reclk.bl.reanti.br";

rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;
break;
case 2341: //cout<<"reclk.reclk.bl.reanti.br.reanti.ld.reclk.lu";

rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;
break;
case 4351:
case 4153: //cout<<"reanti";
rear_anticlk();opstring[n]=12;n++;
solve(search(red,blue));
break;
case 1143:
case 1341: //cout<<"reanti.reanti";

rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;
solve(search(red,blue));
break;
case 4361:
case 4163: //cout<<"reclk";

rear_clk();opstring[n]=11;n++;
solve(search(red,blue));
break;
case 2361:
case 2163: //cout<<"rd.reanti.ru.reanti.br.reclk.bl";

rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;
solve(search(red,blue));
break;





//orange blue (right8 bottom6)


case 2165: //cout<<"no change";
break;
case 2561: //cout<<".rd.reanti.ru.reanti.br.reclk.bl";

rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;
solve(search(orange,blue));
break;
case 2145: //cout<<".reclk.rd.reanti.ru.reanti.br.reclk.bl";

rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;
break;

case 2541: //cout<<".reclk.reclk.br.reclk.bl.reclk.rd.reanti.ru";

rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;
break;

case 4165:
case 4561: //cout<<"reclk.";

rear_clk();opstring[n]=11;n++;
solve(search(orange,blue));
break;
case 1541:
case 1145: //cout<<"reclk.reclk.";

rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;
solve(search(orange,blue));
break;
case 4155:
case 4551: //cout<<"reanti.";

rear_anticlk();opstring[n]=12;n++;
solve(search(orange,blue));
break;




//3 colors

//white green red
case 301253: //cout<<"no";
break;
case 331052: //cout<<"lu.reanti.ld.reclk.lu.reanti.ld";
leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;break;
case 321350: //cout<<"lu.reclk.ld.reanti.reanti.tl.reclk.tr";
leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;break;
case 421053: //cout<<"reclk.lu.reanti.ld";
rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;break;
case 431250: //cout<<"reanti.tl.reclk.tr";
rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;break;
case 401352: //cout<<"lu.reclk.reclk.ld.reanti.reanti.tl.reclk.tr";
leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;break;

case 431062:
case 401263:
case 421360:
//cout<<"reanti";
rear_anticlk();opstring[n]=12;n++;solve(search(white,green,red));
break;


case 422063:
case 432260:
case 402362:
//cout<<"reanti.reanti";
rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;solve(search(white,green,red));break;

case 422350:
case 432052:
case 402253:
//cout<<"reclk";
rear_clk();opstring[n]=11;n++;solve(search(white,green,red));break;


case 331260:
case 301362:
case 321063:
//cout<<"ru.reanti.rd";
rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;solve(search(white,green,red));break;


case 332062:
case 302263:
case 322360:
//cout<<"rd.reanti.reanti.ru";
rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;solve(search(white,green,red));break;


case 322053:
case 332250:
case 302352:
//cout<<"ld.reclk.reclk.lu.reanti";
leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;solve(search(white,green,red));break;


//white green orange

case 301265: //cout<<"no change";
break;
case 321560: //cout<<"ru.reanti.rd.reclk.reclk.tr.reanti.tl";
rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;break;
case 351062: //cout<<"tr.reclk.tl.reanti.reanti.ru.reclk.rd";
topright();opstring[n]=5;n++;rear_clk();opstring[n]=11;n++;topleft();opstring[n]=6;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;break;
case 421065: //cout<<"reanti.ru.reclk.rd";
rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;break;
case 451260: //cout<<"reclk.tr.reanti.tl";
rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;break;
case 401562: //cout<<"tr.reclk.reclk.tl.reanti.reanti.ru.reclk.rd";
topright();opstring[n]=5;n++; rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;topleft();opstring[n]=6;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;break;


case 422560:
case 452062:
case 402265://cout<<"reanti";
rear_anticlk();opstring[n]=12;n++;solve(search(white,green,orange));break;

case 421550:
case 451052:
case 401255://cout<<"reclk";
rear_clk();opstring[n]=11;n++;solve(search(white,green,orange));break;

case 422055:
case 452250:
case 402552://cout<<"reclk.reclk";
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;solve(search(white,green,orange));break;

case 302562:
case 322065:
case 352260://cout<<"rd.reanti.reanti.ru.reclk";
rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++; solve(search(white,green,orange));break;


case 322550:
case 352052:
case 302255://cout<<"ld.reclk.reclk.lu";
leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;solve(search(white,green,orange));break;

//white blue red
case 302153: //cout<<"no change";
break;
case 312350: //cout<<"bl.reanti.br.reclk.bl.reanti.br";
bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;break;
case 332051: //cout<<"bl.reclk.br.reanti.reanti.ld.reclk.lu";
bottomleft();opstring[n]=8;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;break;
case 412053: //cout<<"reanti.ld.reclk.lu";
rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;break;
case 432150: //cout<<"reclk.bl.reanti.br";
rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;break;
case 402351: //cout<<"bl.reclk.reclk.br.reanti.reanti.ld.reclk.lu";
bottomleft();opstring[n]=8;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;break;

case 412360:
case 432061:
case 402163: //cout<<"reclk";
rear_clk();opstring[n]=11;n++;solve(search(white,blue,red));break;


case 411350:
case 431051:
case 401153: //cout<<"reanti";
rear_anticlk();opstring[n]=12;n++;solve(search(white,blue,red));break;

case 411063:
case 431160:
case 401361: //cout<<"reclk.reclk";
rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;solve(search(white,blue,red));break;

case 302361:
case 312063:
case 332160: //cout<<"rd.reclk.ru";
rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;rightup();opstring[n]=3;n++;solve(search(white,blue,red));break;

//WHITE BLUE ORANGE

case 302165: //cout<<"no change";
break;
case 312560: //cout<<"rd.reclk.ru.reanti.reanti.br.reclk.bl";
rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;break;
case 352061: //cout<<"br.reanti.bl.reclk.reclk.rd.reanti.ru";
bottomright();opstring[n]=7;n++;rear_anticlk();opstring[n]=12;n++;bottomleft();opstring[n]=8;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;break;
case 452160: //cout<<"reanti.br.reclk.bl";
rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;break;
case 402561: //cout<<"rd.reclk.reclk.ru.reanti.reanti.br.reclk.bl";
rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;rear_clk();opstring[n]=11;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;break;
case 412065: //cout<<"reclk.rd.reanti.ru";
rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;break;

case 451061:
case 401165:
case 411560: //cout<<"reclk";
rear_clk();opstring[n]=11;n++; solve(search(white,blue,orange)); break;

case 452051:
case 402155:
case 412550: //cout<<"reanti";
rear_anticlk();opstring[n]=12;n++; solve(search(white,blue,orange)); break;

case 451150:
case 401551:
case 411055: //cout<<"reanti.reanti";
rear_anticlk();opstring[n]=12;n++; rear_anticlk();opstring[n]=12;n++;  solve(search(white,blue,orange)); break;


}
}


void rubik::LastLayerCross()
{
gotoxy(25,25);
static int a=0;
if(rear[0][1]==4 && rear[1][0]==4 && rear[1][1]==4 && rear[1][2]==4 && rear[2][1]==4)
{
//cout<<"no change";
//opstring[n]=0;n++;

}
/*else if(rear[1][0]==4 && rear[1][1]==4 && rear[1][2]==4 && rear[0][1]!=4 && rear[2][1]!=4)
{
//cout<<"TL.RU.ReAnti.RD.ReClk.TR";

topleft();opstring[n]=6;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;
}*/
else if((rear[0][1]==4 && rear[1][1]==4 && rear[2][1]==4) || (rear[1][0]==4 && rear[1][1]==4 && rear[1][2]==4))
{
//cout<<"ReClk.TL.RU.ReAnti.RD.ReClk.TR";

rear_clk();opstring[n]=11;n++;topleft();opstring[n]=6;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;
LastLayerCross();
}
else
{
a=a+1;
//cout<<"TL.RU.ReAnti.RD.ReClk.TR";
topleft();opstring[n]=6;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;
if(a>3)
{
//cout<<"ReAnti.";
rear_anticlk();opstring[n]=12;n++;
}
LastLayerCross();
}
}




void rubik::LastLayerCrossCorrespondingSideEdges()
{
gotoxy(25,25);
static int a=0;
for(int i=0;i<4;i++)
{
if(top[0][1]==2 && left[1][0]==3 && bottom[2][1]==1 && right[1][2]==5)
{
//cout<<"no change";
//opstring[n]=0;n++;
break;
}
else
{
//cout<<"ReAnti.";

rear_anticlk();opstring[n]=12;n++;
}
}
if(top[0][1]==2 && left[1][0]==3 && bottom[2][1]==1 && right[1][2]==5)
{
//cout<<"no change";
//opstring[n]=0;n++;
}
else if((left[1][0]==3 && right[1][2]==5) || (bottom[2][1]==1 && right[1][2]==5))
{
//cout<<".RU.Reanti.RD.Reanti.RU.Reanti.Reanti.RD";

rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;
LastLayerCrossCorrespondingSideEdges();
}

else if((bottom[2][1]==1 && top[0][1]==2) || (right[1][2]==5 && top[0][1]==2))
{
//cout<<"TL.Reanti.TR.Reanti.TL.Reanti.Reanti.TR";

topleft();opstring[n]=6;n++;rear_anticlk();opstring[n]=12;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;topright();opstring[n]=5;n++;
LastLayerCrossCorrespondingSideEdges();
}

else if((left[1][0]==3 && right[1][2]==5) || (top[0][1]==2 && left[1][0]==3))
{
//cout<<"LD.Reanti.LU.Reanti.LD.Reanti.Reanti.LU";

leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;
LastLayerCrossCorrespondingSideEdges();
}

else if((bottom[2][1]==1 && top[0][1]==2) || (left[1][0]==3 && bottom[2][1]==1))
{
//cout<<"BR.Reanti.BL.Reanti.BR.Reanti.Reanti.BL";

bottomright();opstring[n]=7;n++;rear_anticlk();opstring[n]=12;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;bottomleft();opstring[n]=8;n++;
LastLayerCrossCorrespondingSideEdges();
}
else
{
a=a+1;
if(a>2)
{
//cout<<"ReAnti.";

rear_anticlk();opstring[n]=12;n++;
}
else{
//cout<<".RU.Reanti.RD.Reanti.RU.Reanti.Reanti.RD.Reanti";

rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_anticlk();opstring[n]=12;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;
}
LastLayerCrossCorrespondingSideEdges();
}

}




void rubik::LastLayerCornerEdgesSettling()
{
gotoxy(25,25);
if(((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
&& ((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
&& ((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
&& ((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3)))
{
//cout<<"no change";
//opstring[n]=0;n++;
}

else if((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
{
for(int i=0;i<2;i++)
{
if(((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
&& ((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
&& ((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
&& ((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3)))
{
break;
}
else
{
//cout<<"Reanti.RU.Reclk.LU.Reanti.RD.Reclk.LD";

rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;
}
}
LastLayerCornerEdgesSettling();
}

else if((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
{
for(int i=0;i<3;i++)
{

if(((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
&& ((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
&& ((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
&& ((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3)))
{
break;
}
else
{
//cout<<"Reanti.TL.Reclk.BL.Reanti.TR.Reclk.BR";

rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;topright();opstring[n]=5;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;
}
}
LastLayerCornerEdgesSettling();
}

else if((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
{
for(int i=0;i<3;i++)
{
if(((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
&& ((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
&& ((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
&& ((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3)))
{
break;
}
else
{
//cout<<"Reanti.BR.Reclk.TR.Reanti.BL.Reclk.TL";

rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;bottomleft();opstring[n]=8;n++;rear_clk();opstring[n]=11;n++;topleft();opstring[n]=6;n++;
}
}
LastLayerCornerEdgesSettling();
}

else if((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3))
{
for(int i=0;i<3;i++)
{
if(((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
&& ((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
&& ((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
&& ((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3)))
{
break;
}
else
{
//cout<<"Reanti.LD.Reclk.RD.Reanti.LU.Reclk.RU";

rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;rightup();opstring[n]=3;n++;
}
}
LastLayerCornerEdgesSettling();
}

else
{
//cout<<"Reanti.RU.Reclk.LU.Reanti.RD.Reclk.LD";

rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;
LastLayerCornerEdgesSettling();
}
}



/*
void rubik::LastLayerCornerEdgesSettling()
{
gotoxy(25,25);
long ygo=search(yellow,green,orange);
long ygr=search(yellow,green,red);
long ybo=search(yellow,blue,orange);
long ybr=search(yellow,blue,red);
if((ygo==441265 || ygo==421564 || ygo==451462)
&& (ygr==441253 || ygr==431452 || ygr==421354)
&& (ybo==442165 || ybo==452461 || ybo==412564)
&& (ybr==441153 || ybr==431451 || ybr==411354)) 
{
//cout<<"no change";
//opstring[n]=0;n++;
}

else if((rear[0][0]==4 || top[0][2]==4 || right[0][2]==4) && (rear[0][0]==2 || top[0][2]==2 || right[0][2]==2) && (rear[0][0]==5 || top[0][2]==5 || right[0][2]==5))
{
for(int i=0;i<3;i++)
{
long ygo=search(yellow,green,orange);
long ygr=search(yellow,green,red);
long ybo=search(yellow,blue,orange);
long ybr=search(yellow,blue,red);
if((ygo==441265 || ygo==421564 || ygo==451462)
&& (ygr==441253 || ygr==431452 || ygr==421354)
&& (ybo==442165 || ybo==452461 || ybo==412564)
&& (ybr==441153 || ybr==431451 || ybr==411354)) 
{
break;
}
else
{
//cout<<"Reanti.RU.Reclk.LU.Reanti.RD.Reclk.LD";

rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;
}
}
LastLayerCornerEdgesSettling();
}

else if((rear[0][2]==4 || top[0][0]==4 || left[0][0]==4) && (rear[0][2]==2 || top[0][0]==2 || left[0][0]==2) && (rear[0][2]==3 || top[0][0]==3 || left[0][0]==3))
{
for(int i=0;i<3;i++)
{
long ygo=search(yellow,green,orange);
long ygr=search(yellow,green,red);
long ybo=search(yellow,blue,orange);
long ybr=search(yellow,blue,red);
if((ygo==441265 || ygo==421564 || ygo==451462)
&& (ygr==441253 || ygr==431452 || ygr==421354)
&& (ybo==442165 || ybo==452461 || ybo==412564)
&& (ybr==441153 || ybr==431451 || ybr==411354)) 
{
break;
}
else
{
//cout<<"Reanti.TL.Reclk.BL.Reanti.TR.Reclk.BR";

rear_anticlk();opstring[n]=12;n++;topleft();opstring[n]=6;n++;rear_clk();opstring[n]=11;n++;bottomleft();opstring[n]=8;n++;rear_anticlk();opstring[n]=12;n++;topright();opstring[n]=5;n++;rear_clk();opstring[n]=11;n++;bottomright();opstring[n]=7;n++;
}
}
LastLayerCornerEdgesSettling();
}

else if((rear[2][0]==4 || bottom[2][2]==4 || right[2][2]==4) && (rear[2][0]==1 || bottom[2][2]==1 || right[2][2]==1) && (rear[2][0]==5 || bottom[2][2]==5 || right[2][2]==5))
{
for(int i=0;i<3;i++)
{
long ygo=search(yellow,green,orange);
long ygr=search(yellow,green,red);
long ybo=search(yellow,blue,orange);
long ybr=search(yellow,blue,red);
if((ygo==441265 || ygo==421564 || ygo==451462)
&& (ygr==441253 || ygr==431452 || ygr==421354)
&& (ybo==442165 || ybo==452461 || ybo==412564)
&& (ybr==441153 || ybr==431451 || ybr==411354)) 
{
break;
}
else
{
//cout<<"Reanti.BR.Reclk.TR.Reanti.BL.Reclk.TL";

rear_anticlk();opstring[n]=12;n++;bottomright();opstring[n]=7;n++;rear_clk();opstring[n]=11;n++;topright();opstring[n]=5;n++;rear_anticlk();opstring[n]=12;n++;bottomleft();opstring[n]=8;n++;rear_clk();opstring[n]=11;n++;topleft();opstring[n]=6;n++;
}
}
LastLayerCornerEdgesSettling();
}

else if((rear[2][2]==4 || bottom[2][0]==4 || left[2][0]==4) && (rear[2][2]==1 || bottom[2][0]==1 || left[2][0]==1) && (rear[2][2]==3 || bottom[2][0]==3 || left[2][0]==3))
{
for(int i=0;i<3;i++)
{
long ygo=search(yellow,green,orange);
long ygr=search(yellow,green,red);
long ybo=search(yellow,blue,orange);
long ybr=search(yellow,blue,red);
if((ygo==441265 || ygo==421564 || ygo==451462)
&& (ygr==441253 || ygr==431452 || ygr==421354)
&& (ybo==442165 || ybo==452461 || ybo==412564)
&& (ybr==441153 || ybr==431451 || ybr==411354)) 
{
break;
}
else
{
//cout<<"Reanti.LD.Reclk.RD.Reanti.LU.Reclk.RU";

rear_anticlk();opstring[n]=12;n++;leftdown();opstring[n]=2;n++;rear_clk();opstring[n]=11;n++;rightdown();opstring[n]=4;n++;rear_anticlk();opstring[n]=12;n++;leftup();opstring[n]=1;n++;rear_clk();opstring[n]=11;n++;rightup();opstring[n]=3;n++;
}
}
LastLayerCornerEdgesSettling();
}

else
{
//cout<<"Reanti.RU.Reclk.LU.Reanti.RD.Reclk.LD";

rear_anticlk();opstring[n]=12;n++;rightup();opstring[n]=3;n++;rear_clk();opstring[n]=11;n++;leftup();opstring[n]=1;n++;rear_anticlk();opstring[n]=12;n++;rightdown();opstring[n]=4;n++;rear_clk();opstring[n]=11;n++;leftdown();opstring[n]=2;n++;
LastLayerCornerEdgesSettling();
}
}
*/



void rubik::LastLayerCornerEdgesFliping()
{
gotoxy(25,25);
if((rear[0][0]==4 && top[0][2]==2 && right[0][2]==5) 
&& (rear[0][2]==4 && top[0][0]==2 && left[0][0]==3)
&& (rear[2][0]==4 && bottom[2][2]==1 && right[2][2]==5)
&& (rear[2][2]==4 && bottom[2][0]==1 && left[2][0]==3))
{
//cout<<"no change";
//opstring[n]=0;n++;
}
else if(rear[0][0]==4)
{
//cout<<"RearAntiClk";

rear_anticlk();opstring[n]=12;n++;
LastLayerCornerEdgesFliping();
}
else
{
//cout<<"RD.FrontAntiCLK.RU.FrontCLK";

rightdown();opstring[n]=4;n++;front_anticlk();opstring[n]=10;n++;rightup();opstring[n]=3;n++;front_clk();opstring[n]=9;n++;
LastLayerCornerEdgesFliping();
}
}





void rubik::SettlingOfBottomLayer()
{
gotoxy(25,25);
if((front[1][1]==front[2][1])
&& (right[1][1]==right[2][1])
&& (rear[1][1]==rear[2][1])
&& (left[1][1]==left[2][1]))
{
//cout<<"\n No change";
//opstring[n]=0;n++;
}
else
{
//cout<<"BottomRight.";

bottomright();opstring[n]=7;n++;
SettlingOfBottomLayer();
}
}






void rubik::outputstringredudandancycheak()
{
redchknum=1;
//redcount++;
for(int k=0;k<(n+1);k++)
{
if(opstring[k]==0)
continue;
else
{
int t=k;
//cout<<"\n";
//cout<<opstring[t];
//cout<<opstring[t+1];
//cout<<opstring[t+2];
//cout<<opstring[t+3];
t=k;
if((opstring[t]==1) && (opstring[t+1]==1) && (opstring[t+2]==1) && (opstring[t+3]==1))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==2) && (opstring[t+1]==2) && (opstring[t+2]==2) && (opstring[t+3]==2))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==3) && (opstring[t+1]==3) && (opstring[t+2]==3) && (opstring[t+3]==3))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==4) && (opstring[t+1]==4) && (opstring[t+2]==4) && (opstring[t+3]==4))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==5) && (opstring[t+1]==5) && (opstring[t+2]==5) && (opstring[t+3]==5))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==6) && (opstring[t+1]==6) && (opstring[t+2]==6) && (opstring[t+3]==6))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==7) && (opstring[t+1]==7) && (opstring[t+2]==7) && (opstring[t+3]==7))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==8) && (opstring[t+1]==8) && (opstring[t+2]==8) && (opstring[t+3]==8))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==9) && (opstring[t+1]==9) && (opstring[t+2]==9) && (opstring[t+3]==9))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==10) && (opstring[t+1]==10) && (opstring[t+2]==10) && (opstring[t+3]==10))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==11) && (opstring[t+1]==11) && (opstring[t+2]==11) && (opstring[t+3]==11))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else if((opstring[t]==12) && (opstring[t+1]==12) && (opstring[t+2]==12) && (opstring[t+3]==12))
{
opstring[t]=0;opstring[t+1]=0;opstring[t+2]=0;opstring[t+3]=0;redchknum=0;
}
else
{
continue;
}
}
}

for(k=0;k<(n+1);k++)
{
if(opstring[k]==0)
continue;
else
{
int t=k;
//cout<<"\n";
//cout<<opstring[t];
//cout<<opstring[t+1];
//cout<<opstring[t+2];
/*cout<<opstring[t+3];*/
t=k;
if((opstring[t]==1) && (opstring[t+1]==1) && (opstring[t+2]==1))
{
opstring[t]=2;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==2) && (opstring[t+1]==2) && (opstring[t+2]==2))
{
opstring[t]=1;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==3) && (opstring[t+1]==3) && (opstring[t+2]==3))
{
opstring[t]=4;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==4) && (opstring[t+1]==4) && (opstring[t+2]==4))
{
opstring[t]=3;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==5) && (opstring[t+1]==5) && (opstring[t+2]==5))
{
opstring[t]=6;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==6) && (opstring[t+1]==6) && (opstring[t+2]==6))
{
opstring[t]=5;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==7) && (opstring[t+1]==7) && (opstring[t+2]==7))
{
opstring[t]=8;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==8) && (opstring[t+1]==8) && (opstring[t+2]==8))
{
opstring[t]=7;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==9) && (opstring[t+1]==9) && (opstring[t+2]==9))
{
opstring[t]=10;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==10) && (opstring[t+1]==10) && (opstring[t+2]==10))
{
opstring[t]=9;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==11) && (opstring[t+1]==11) && (opstring[t+2]==11))
{
opstring[t]=12;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else if((opstring[t]==12) && (opstring[t+1]==12) && (opstring[t+2]==12))
{
opstring[t]=11;opstring[t+1]=0;opstring[t+2]=0;redchknum=0;
}
else
{
continue;
}
}
}
for(k=0;k<(n+1);k++)
{
if(opstring[k]==0)
continue;
else
{
int t=k;
//cout<<"\n";
//cout<<opstring[t];
//cout<<opstring[t+1];
/*cout<<opstring[t+2];
cout<<opstring[t+3];*/
t=k;
if((opstring[t]==1) && (opstring[t+1]==2))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==2) && (opstring[t+1]==1))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==3) && (opstring[t+1]==4))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==4) && (opstring[t+1]==3))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==5) && (opstring[t+1]==6))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==6) && (opstring[t+1]==5))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==7) && (opstring[t+1]==8))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==8) && (opstring[t+1]==7))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==9) && (opstring[t+1]==10))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==10) && (opstring[t+1]==9))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==11) && (opstring[t+1]==12))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else if((opstring[t]==12) && (opstring[t+1]==11))
{
opstring[t]=0;opstring[t+1]=0;redchknum=0;
}
else
{
continue;
}
}
}
}



void rubik::displayoutput()
{

for(int k=0;k<(500);k++)
{
if(opstring[k]==0)
continue;
else if(opstring[k]==1)
{
//cout<<"\nLEFT UP";
leftupnew();redcount++;
}
else if(opstring[k]==2)
{
//cout<<"\nLEFT DOWN";
leftdownnew();redcount++;
}
else if(opstring[k]==3)
{
//cout<<"\nRIGHT UP";
rightupnew();redcount++;
}
else if(opstring[k]==4)
{
//cout<<"\nRIGHT DOWN";
rightdownnew();redcount++;
}
else if(opstring[k]==5)
{
//cout<<"\nTOP RIGHT";
toprightnew();redcount++;
}
else if(opstring[k]==6)
{
//cout<<"\nTOP LEFT";
topleftnew();redcount++;
}
else if(opstring[k]==7)
{
//cout<<"\nBOTTOM RIGHT";
bottomrightnew();redcount++;
}
else if(opstring[k]==8)
{
//cout<<"\nBOTTOM LEFT";
bottomleftnew();redcount++;
}
else if(opstring[k]==9)
{
//cout<<"\nFRONT CLOCK";
front_clknew();redcount++;
}
else if(opstring[k]==10)
{
//cout<<"\nFRONT ANTI CLOCK";
front_anticlknew();redcount++;
}
else if(opstring[k]==11)
{
//cout<<"\nREAR CLOCK";
rear_clknew();redcount++;
}
else if(opstring[k]==12)
{
//cout<<"\nREAR ANTI CLOCK";
rear_anticlknew();redcount++;
}
else
continue;
}
}

void rubik::toprightnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[0][i];
front[0][i]=left[0][i];
left[0][i]=rear[0][i];
rear[0][i]=right[0][i];
right[0][i]=temp;
}
face_change_anti(top);
//face_change(top);
outtextxy(500,10,"top right");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::topleftnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=left[0][i];
left[0][i]=front[0][i];
front[0][i]=right[0][i];
right[0][i]=rear[0][i];
rear[0][i]=temp;
}
//face_change_anti(top);
face_change(top);
outtextxy(500,10,"top left");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::bottomleftnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=left[2][i];
left[2][i]=front[2][i];
front[2][i]=right[2][i];
right[2][i]=rear[2][i];
rear[2][i]=temp;
}
face_change_anti(bottom);
//face_change(top);
outtextxy(500,10,"bottom left");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::bottomrightnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[2][i];
front[2][i]=left[2][i];
left[2][i]=rear[2][i];
rear[2][i]=right[2][i];
right[2][i]=temp;
}
//face_change_anti(top);
face_change(bottom);
outtextxy(500,10,"bottom right");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::rightupnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][2];
front[i][2]=bottom[i][2];
bottom[i][2]=rear[2-i][0];
rear[2-i][0]=top[i][2];
top[i][2]=temp;
}
//face_change_anti(top);
face_change(right);
outtextxy(500,10,"right up");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::rightdownnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][2];
front[i][2]=top[i][2];
top[i][2]=rear[2-i][0];
rear[2-i][0]=bottom[i][2];
bottom[i][2]=temp;
}
face_change_anti(right);
//face_change(right);
outtextxy(500,10,"right down");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::leftupnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][0];
front[i][0]=bottom[i][0];
bottom[i][0]=rear[2-i][2];
rear[2-i][2]=top[i][0];
top[i][0]=temp;
}
face_change_anti(left);
//face_change(right);
outtextxy(500,10,"left up");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::leftdownnew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=front[i][0];
front[i][0]=top[i][0];
top[i][0]=rear[2-i][2];
rear[2-i][2]=bottom[i][0];
bottom[i][0]=temp;
}
//face_change_anti(top);
face_change(left);
outtextxy(500,10,"left down");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}



void rubik::rear_clknew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[0][i];
top[0][i]=left[2-i][0];
left[2-i][0]=bottom[2][2-i];
bottom[2][2-i]=right[i][2];
right[i][2]=temp;
}
face_change_anti(rear);
//face_change(left);
outtextxy(500,10,"rear clk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::rear_anticlknew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[0][i];
top[0][i]=right[i][2];
right[i][2]=bottom[2][2-i];
bottom[2][2-i]=left[2-i][0];
left[2-i][0]=temp;
}
//face_change_anti(rear);
face_change(rear);
outtextxy(500,10,"rear anticlk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::front_clknew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[2][i];
top[2][i]=left[2-i][2];
left[2-i][2]=bottom[0][2-i];
bottom[0][2-i]=right[i][0];
right[i][0]=temp;
}
//face_change_anti(rear);
face_change(front);
outtextxy(500,10,"front clk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}

void rubik::front_anticlknew()
{
int temp;
for(int i=0;i<3;i++)
{
temp=top[2][i];
top[2][i]=right[i][0];
right[i][0]=bottom[0][2-i];
bottom[0][2-i]=left[2-i][2];
left[2-i][2]=temp;
}
face_change_anti(front);
//face_change(left);
outtextxy(500,10,"front anticlk");
draw();
if(scr==0)
getch();
setfillstyle(0,1);
bar(490,0,630,20);
}



void rubik::copyopstrong()
{
int l=0;
for(int k=0;k<500;k++)
{
if(opstring[k]==0)
continue;
else
{
demoopstring[l]=opstring[k];
l++;
//cout<<demoopstring[l];
}
}
for(k=0;k<500;k++)
{
opstring[k]=0;
}
for(k=0;k<500;k++)
{
if(demoopstring[k]==0)
continue;
else
opstring[k]=demoopstring[k];
}
for(k=0;k<500;k++)
{
demoopstring[k]=0;
}
}





void main()
{
clrscr();
for(int k=0;k<500;k++)
{
opstring[k]=0;demoopstring[k]=0;
}
rubik r1;
rubik r2;
setboard();
r1.draw();
getch();

/*
r1.rightup();
r1.topleft();
r1.bottomright();
r1.front_anticlk();
r1.rear_clk();
r1.topleft();
r1.bottomright();
r1.bottomright();
r1.rear_anticlk();
r1.rightdown();
r1.leftdown();
r1.topright();
//r1.display();
getch();


r2=r1;*/








/*r1.front_anticlk();
r1.rear_clk();
r1.bottomright();
r1.leftdown();
/*r1.leftup();
//r1.bottomleft();
//r1.front_clk();
//r1.rear_anticlk();*/
cout<<"\n";
//r1.front_anticlk();
//r1.bottomright();
//r1.rear_clk();
//r1.display();
//getch();
//setboard();
//getch();
r1.scrumble();
r2=r1;
getch();

/*char *str;
outtextxy(500,400,itoa(r1.search(white,white),str,10));
getch();
outtextxy(500,300,itoa(r1.search(green,orange),str,10));
getch();*/
r1.solve(r1.search(white,green));
//getch();
r1.solve(r1.search(white,red));
//getch();
r1.solve(r1.search(white,orange));
//getch();
r1.solve(r1.search(white,blue));
//getch();
r1.solve(r1.search(white,green,red));
//getch();
r1.solve(r1.search(white,green,orange));
//getch();
r1.solve(r1.search(white,blue,red));
//getch();
r1.solve(r1.search(white,blue,orange));
//getch();
r1.solve(r1.search(green,red));
//getch();
r1.solve(r1.search(green,orange));
//getch();
r1.solve(r1.search(red,blue));
//getch();
r1.solve(r1.search(orange,blue));
//getch();
//gotoxy(25,25);
r1.LastLayerCross();
//getch();
//gotoxy(25,25);
r1.LastLayerCrossCorrespondingSideEdges();
//getch();
r1.LastLayerCornerEdgesSettling();
//getch();
r1.LastLayerCornerEdgesFliping();
//getch();
r1.SettlingOfBottomLayer();
//getch();
//cout<<"\nPORG iS HERE BEFORE STRING mALUPALTION";
//getch();

//getch();
//cout<<"STRING MANU DONE";
//getch();

//clrscr();
//cout<<redcount;
redchknum=0;
int hi=0;
for(int h=0;h<500;h++)
{hi++;
if(redchknum==1)
break;
else
{
r1.outputstringredudandancycheak();
r1.copyopstrong();
r1.outputstringredudandancycheak();
}
}
setboard();
r2.draw();
r2.display();
r2.displayoutput();
getch();

//cout<<"O/P DISPALYED";
getch();
gotoxy(25,25);
cout<<"                                                                                   ";
//getch();
gotoxy(25,25);
cout<<"UR CUBE IS COMPLTETEY SOLVED !!!\n THANK YOU \n MOSES DAVID GANGIPOGU";
cout<<"\nstepcount="<<redcount<<"\nHI="<<hi;
/*char *str;
outtextxy(500,400,ltoa(r1.search(white,green,orange),str,10));
outtextxy(500,350,ltoa(r1.search(white,green,red),str,10));
outtextxy(500,300,ltoa(r1.search(white,blue,red),str,10));
outtextxy(500,250,ltoa(r1.search(white,blue,orange),str,10));
getch();
closegraph();
r1.search(yellow,blue,orange);
r1.search(yellow,blue,red);
r1.search(yellow,green,orange);
r1.search(yellow,green,red);*/
getch();
}





















































