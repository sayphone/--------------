--------------
==============

OpenGL

#include<glut.h>
#include <stdio.h>
#define ESCAPE 27
GLint window;
 GLfloat xRotated, yRotated, zRotated;
 GLfloat xt=1.0,yt=1.0;
void init(void)
{
glClearColor(0,0,0,0);

  }
void keyboardAssign (GLubyte key, GLint x, GLint y)
{
  switch ( key )
	{
	case ESCAPE :
		printf(" escape press. exit. \n");
		glutDestroyWindow(window);
		
		break;
	case 'd':
			xt += 2.0;
			glutPostRedisplay();
			break;

	case 'a':
			xt -= 2.0;
			glutPostRedisplay();
			break;

	case 'w':
			yt += 2.0;
			glutPostRedisplay();
			break;

	case 's':
			yt -= 2.0;
			glutPostRedisplay();
			break;

	case 'e':
			xt += 2.0;
			yt += 2.0;
			glutPostRedisplay();
			break;

	case 'q':
			xt -= 3.0;
			yt += 3.0;
			glutPostRedisplay();
			break;
	case 'c':
			xt += 2.0;
			yt -= 2.0;
			glutPostRedisplay();
			break;

	case 'z':
			xt -= 2.0;
			yt -= 2.0;
			glutPostRedisplay();
			break;
	default:
				break;
	}
}

void DrawCube(void)
{

     glMatrixMode(GL_MODELVIEW);     // clear the drawing buffer.
    glClear(GL_COLOR_BUFFER_BIT);
   glLoadIdentity();
    glTranslatef(xt,yt,-10.5);
    glRotatef(xRotated,1.0,0.0,0.0);   // rotation about Y axis
    glRotatef(yRotated,0.0,1.0,0.0);   // rotation about Z axis
    glRotatef(zRotated,0.0,0.0,1.0);
  glBegin(GL_QUADS);        // Draw The Cube Using quads
    glColor3f(0.0f,1.0f,0.0f);    // Color Blue
    glVertex3f( 1.0f, 1.0f,-1.0f);    // Top Right Of The Quad (Top)
    glVertex3f(-1.0f, 1.0f,-1.0f);    // Top Left Of The Quad (Top)
    glVertex3f(-1.0f, 1.0f, 1.0f);    // Bottom Left Of The Quad (Top)
    glVertex3f( 1.0f, 1.0f, 1.0f);    // Bottom Right Of The Quad (Top)
    glColor3f(1.0f,0.5f,0.0f);    // Color Orange
    glVertex3f( 1.0f,-1.0f, 1.0f);    // Top Right Of The Quad (Bottom)
    glVertex3f(-1.0f,-1.0f, 1.0f);    // Top Left Of The Quad (Bottom)
    glVertex3f(-1.0f,-1.0f,-1.0f);    // Bottom Left Of The Quad (Bottom)
    glVertex3f( 1.0f,-1.0f,-1.0f);    // Bottom Right Of The Quad (Bottom)
    glColor3f(1.0f,0.0f,0.0f);    // Color Red    
    glVertex3f( 1.0f, 1.0f, 1.0f);    // Top Right Of The Quad (Front)
    glVertex3f(-1.0f, 1.0f, 1.0f);    // Top Left Of The Quad (Front)
    glVertex3f(-1.0f,-1.0f, 1.0f);    // Bottom Left Of The Quad (Front)
    glVertex3f( 1.0f,-1.0f, 1.0f);    // Bottom Right Of The Quad (Front)
    glColor3f(1.0f,1.0f,0.0f);    // Color Yellow
    glVertex3f( 1.0f,-1.0f,-1.0f);    // Top Right Of The Quad (Back)
    glVertex3f(-1.0f,-1.0f,-1.0f);    // Top Left Of The Quad (Back)
    glVertex3f(-1.0f, 1.0f,-1.0f);    // Bottom Left Of The Quad (Back)
    glVertex3f( 1.0f, 1.0f,-1.0f);    // Bottom Right Of The Quad (Back)
    glColor3f(0.0f,0.0f,1.0f);    // Color Blue
    glVertex3f(-1.0f, 1.0f, 1.0f);    // Top Right Of The Quad (Left)
    glVertex3f(-1.0f, 1.0f,-1.0f);    // Top Left Of The Quad (Left)
    glVertex3f(-1.0f,-1.0f,-1.0f);    // Bottom Left Of The Quad (Left)
    glVertex3f(-1.0f,-1.0f, 1.0f);    // Bottom Right Of The Quad (Left)
    glColor3f(1.0f,0.0f,1.0f);    // Color Violet
    glVertex3f( 1.0f, 1.0f,-1.0f);    // Top Right Of The Quad (Right)
    glVertex3f( 1.0f, 1.0f, 1.0f);    // Top Left Of The Quad (Right)
    glVertex3f( 1.0f,-1.0f, 1.0f);    // Bottom Left Of The Quad (Right)
    glVertex3f( 1.0f,-1.0f,-1.0f);    // Bottom Right Of The Quad (Right)
	
  glEnd();            // End Drawing The Cube
glFlush();
}


void animation(void)
{
 
     yRotated += 0.01;
     xRotated += 0.02;
    DrawCube();
}
void reshape(int x, int y)
{
    if (y == 0 || x == 0) return;  //Nothing is visible then, so return
    glMatrixMode(GL_PROJECTION);  
    glLoadIdentity();
    gluPerspective(40.0,(GLdouble)x/(GLdouble)y,0.5,20.0);
    glMatrixMode(GL_MODELVIEW);
    glViewport(0,0,x,y);  //Use the whole window for rendering
}

int main(int argc, char** argv)
{
glutInit(&argc, argv);  //we initizlilze the glut. functions
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);
glutInitWindowPosition(100, 100);
glutInitWindowSize(500,500);
glutCreateWindow(argv[0]);
init();
glutDisplayFunc(DrawCube);
glutReshapeFunc(reshape);  //Set the function for the animation.
glutIdleFunc(animation);
glutKeyboardFunc(keyboardAssign);
glutMainLoop();
return 0;
}
