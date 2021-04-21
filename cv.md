### 1. Name
Kiryl, Kaveryn
### 2. Contact info
Discord: KirylK#6310, email: kirylkaveryn@gmail.com
### 3. Summary
I am 31 years old. My first and main profession at the moment is structural design and analyse of civil buildings and subway structures (in Minsk and Moscow).
I am very interested in the field of software development and mobile development. I have no development experience, but I have a great desire to develop, learn new things, and solve complex problems. When I was taking the course Harvard CS50 I realized, that the approach to solving problems is very similar to design of buildings and for this I have all the necessary qualities: perseverance, the ability to find and analyze information, solve comlex problems in different ways, think structurally in general, communicate with others specialists, make decisions and take responsibility, because the structural analysis of buildings is a work associated with great responsibility (for the lives of people), requires extreme care and minimization of risks.
From the course, I expect, first of all, structured knowledge and support from the community. And in general I want to learn new things!
### 4. Skills
I am newbie in developing :((
### 5. Code examples:
This is little program on C from CS50 that recover a jpeg images from "damaged" file:
```C
#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>


typedef uint8_t BYTE;
typedef uint32_t LONG; // limit of file is 4 294 967 295 BYTEs

const int rgbfour[16] = {0xe0, 0xe1, 0xe2, 0xe3, 0xe4, 0xe5, 0xe6, 0xe7, 0xe8, 0xe9, 0xea, 0xeb, 0xec, 0xed, 0xee, 0xef};

bool signature(LONG n, BYTE *pfirst);
void writeToFile(LONG start, LONG end, int imagenum, BYTE *pbuffer);

int main(int argc, char *argv[])
{
    // Ensure proper usage
    if (argc != 2)
    {
        printf("Usage ./recover image\n");
        return 1;
    }

    FILE *file = fopen(argv[1], "r");

    // Ensure file exists
    if (file == NULL)
    {
        printf("Could not open\n");
        fclose(file);
        return 2;
    }

    // Determine the size of input file
    long fsize = 0;
    BYTE buffer;

    // Read data from recovered file to memory
    while (fread(&buffer, sizeof(BYTE), 1, file))
    {
        fsize++;
    }
    // printf("File size: %li\n", fsize);

    // Alloceate memory for bufferfile (array of bytes)
    BYTE *pbuffer = malloc(fsize);
    if (pbuffer == NULL)
    {
        printf("Not enough memory for recover\n");
        return 3;
    }

    rewind(file); // sets the file position indicator to the beginning of the file

    // Read input file to buffer
    fread(pbuffer, sizeof(BYTE), fsize, file);
    fclose(file);

    LONG start = 0, end = 0;
    int imagecount = 0;

    // finding a header of jpg
    for (LONG i = 0; i < fsize; i++)
    {
        end = i - 1;

        // write previous jpg and mark the start of next jpg
        if (signature(i, &pbuffer[i]) && imagecount > 0)
        {
            writeToFile(start, end, imagecount, &pbuffer[start]);
            imagecount++;
            start = i;
        }

        // write last jpg until the end fo input file
        if (imagecount > 0 && end == fsize - 2)
        {
            writeToFile(start, end + 1, imagecount, &pbuffer[start]);
        }

        // mark a 1st file starting
        if (signature(i, &pbuffer[i]) && imagecount == 0)
        {
            start = i;
            imagecount++;
        }
    }

    free(pbuffer);
}

// Check header of .jpg file
bool signature(LONG n, BYTE *pfirst)
{
    if (*pfirst == 0xff && *(pfirst + 1) == 0xd8 && *(pfirst + 2) == 0xff)
    {
        for (int j = 0; j < 16; j++)
        {
            if (*(pfirst + 3) == rgbfour[j])
            {
                return true;
                break;
            }
        }
    }
    return false;
}


// Create new jpg file and write a data
void writeToFile(LONG start, LONG end, int imagenum, BYTE *pbuffer)
{

    // set name to image
    char *number = malloc(7);
    sprintf(number, "%.3d.jpg", imagenum - 1);

    // Open new file to write an recovered image
    FILE *wrfile = fopen(number, "w");

    fwrite(pbuffer, sizeof(BYTE), end - start + 1, wrfile);

    // Free memory
    fclose(wrfile);
    free(number);
}
```
6. English
Spoken English is rather weak, but I read technical documentation and perceive it by ear is OK.
