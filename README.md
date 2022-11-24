# OpenGL2DProject
#include <GL/gl.h>
#include <GL/glu.h>
#include <GL/glut.h>
#include <stdlib.h>
#include <windows.h>
#include <math.h>
void display();
void reshape(int w,int h);
void timer(int);
void init()
{
glClearColor(0,0,0,0);
}
int main(int argc,char**argv)
{
glutInit(&argc,argv);
glutInitDisplayMode(GLUT_RGB | GLUT_DOUBLE );
glutInitWindowPosition(200,0);
glutInitWindowSize(1200,800);
glutCreateWindow("19200586 , 19103385 ,19100568");
glutDisplayFunc(display);
glutReshapeFunc(reshape);
glutTimerFunc(0,timer,0);
init();
glutMainLoop();
}
float x = -10.0; //animation
float ang = 0.0; // angle rotation

void display()
{
glPushMatrix();
int i;
double angle;
glClear(GL_COLOR_BUFFER_BIT);
glLoadIdentity();
glLineWidth(5.0);
glBegin(GL_LINES); //2d road
glColor3f(0.9,1,0.4);
glVertex2f(-1,-1);
glVertex2f(-7,-1);
glVertex2f(1,-1);
glVertex2f(7,-1);
glVertex2f(-3,-5);
glVertex2f(3,-5);
glVertex2f(-7,-8);
glVertex2f(-1,-8);
glVertex2f(1,-8);
glVertex2f(7,-8);

glEnd();
glPopMatrix();
glPushMatrix();
glTranslatef(10+x,10,0);
glBegin(GL_POLYGON);
glColor3f(1,1,0.9);
for(i = 0; i <= 360; i++) //moon
{
angle = i * 3.14 / 180;
glVertex2f(2 * cos(angle), 2 * sin(angle));
}
glEnd();
glPopMatrix();
glPushMatrix();
glRecti(11,0,-11,2); // Sidewalk
glRecti(11,-11,-11,-9);
glPopMatrix();
glPushMatrix(); //tree branch
glColor3f(0.7,0.5,0);
glRecti(-6,2,-8,8);
glRecti(1,2,-1,8);

glPopMatrix();
glPushMatrix(); //tree 1
glTranslatef(-7,9,0);

glBegin(GL_POLYGON);
glColor3f(0.1,1,0);
for(i = 0; i <= 360; i++)
{
angle = i * 3.14 / 180;
glVertex2f(3* cos(angle), 3* sin(angle));
}
glEnd();
glPopMatrix();
glPushMatrix(); //tree 2
glTranslatef(0,9,0);
glBegin(GL_POLYGON);
glColor3f(0.1,1,0);
for(i = 0; i <= 360; i++)
{
angle = i * 3.14 / 180;
glVertex2f(3* cos(angle), 3* sin(angle));
}

glEnd();
glPopMatrix();
glPushMatrix(); // rec. of car
glColor3f(0,0.2,1);
glRecti( -4 +x, -5,-10+x,-2);
glPopMatrix();
glPushMatrix(); // line loop of car
glColor3f(1,0,0.9);
glRecti(-4 +x,-3,-10+x,-2);
glPopMatrix();
glPushMatrix(); // glass of car
glColor3f(1,1,0.9);
glRecti(-9 +x,-3,-10+x,-2);
glRecti(-6 +x,-3,-7+x,-2);
glRecti(-4 +x,-3,-5+x,-2);

glPopMatrix();
glPushMatrix(); //first tier
glTranslatef(-9 +x,-5,0);
glBegin(GL_POLYGON);
glColor3f(1,1,0.9);
for(i = 0; i <= 360; i++)
{
angle = i * 3.14 / 180;
glVertex2f(1 * cos(angle),1 * sin(angle));
}

glEnd();
glPopMatrix();
glPushMatrix(); //second tier
glTranslatef(-5 +x,-5,0);

glBegin(GL_POLYGON);
glColor3f(1,1,0.9);
for(i = 0; i <= 360; i++)
{
angle = i * 3.14 / 180;
glVertex2f(1 * cos(angle),1 * sin(angle));
}

glEnd();
glPopMatrix();
glPushMatrix();//stars
glRotatef(ang,1,1,1);

glBegin(GL_TRIANGLES);
glColor3f(0.8,1,1);
glVertex2f(5,10);
glVertex2f(4,9);
glVertex2f(6 ,9);
glEnd();
glPopMatrix();
glPushMatrix(); //half road color red
glColor3f(1,0,0);
glRecti(-5,0,-8,2);//up
glRecti(1,0,-2,2);
glRecti(7,0,4,2);
glRecti(-5,-11,-8,-9);//down
glRecti(1,-11,-2,-9);
glRecti(7,-11,4,-9);
glPopMatrix();
glutSwapBuffers();
}

void reshape(int w,int h)
{
glViewport(0,0,(GLsizei)w,(GLsizei)h);
glMatrixMode(GL_PROJECTION);
glLoadIdentity();
gluOrtho2D(-11,11,-11,11);
glMatrixMode(GL_MODELVIEW);
}
void timer(int)
{
glutPostRedisplay();
glutTimerFunc(1000/60,timer,0);
x += 0.2;
ang +=0.8*4;
if(ang > 360)
ang=ang-360;
}
