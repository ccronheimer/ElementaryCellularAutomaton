Elementary Cellular Automaton

    - I read the files ruleSet.txt and ruleSetWide.txt in that contain the rules.
    - c to change colour.
    - m for mono colour.
    - w for wide.
    - q to quit.

    to build in terminal -> gcc -framework OpenGL -framework GLUT -o oneauto oneauto.c
    to run -> ./oneauto

I am on a Mac so importing glut is different so I hope this works for you.
#ifdef __APPLE_CC__
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#endif

have a nice day! Cheers  

