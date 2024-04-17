# Encryption/Decryption Tool
<br> 

### Overview 
We developed an encryption/decryption tool in C. The tool was capable of encrypting text files with an encryption key defined using a hexadecimal algorithm. The tool would generate a ".crp" file that could then be deciphered using the deryption tool.
<br><br>

### My Role
I led the developement portion of the team. I was responsible for writing all of the code to implement the functionality. I also handled testing for quality assurance. 
<br> <br> 
### Sample Text File &emsp; ---> &emsp; After Encryption 
[Regular Text](https://githerdone17.github.io/kobes-portfolio/Files/Regular_Text.txt) &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;[Encrypted Text](https://githerdone17.github.io/kobes-portfolio/Files/Encrypted_Text.crp)
<br> <br> 
### The Code
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>



FILE *in_file;
FILE *out_file;
char inName[15], outName[15], temp[2], inChar1[121], inChar2[120], outChar1[255], outChar2[255], hexdec[2];


//Function to encrypt messages
    int Encrypt(char *argv[], int x){

//Opens output file, if it can't, error printed

    strcpy(inName, argv[x]);
    in_file = fopen(inName, "r");
    if (in_file == NULL){
        printf("Can't open file");
        exit(1);
    }
    printf("\n%s Is being encrypted", inName);

//For naming output file with same name as input plus '.crp' concatenated

    int i, len;
    len = strlen(inName);
    for ( i = 0; i < len; i++) {
        temp[0] = inName[i];
        if(inName[i] != '.') strcat(outName, temp);
        else break;
    }
    strcat(outName, ".crp");

    out_file = fopen(outName, "w");

//For scanning through the document

    while(!feof(in_file)){

        fgets(inChar1, 120, in_file);

//Reading the document one character at a time

        inChar1[strlen(inChar1)] = '\0';

        for (i = 0; i < strlen(inChar1); i++) {
            if (inChar1[i] == '\n') {
                break;
            }

//Converting tab to 'TT'

            if (inChar1[i] == 9) {
                char tempString[] = "TT";
                fputs(tempString, out_file);
            }
            
//Converting input string to hexadecimal values

            if(inChar1[i] - 16 < 32){
                inChar1[i] -= 16;
                int little = (inChar1[i] - 32) + 144;
                fprintf(out_file, "%02X", little);
            } else {
                fprintf(out_file, "%02X", (inChar1[i] - 16));
            }
        }
        fprintf(out_file, "%c", '\n');

    }

//Indicating the status of the encryption

    if (feof(in_file)) {
        printf("\nFile Scan: 100 percent completed.");
    } else{
        printf("Uh Oh, We've encoutered an unexpected issue!");
        
    }
    return 0;
}

/////////////////////////////////////////////////////////////////////////////////////////////Encryption^

int Decrypt(char *argv[], int x){
   
//Opens output file, if it can't, error printed
    strcpy(inName, argv[x]);
    in_file = fopen(inName, "r");
    if (in_file == NULL){
        printf("Can't open file");
        exit(1);
    }
    printf("\n%s Is being decrypted...", inName);

//Name output file with same name as input plus '.txt' concatenated
    int i, len, mid;
    len = strlen(inName);
    for ( i = 0; i < len; i++) {
        temp[0] = inName[i];
        if(inName[i] != '.') strcat(outName, temp);
        else break;
    }
    strcat(outName, ".txt");
    
    out_file = fopen(outName, "w");

//For scanning through the whole file 

    while(!feof(in_file)){
        
        fgets(outChar1, 255, in_file);
        
        if(strcmp(outChar1, outChar2) == 0 && feof(in_file)) break;
        strcpy(outChar2, outChar1);

//For every char in the line // Works in pairs of 2 digits at a time
        for(i=0; i<255; i=i+2){
            hexdec[0] = outChar1[i];
            hexdec[1] = outChar1[i+1];

            if(hexdec[0] == 0) break;

//To change lines
            if(hexdec[0] == '\n'){
                fputc('\n', out_file);
                break;
            }
            
//Checks if hexdec is "TT", adds a tab to output_file

            else if(hexdec[0] == 'T' && hexdec[1] == 'T') fprintf(out_file, "\t");
            
            
//Converts hexdec to char

            else {
                sscanf(hexdec, "%X", &mid);
                
                mid += 16;
                if(mid > 127) mid = (mid - 144) + 32;
                fprintf(out_file, "%c", mid);
            }
        }
    }
    
    if (feof(in_file)) printf("\nFile Scan: 100 percent completed.");
    else {
        printf("\nUh Oh, We've encoutered an unexpected issue!");
        return(1);
    }

    return(0);
}

///////////////////////////////////////////////////////////////////////////////////////////Decryption^

//Main code for indicating whether the file is to be encrypted or decrypted

int main(int argc, char *argv[]) {

    if (argc < 2){
        printf("Cannot process request");
        exit(1);
    }

//While executing in CMD, use '-E' to encrypt
    if(strcmp(argv[1], "-E") == 0) { 
        printf("Encrypting..."); 
        Encrypt(argv, 2);
    }

//While executing in CMD, use '-D'
  else if(strcmp(argv[1], "-D") == 0) { 
        printf("Decrypting.."); 
        Decrypt(argv, 2);}

//if not specified, encryption is assumed
  else { 
        Encrypt(argv, 2);
          printf("Not specifed, encryption is assumed");}

    fclose(in_file);
    fclose(out_file);
    return(0);
}
```
<br> <br> <br>
[back](https://githerdone17.github.io/kobes-portfolio/)
