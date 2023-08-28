#include <GL/glut.h>
#include <cstdlib>
#include<math.h>
#include <iostream>
#include<string>
#include<string.h>
#include<stdlib.h>
using namespace std;
float translate_x = 0.0;
float translate_y = 0.0;
float translate_z = 0.0;
float translate_x1 = 1.0;
float translate_y1 = 1.0;
float translate_z1 = 1.0;
float a = 0.0;
float b = 0.0;
float c = 0.0;
float d = 0.0;
float bubbleSpeed = 0.0001;
float rockSpeed = 0.0001;
float fishSpeed = 0.0001;
GLfloat angle = 45.0;
int refreshmill = 1;
int scoree = 0;


void RenderString(float x, float y, void* font)
{
	char gameover[10] = { 'G','A','M','E',' ','O','V','E','R','!' };
	int xa = x;
	glColor3f(0, 0, 0);
	glRasterPos2f(xa, y);
	for (int i = 0; i < 10; i++) {
		glutBitmapCharacter(font, gameover[i]);
		xa += 0.1;
	}
}

void score(int Score) {
	glColor3f(1.0, 0.0, 0.0);

	glRasterPos2f(-1, 0.9); //define position on the screen
	char int_str[20];
	sprintf_s(int_str, "%d", Score);
	char str[20] = "Your Score : ";
	strcat_s(str, int_str);
	char* string = (str);

	while (*string) {
		glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_24, *string++);
	}
}
//void RenderString(float x, float y, void* font)
//{
//	char c = static_cast<char>(score);
//	glColor3f(1, 0, 0);
//	glRasterPos2f(x, y);
//	glutBitmapCharacter(font, score);
//}

void timer(int value) {
	glutPostRedisplay();
	glutTimerFunc(refreshmill, timer, 0);
}

//----------------------------------------------------------------------------------
float RandomNumber(float x, float y) {
	return((float)rand() / RAND_MAX * (y - x) + x);
}
//----------------------------------------------------------------------------------kayboard


void keyboard(unsigned char key, int x, int y)
{
	if (key == 'd')
	{
		translate_x += 0.1;
		glutPostRedisplay();
	}
	else if (key == 'a')
	{
		translate_x -= 0.1;
		glutPostRedisplay();
	}
	else if (key == 'w')
	{
		translate_y += 0.1;
		glutPostRedisplay();
	}
	else if (key == 's')
	{
		translate_y -= 0.1;
		glutPostRedisplay();
	}
	else if (key == '+')
	{
		translate_x1 += 0.1;
		translate_y1 += 0.1;
		translate_z1 += 0.1;
		glutPostRedisplay();
	}
	else if (key == '-')
	{
		translate_x1 -= 0.1;
		translate_y1 -= 0.1;
		translate_z1 -= 0.1;
		glutPostRedisplay();
	}
	else if (key == '4')
	{
		translate_x1 = -translate_x1;
		translate_y1 = translate_y1;
		translate_z1 = translate_z1;
		glutPostRedisplay();
	}
	else if (key == '2')
	{
		//a = 45;
		//b = 1;
		glutPostRedisplay();
	}
	//-------- reset -------
	else if (key == 'r')
	{
		translate_x = 0.0;
		translate_y = 0.0;
		translate_z = 0.0;
		translate_x1 = 1.0;
		translate_y1 = 1.0;
		translate_z1 = 1.0;
		glutPostRedisplay();
	}

}
//----------------------------------------------------------------------------------star
void star(float x, float y) {

	glMatrixMode(GL_MODELVIEW);
	glPushMatrix();
	glLoadIdentity();

	glTranslatef(x, y, 0);
	glPushMatrix();
	glTranslatef(0.5, 0, 0);
	glRotatef(angle, 0, 0, 1);
	glBegin(GL_TRIANGLES);
	glColor3f(1, 1, 1);
	glVertex3f(0.0, 0.6 / 3, 0);
	glVertex3f(-0.3 / 3, 0.0, 0);
	glVertex3f(0.3 / 3, 0.0, 0);
	glEnd();
	glBegin(GL_TRIANGLES);
	glColor3f(1, 1, 1);
	glVertex3f(0.0, -0.2 / 3, 0);
	glVertex3f(-0.3 / 3, 0.4 / 3, 0);
	glVertex3f(0.3 / 3, 0.4 / 3, 0);

	glEnd();

	glPopMatrix();
	glPopMatrix();
	////glutSwapBuffers();
	angle += 0.1;
	glFlush();
}

//---------------------------------------------------------------------------------fish
typedef struct fish {
	float x = RandomNumber(-1, 1);
	float y = RandomNumber(-1, 1);
	float z = RandomNumber(-1, 1);

}fish;

fish ff[10];
void fish1(float translate_x2, float translate_y2, float translate_z2)
{
	glPushMatrix();
	glLoadIdentity();
	glScalef(-1, 1, 1);
	glTranslatef(translate_x2, translate_y2, translate_z2);
	glColor3f(1.0, 0.0, 0.6);
	glBegin(GL_POLYGON);
	glVertex2f(0.7, 0.25);
	glVertex2f(0.75, 0.3);
	glVertex2f(0.775, 0.3);
	glVertex2f(0.85, 0.25);
	glVertex2f(0.775, 0.2);
	glVertex2f(0.75, 0.2);
	glEnd();

	glBegin(GL_TRIANGLES);
	glVertex2f(0.83, 0.25);
	glVertex2f(0.9, 0.29);
	glVertex2f(0.9, 0.21);
	glEnd();

	glBegin(GL_TRIANGLES);
	glVertex2f(0.775, 0.3);
	glVertex2f(0.79, 0.4);
	glVertex2f(0.75, 0.3);
	glEnd();

	glBegin(GL_TRIANGLES);
	glVertex2f(0.775, 0.2);
	glVertex2f(0.79, 0.1);
	glVertex2f(0.75, 0.2);
	glEnd();

	glColor3f(1.0, 1.0, 1.0);
	glPointSize(8.0);
	glBegin(GL_POINTS);
	glVertex2f(0.73, 0.265);
	glEnd();
	glPopMatrix();


}

void d_fish() {
	for (int i = 0; i < 10; i++) {
		fish1(ff[i].x, ff[i].y, ff[i].z);
	}
	for (int i = 0; i < 10; i++) {
		ff[i].x -= fishSpeed;
		if (ff[i].x < -2.5) {
			ff[i].x = 1;
		}
		//if (ff[i].y >= 0.2 + translate_y && ff[i].x * -1 >= 0.43 + translate_x) {
		//	scoree++;
		//	ff[i].x = -1;
		//}
		if ((ff[i].x + 0.7) * -1 >= (translate_x + 0.4) * translate_x1 && (ff[i].x + 0.7) * -1 <= (translate_x + 0.69) * translate_x1 && (ff[i].y + 0.25) <= (translate_y + 0.3) * translate_y1 && (ff[i].y + 0.25) >= (translate_y + 0.05) * translate_y1)
		{
			cout << "bonus" << endl;
			ff[i].y = RandomNumber(-1, 1);
			ff[i].x = 1.5;
			scoree++;
		}
	}
	glEnd();

	glFlush();
	glutPostRedisplay();
}
//----------------------------------------------------------------rock
typedef struct rock {
	float x[15];
	float y[15];
}rock;

rock m;


void circleFilled(float r, float posx, float posy, float a, float b, float c) {
	glColor3f(1, 1, 1);
	glBegin(GL_POLYGON);
	for (float theta = 0; theta < 360; theta++) {
		float deginrad = theta * 3.14 / 180;
		glVertex2f(posx + r * cos(deginrad), posy + r * sin(deginrad));
	}
	glEnd();

}
void rockk()
{

	for (int i = 0; i < 15; i++)
	{

		glColor3f(0, 0, 0);
		glBegin(GL_POLYGON);
		glVertex2f(-0.53966 + m.x[i], 0.80084 + m.y[i]);
		glVertex2f(-0.45633 + m.x[i], 0.80084 + m.y[i]);
		glVertex2f(-0.40002 + m.x[i], 0.75129 + m.y[i]);
		glVertex2f(-0.40002 + m.x[i], 0.6567 + m.y[i]);
		glVertex2f(-0.45633 + m.x[i], 0.6004 + m.y[i]);
		glVertex2f(-0.53966 + m.x[i], 0.6004 + m.y[i]);
		glVertex2f(-0.59822 + m.x[i], 0.6567 + m.y[i]);
		glVertex2f(-0.59822 + m.x[i], 0.75129 + m.y[i]);
		glEnd();

		circleFilled(0.0361, -0.54006 + m.x[i], 0.73504 + m.y[i], 245.0f / 255.0f, 222.0f / 255.0f, 179.0f / 255.0f);
		circleFilled(0.0180, -0.54006 + m.x[i], 0.73504 + m.y[i], 139.0f / 255.0f, 69.0f / 255.0f, 19.0f / 255.0f);
		circleFilled(0.0230, -0.45106 + m.x[i], 0.74226 + m.y[i], 139.0f / 255.0f, 69.0f / 255.0f, 19.0f / 255.0f);
		circleFilled(0.0200, -0.4655 + m.x[i], 0.66449 + m.y[i], 139.0f / 255.0f, 69.0f / 255.0f, 19.0f / 255.0f);
		circleFilled(0.0140, -0.53926 + m.x[i], 0.66288 + m.y[i], 139.0f / 255.0f, 69.0f / 255.0f, 19.0f / 255.0f);

		//if (m.y[i] + 0.6004 <= 0.2 + translate_y && m.x[i] - 0.45633 >= 0.43 + translate_x && m.x[i] - 0.53966 <= 0.43 + translate_x) {
		//	cout << "Game over" << endl;
		//	bubbleSpeed = 0;
		//	rockSpeed = 0;
		//	fishSpeed = 0;
		//	angle = 0;
		//}

		if (m.x[i] - 0.40002 <= (translate_x + 0.69) * translate_x1 && m.x[i] - 0.40002 >= (translate_x + 0.4) * translate_x1 && 0.80084 + m.y[i] <= (translate_y + 0.3) * translate_y1 && 0.80084 + m.y[i] >= (translate_y + 0.05) * translate_y1)
		{
			RenderString(-0.4f, 0.0f, GLUT_BITMAP_TIMES_ROMAN_24);
			bubbleSpeed = 0;
			rockSpeed = 0;
			fishSpeed = 0;
			angle = 0;
		}
		else if (m.x[i] - 0.40002 <= (translate_x + 0.69) * translate_x1 && m.x[i] - 0.40002 >= (translate_x + 0.4) * translate_x1 && 0.6004 + m.y[i] <= (translate_y + 0.3) * translate_y1 && 0.6004 + m.y[i] >= (translate_y + 0.05) * translate_y1)
		{
			RenderString(-0.4f, 0.0f, GLUT_BITMAP_TIMES_ROMAN_24);
			bubbleSpeed = 0;
			rockSpeed = 0;
			fishSpeed = 0;
			angle = 0;
		}

	}
	for (int i = 0; i < 15; i++) {
		m.y[i] -= rockSpeed;
		if (m.y[i] < -1.8) {
			m.y[i] = 0.5;
		}
	}
}
//---------------------------------------------------------------------------sea
typedef struct seaa {
	float x = RandomNumber(-1, 1);
	float y = RandomNumber(-1, 1);
	float r = 0.009;

}seaa;
seaa s[10];

void drawcircle(float r, float posx, float posy) {
	//float r = 0.01;
	glColor3f(1, 1, 1);
	glBegin(GL_LINE_LOOP); //scalar
	for (float theta = 0; theta < 360; theta++) {
		float deginrad = theta * 3.14 / 180;
		glVertex2f(posx + r * cos(deginrad), posy + r * sin(deginrad));
	}
	glEnd();

}

void d_sea() {
	//	glClearColor(0.0f, 0.0f, 0.0f, 0.0f);
		//glClear(GL_COLOR_BUFFER_BIT);
		//glVertex2f(posx, 0.0f);
	for (int i = 0; i < 10; i++) {
		drawcircle(s[i].r + 0.04, s[i].x, s[i].y);
	}
	for (int i = 0; i < 10; i++) {
		s[i].y += bubbleSpeed;
		if (s[i].y > 1.2) {
			s[i].y = -1;
		}
	}
	glEnd();
	glFlush();
	glutPostRedisplay();
}

//----------------------------------------------------------------------------------shark
void shark() {
	//glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	float x = 0, y = 0;
	glMatrixMode(GL_MODELVIEW);
	//glClear(GL_COLOR_BUFFER_BIT);
	//glClearColor(0.0f, 0.5f, 1.0f, 0);
	glPushMatrix();
	glLoadIdentity();   //عشان الحاجه ترحع لأصلها
	//	glTranslatef(0.5, 0.5, 0);  //martix 
	glTranslatef(translate_x, translate_y, translate_z);
	glScalef(translate_x1, translate_y1, translate_z1);
	glRotatef(a, b, c, d);
	glEnable(GL_POLYGON_SMOOTH);
	//1
	glColor3f(0.4, 0.4, 0.4);
	glBegin(GL_POLYGON);
	glVertex2f(0.45, 0.0);
	glVertex2f(0.4, 0.3);
	glVertex2f(0.6, 0.3);
	glVertex2f(0.6, 0.0);
	glEnd();
	//2.1
	glBegin(GL_POLYGON);
	glVertex2f(0.6, 0.0);
	glVertex2f(0.6, 0.3);
	glVertex2f(0.66, 0.15);
	glEnd();
	//2.2
	glBegin(GL_POLYGON);
	glVertex2f(0.66, 0.15);
	glVertex2f(0.69, 0.245);
	glVertex2f(0.69, 0.046);
	glEnd();
	//3.1
	glBegin(GL_POLYGON);
	glVertex2f(0.53, 0.3);
	glVertex2f(0.57, 0.36);
	glVertex2f(0.57, 0.3);
	glEnd();
	//3.2
	glBegin(GL_POLYGON);
	glVertex2f(0.56, -0.04);
	glVertex2f(0.54, 0.0);
	glVertex2f(0.56, 0.0);
	glEnd();
	//m
	glColor3f(0.0, 0.0, 0.0);
	glBegin(GL_LINE_STRIP);
	glVertex2f(0.442, 0.05);
	glVertex2f(0.54, 0.05);
	glVertex2f(0.54, 0.05);
	glVertex2f(0.57, 0.1);
	glEnd();
	//4
	glBegin(GL_LINES);
	glVertex2f(0.41, 0.28);
	glVertex2f(0.415, 0.26);
	glEnd();
	//5
	glBegin(GL_LINES);
	glVertex2f(0.54, 0.24);
	glVertex2f(0.56, 0.28);
	glBegin(GL_LINES);
	glVertex2f(0.55, 0.24);
	glVertex2f(0.57, 0.28);
	glBegin(GL_LINES);
	glVertex2f(0.56, 0.24);
	glVertex2f(0.58, 0.28);
	glEnd();
	//eye
	float r = 0.015;
	glColor3f(0.0, 0.0, 0.0);
	glBegin(GL_POLYGON); //scalar
	for (float theta = 0; theta < 360; theta++) {
		float deginrad = theta * 3.14 / 180;
		glVertex2f(0.48 + r * cos(deginrad), 0.26 + r * sin(deginrad));

	}
	glEnd();
	//te20 x1=+0.5 x2=x1 prev x3=x2 curr
	float x1 = 0.446, x2 = 0.442, x3 = 0.446;
	for (int i = 0; i < 20; i++) {

		glBegin(GL_POLYGON);
		glVertex2f(x1, 0.04);
		glVertex2f(x2, 0.05);
		glVertex2f(x3, 0.05);
		glEnd();
		x2 = x1;
		x1 += 0.005;
		x3 = x1;

	}

	glPopMatrix();
	glFlush();
	glutPostRedisplay();
}

//----------------------------------------------------------------------------------display
void display() {
	glClear(GL_COLOR_BUFFER_BIT);
	glClearColor(0.0f, 0.5f, 1.0f, 0);
	d_sea();
	d_fish();
	star(-1.5, -0.8);
	star(0, -0.9);
	rockk();
	shark();
	score(scoree);
	//RenderString(0, 0, GLUT_BITMAP_TIMES_ROMAN_24);
	glutSwapBuffers();
	glFlush();
	glutPostRedisplay();
}
//----------------------------------------------------------------------------------main
void reshape(GLsizei width, GLsizei height) {  // GLsizei for non-negative integer
	// Compute aspect ratio of the new window
	if (height == 0) height = 1;                // To prevent divide by 0
	GLfloat aspect = (GLfloat)width / (GLfloat)height;

	// Set the viewport to cover the new window
	glViewport(0, 0, width, height);

	// Set the aspect ratio of the clipping area to match the viewport
	glMatrixMode(GL_PROJECTION);  // To operate on the Projection matrix
	glLoadIdentity();             // Reset the projection matrix
	if (width >= height) {
		// aspect >= 1, set the height from -1 to 1, with larger width
		gluOrtho2D(-1.0 * aspect, 1.0 * aspect, -1.0, 1.0);
	}
	else {
		// aspect < 1, set the width to -1 to 1, with larger height
		gluOrtho2D(-1.0, 1.0, -1.0 / aspect, 1.0 / aspect);
	}
}
int main(int argc, char** argv) {
	for (int i = 0; i < 4; i++) {
		m.x[i] = RandomNumber(-1, 1);
		m.y[i] = RandomNumber(-1, 1);
	}
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_RGB | GLUT_DOUBLE);
	glutInitWindowSize(640, 480);
	glutInitWindowPosition(0, 0);
	glutCreateWindow("OpenGL sea");
	glutDisplayFunc(display);
	glutKeyboardFunc(keyboard);
	glutReshapeFunc(reshape);
	glutTimerFunc(0, timer, 0);
	//glutIdleFunc(display);
	glutMainLoop();
	return 0;
}
