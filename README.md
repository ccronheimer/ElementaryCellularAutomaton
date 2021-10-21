### Elementary Cellular Automaton

### Code

```c
#ifdef __APPLE_CC__
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#endif

#include <stdlib.h> // need both for macos
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

// An example of dynamic multi-dimensional arrays in C.
//
// gcc -framework OpenGL -framework GLUT -o oneauto oneauto.c

// wolfram elementary cellular automata
// grid of cells [][][][][][]
// cell state [1][0][1]

int ruleset[8];
int wideRuleSet[32];
float colourSet[8][3];

bool isColoured = false;
bool isWide = false;

int rules(int a, int b, int c)
{

    if (a == 1 && b == 1 && c == 1)
        return ruleset[0];
    else if (a == 1 && b == 1 && c == 0)
        return ruleset[1];
    else if (a == 1 && b == 0 && c == 1)
        return ruleset[2];
    else if (a == 1 && b == 0 && c == 0)
        return ruleset[3];
    else if (a == 0 && b == 1 && c == 1)
        return ruleset[4];
    else if (a == 0 && b == 1 && c == 0)
        return ruleset[5];
    else if (a == 0 && b == 0 && c == 1)
        return ruleset[6];
    else if (a == 0 && b == 0 && c == 0)
        return ruleset[7];
}

int wideRules(int l2, int l1, int c, int r1, int r2)

{
    if (l2 == 0 && l1 == 0 && c == 0 && r1 == 0 && r2 == 0)
    {
        return ruleset[0];
    }
    if (l2 == 0 && l1 == 0 && c == 0 && r1 == 1 && r2 == 0)
    {
        return ruleset[1];
    }
    if (l2 == 0 && l1 == 0 && c == 0 && r1 == 1 && r2 == 1)
    {
        return ruleset[2];
    }
    if (l2 == 0 && l1 == 0 && c == 1 && r1 == 0 && r2 == 0)
    {
        return ruleset[3];
    }
    if (l2 == 0 && l1 == 0 && c == 1 && r1 == 0 && r2 == 1)
    {
        return ruleset[4];
    }
    if (l2 == 0 && l1 == 0 && c == 1 && r1 == 1 && r2 == 0)
    {
        return ruleset[5];
    }
    if (l2 == 0 && l1 == 0 && c == 1 && r1 == 1 && r2 == 1)
    {
        return ruleset[6];
    }
    if (l2 == 0 && l1 == 1 && c == 0 && r1 == 0 && r2 == 0)
    {
        return ruleset[7];
    }
    if (l2 == 0 && l1 == 1 && c == 0 && r1 == 0 && r2 == 1)
    {
        return ruleset[8];
    }
    if (l2 == 0 && l1 == 1 && c == 0 && r1 == 1 && r2 == 0)
    {
        return ruleset[9];
    }
    if (l2 == 0 && l1 == 1 && c == 0 && r1 == 1 && r2 == 1)
    {
        return ruleset[10];
    }
    if (l2 == 0 && l1 == 1 && c == 1 && r1 == 0 && r2 == 0)
    {
        return ruleset[11];
    }
    if (l2 == 0 && l1 == 1 && c == 1 && r1 == 0 && r2 == 1)
    {
        return ruleset[12];
    }
    if (l2 == 0 && l1 == 1 && c == 1 && r1 == 1 && r2 == 0)
    {
        return ruleset[13];
    }
    if (l2 == 0 && l1 == 1 && c == 1 && r1 == 1 && r2 == 1)
    {
        return ruleset[15];
    }
    if (l2 == 1 && l1 == 0 && c == 0 && r1 == 0 && r2 == 0)
    {
        return ruleset[16];
    }
    if (l2 == 1 && l1 == 0 && c == 0 && r1 == 0 && r2 == 1)
    {
        return ruleset[17];
    }
    if (l2 == 1 && l1 == 0 && c == 0 && r1 == 1 && r2 == 0)
    {
        return ruleset[18];
    }
    if (l2 == 1 && l1 == 0 && c == 1 && r1 == 0 && r2 == 0)
    {
        return ruleset[19];
    }
    if (l2 == 1 && l1 == 0 && c == 1 && r1 == 0 && r2 == 1)
    {
        return ruleset[20];
    }
    if (l2 == 1 && l1 == 0 && c == 1 && r1 == 1 && r2 == 0)
    {
        return ruleset[21];
    }
    if (l2 == 1 && l1 == 0 && c == 1 && r1 == 1 && r2 == 1)
    {
        return ruleset[22];
    }
    if (l2 == 1 && l1 == 1 && c == 0 && r1 == 0 && r2 == 0)
    {
        return ruleset[23];
    }
    if (l2 == 1 && l1 == 1 && c == 0 && r1 == 0 && r2 == 1)
    {
        return ruleset[24];
    }
    if (l2 == 1 && l1 == 1 && c == 0 && r1 == 1 && r2 == 0)
    {
        return ruleset[25];
    }
    if (l2 == 1 && l1 == 1 && c == 0 && r1 == 1 && r2 == 1)
    {
        return ruleset[26];
    }
    if (l2 == 1 && l1 == 1 && c == 1 && r1 == 0 && r2 == 0)
    {
        return ruleset[27];
    }
    if (l2 == 1 && l1 == 1 && c == 1 && r1 == 0 && r2 == 1)
    {
        return ruleset[28];
    }
    if (l2 == 1 && l1 == 1 && c == 1 && r1 == 1 && r2 == 0)
    {
        return ruleset[29];
    }
    if (l2 == 1 && l1 == 1 && c == 1 && r1 == 1 && r2 == 1)
    {
        return ruleset[30];
    }
    if (l2 == 0 && l1 == 0 && c == 0 && r1 == 0 && r2 == 1)
    {
        return ruleset[31];
    }
    // 32 combo 5 bit
}

float *colourRule(int a, int b, int c)
{

    if (a == 1 && b == 1 && c == 1)
        return colourSet[0]; // return the 3 colour values from 0
    else if (a == 1 && b == 1 && c == 0)
        return colourSet[1];
    else if (a == 1 && b == 0 && c == 1)
        return colourSet[2];
    else if (a == 1 && b == 0 && c == 0)
        return colourSet[3];
    else if (a == 0 && b == 1 && c == 1)
        return colourSet[4];
    else if (a == 0 && b == 1 && c == 0)
        return colourSet[5];
    else if (a == 0 && b == 0 && c == 1)
        return colourSet[6];
    else if (a == 0 && b == 0 && c == 0)
        return colourSet[7];
}

void draw(void)
{
    glClear(GL_COLOR_BUFFER_BIT);
    const int numCells = 250;
    int cells[numCells];
    int newCells[numCells];
    int xsize = 0, ysize = 0;
    int cellWidth = 2, cellHeight = 2;
    int reach = 0;

    if (!isWide)
    {
        reach = 1;
    }
    else
    {
        reach = 2;
    }

    // 1. random colour table init // if coloured is true
    for (int i = 0; i < 8; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            colourSet[i][j] = ((1.0f - 0.0f) * ((float)rand() / RAND_MAX)) + 0.0f;
        }
    }

    // 2. random binary row init
    for (int i = 0; i < numCells; i++)
    {
        cells[i] = rand() % 2;
        //    printf("%d ", cells[i]);
    }

    // 3. draw the row | analyze neighbour and use colour rule
    for (int y = 0; y < numCells; y++)
    {
        xsize = 0;

        // draw row
        for (int j = reach; j < numCells - reach; j++)
        {
            glBegin(GL_POLYGON);
            // printf("%d ", cells[j]);
            if (isColoured)
            {
                int left = cells[j - 1];
                int middle = cells[j];
                int right = cells[j + 1];

                float *colour = colourRule(left, middle, right); // return the colour

                glColor3f(colour[0], colour[1], colour[2]);
            }
            else
            {
                if (cells[j] == 1)
                {
                    glColor3f(0, 0, 0); // black
                }
                else
                {
                    glColor3f(1.0, 1.0, 1.0); // white
                }
            }

            glVertex2i(cellWidth + xsize, cellHeight + ysize);
            glVertex2i(0.0 + xsize, cellHeight + ysize);
            glVertex2i(0.0 + xsize, 0.0 + ysize);
            glVertex2i(cellWidth + xsize, 0.0 + ysize);

            glEnd();

            xsize += cellWidth; // moves to the next cell in row
        }

        // 4. analyze and switch the binary numbers
        for (int i = reach; i < numCells - reach; i++)
        {

            int left = cells[i - 1];
            int middle = cells[i];
            int right = cells[i + 1];
            int newState = 0;

            if (!isWide)
            {
                newState = rules(left, middle, right);
            }
            else
            {
                int farLeft = cells[i - 2];
                int farRight = cells[i + 2];
                newState = wideRules(farLeft, left, middle, right, farRight);
            }

            newCells[i] = newState;
        }

        // swap arrays
        for (int i = reach; i < numCells - reach; i++)
        {
            cells[i] = newCells[i];
        }

        ysize += cellHeight;
    }

    glFlush();
    glutSwapBuffers();
}

// Keyboard Listener
void foo(unsigned char key, int x, int y)
{
    switch (key)
    {
    case 'c':
    {
        isColoured = true;

        break;
    }
    case 'm':
    {
        isColoured = false;

        break;
    }
    case 'w':
        if (isWide)
        {
            isWide = false;
        }
        else
        {
            isWide = true;
        }

        break;
    case 'q': // exit
    {
        glutDestroyWindow(glutGetWindow());
        exit(0);
        break;
    }
    }
    glutPostRedisplay();
}

main(int argc, char **argv)
{
    // Reader
    FILE *fileStream, *fileStreamWide;
    char fileText[8], fileTextWide[32];
    fileStream = fopen("ruleSet.txt", "r");
    fileStreamWide = fopen("ruleSetWide.txt", "r");
    fgets(fileText, 8, fileStream);
    fgets(fileTextWide, 32, fileStreamWide);
    fclose(fileStream);
    fclose(fileStreamWide);

    // convert char[] to int[]
    for (int c = 0; c < 8; c++)
    {
        if (fileText[c] == '1')
        {
            ruleset[c] = 1;
        }
        else if (fileText[c] == '0')
        {
            ruleset[c] = 0;
        }
    }

    // convert char[] to int[]
    for (int c = 0; c < 32; c++)
    {
        if (fileTextWide[c] == '1')
        {
            wideRuleSet[c] = 1;
        }
        else if (fileTextWide[c] == '0')
        {
            wideRuleSet[c] = 0;
        }
    }

    glutInit(&argc, argv);
    glutInitWindowSize(400, 400);
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutCreateWindow("Elementary Cellular Automata");

    glutDisplayFunc(draw);

    glMatrixMode(GL_PROJECTION);
    gluOrtho2D(0.0, 399.0, 0.0, 399.0);

    glutKeyboardFunc(foo);

    glutMainLoop();
}
```


