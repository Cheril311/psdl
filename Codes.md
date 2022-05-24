1.
include <xc.h>
const int MAX_SIZE=100;
void main(void) {
    int sum=0;
    int arr[100]={0};
    for(int i=0;i<MAX_SIZE;i++){
        arr[i]=2;
    }
    for(int i=0;i<MAX_SIZE;i++){
        sum=sum+arr[i];
    }
    int sum1=sum;
    
    int *p=&sum1;
    return;
}

2.
#include <xc.h>

void main(void) {
    int arr[]={6,5,4,3,2,1};
    int size=sizeof(arr)/sizeof(int);
    
    for(int i=0;i<size;i++){
        for(int j=i+1;j<size;j++){
            if (arr[j]<arr[i]){
                int temp=arr[i];
                arr[i]=arr[j];
                arr[j]=temp;
            }
        }
    }
    int arr1[6];
    for (int k=0;k<size;k++){
        arr1[k]=arr[k];
    }
    return;
}

3.

#include <xc.h>

void main(void) {
    int arr[]={6,5,4,3,2,1};
    int size=sizeof(arr)/sizeof(int);
    
    for(int i=0;i<size-1;i++){
        int min_idx=i;
        for (int j=i+1;j<size;j++){
            if (arr[j]<arr[min_idx]){
                min_idx=j;
            }
        }
        int temp = arr[min_idx];
        arr[min_idx]=arr[i];
        arr[i]=temp;
    }
    int arr1[6];
    for(int i=0;i<size;i++){
        arr1[i]=arr[i];
    }
    return;
}



4.
#include <xc.h>

void main(void) {
    int a,b;
    int *p;
    T0CON=0x01;
    TRISB=0;
    PORTB=0x02;
    TRISC=0;
    TRISD=0;
    
    p=&a;
    
    while(a==0){
        b=(T0CON*PORTB);
        PORTC=b/256;
        PORTD=b%256;
    }
    while(a!=0){
        PORTC=PORTB/T0CON;
        PORTD=PORTB%T0CON;
    }
    
    return;
}


5.
#include <xc.h>


void main(void) {
    int x=25;
    int y=10;
    
    PORTB:
    while(1){
        PORTB=x+y;
        STATUS;
    }
    
    return;
}

12.
#include <xc.h>
#define relay LATAbits.LATA4
int c = 0;
void __interrupt() isr(){
    if(INT1IF){
        INT1IF = 0;
        if(c==0 && relay==0){
            relay = 1;
        }
        else if(relay==1 && c==0){
            c++;
        }
        else if(relay==1 && c==1){
            c = 0;
            relay = 0;
        }
   
    }
}

void main(void) {
    TRISAbits.TRISA4 = 0;
    TRISBbits.RB1 = 1;
    relay = 0;
    INT1IE = 1;
    INTEDG1 = 0;
    GIE = 1;
    INT1IF = 0;
     while(1);
    return;
}

13.
#include <xc.h>
#include<stdio.h>
#include <pic18f4550.h>
#define _XTAL_FREQ 4000000

void putch(unsigned char c){
    while(PIR1bits.TXIF ==0);
    TXREG = c;
}

void init_uart(void){
    TXSTA1bits.TXEN = 1;
    RCSTA1bits.SPEN = 1;
}

void main (void){
    init_uart();
    int a = 0;
    TRISC=0;
    TXSTA=0x20;
    RCSTA=0b10010000;
    SPBRG=6;
    TRISCbits.TRISC7=1;
    while(1){
        printf("\n PICT");
        a = RCREG;
        if(a>=1 && a<=9){
            printf("\nEntered: %d", a);
            break;
        }
    }
    while(1);
    return;
}

14.
#include <xc.h>
#include<stdio.h>
#define _XTAL_FREQ 4000000
 
void putch(unsigned char c){
    while(PIR1bits.TXIF==0);
    TXREG = c;
}
 
 
void main(void) {
    int a = 0;
    TXSTA = 0x20;
    RCSTA = 0b10010000;
    SPBRG = 6;
    TRISCbits.TRISC7 = 1;
    while(PIR1bits.RCIF==0);
    a = RCREG;
    printf("\nValue of Input k %d",a);
    printf("\nValue 2k %d",a*2);
    printf("\nValue 3k %d",a*3);
    printf("\nValue 4k %d",a*4);
    return;
}


TIMER:
#include <xc.h>
#include <pic18f4550.h>
void main(void){
TRISB=0;
PORTB=0;
T0CON=0x08;
TMR0IF=0;
while(1){
   GIE=1;
   TMR0IE=1;
   for(i=0;i<c;i++){
        TMR0=53536;
        TMR0ON=1;
        while(!TMR0IF);
              TMR0ON=0;
              TMR0IF=0;
        
    }
    PORTB=~PORTB;
}
}



BUZZER
#include <xc.h>
#include <pic18f4550.h>
int c=0;
void_interrupt() Timer1_ISR(){
if(TMR1IF==1){
  TMR1IF=0;
  TMR1=53536;
  c++;
  if(c==1000){
     LATAbits.LATA5=~LATAbits.LATA5;
     c=0;
}
}
}
void main(void){
T1CON=0x80;
TMR1=53536;
GIE=1;
PEIE=1;
TMR1IE=1;
TMR1IF=0;
LATAbits.LATA5=0;
TRISAbits.TRISA5=0;
TMR1ON=1;
while(1);
return;
}
DC MOTOR
#include <xc.h>
void main(void){
TRISCbits.TRISC2=0;
CCP1CON=0b00001100;
T2CON=0b00000010;
PR2=61;
CCPR1L=61;
while(1){
  TMR2IF=0;
  TMR2=0;
  TMR2ON=1
  while(TMR2IF==0);
}
return;
}
