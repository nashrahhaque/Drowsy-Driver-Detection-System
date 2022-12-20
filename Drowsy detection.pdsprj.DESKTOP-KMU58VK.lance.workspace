#include <REGX51.H>

//Variable declarations

sbit EyeSensor = P1^0;
sbit AlcoholSensor = P1^6;
sbit FlameSensor = P0^0;
sbit HeartSensor = P0^1;

sbit Buzzer = P1^1;
sbit VehicleMotor1 = P1^2;
sbit VehicleMotor2 = P1^3;
sbit WaterMotor1 = P1^4;
sbit WaterMotor2 = P1^5;

sbit rs = P3^7;
sbit en = P3^6;

//Function Prototypes

void Delay(unsigned char x);
void LCD_Command(unsigned char x);
void LCD_Data (unsigned char x);
void LCD_Message (unsigned char *p);

//Main function and codee

void main(){

	VehicleMotor1=0;
	VehicleMotor2=0;
	WaterMotor1=0;
	WaterMotor2=0;
	Buzzer=0; //Buzzer is off at 0
	LCD_Command(0x38); //2 lines
	LCD_Command(0x0E); //Display ON
	LCD_Command(0x80); // Force cursor to start
	LCD_Message("DRIVER SAFETY   ");
	LCD_Command(0xc0); // Force cursor beginning of second line
	LCD_Message("SYSTEM          ");
	Delay(500);
	LCD_Command(0x01); // Clear Display
	
	
	while(1){
		
		if(EyeSensor == 1 && AlcoholSensor == 1 && HeartSensor == 1 && FlameSensor == 1){
			Buzzer=0;
			VehicleMotor1 = 0;
			VehicleMotor2 = 1;
			WaterMotor1 = 0;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("DRIVING IS       ");
			LCD_Command(0xc0);
			LCD_Message("SAFE             ");
		}
		else if(EyeSensor == 0 && AlcoholSensor == 0 && HeartSensor == 0 && FlameSensor == 0){
			Buzzer=1;
			VehicleMotor1 = 0;
			VehicleMotor2 = 0;
			WaterMotor1 = 1;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("DRIVING IS       ");
			LCD_Command(0xc0);
			LCD_Message("UNSAFE           ");
		}
		else if(EyeSensor == 1 && HeartSensor == 0 && AlcoholSensor == 1 && FlameSensor == 1){
			Buzzer=1;
			VehicleMotor1 = 0;
			VehicleMotor2 = 0;
			WaterMotor1 = 0;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("DRIVER IS       ");
			LCD_Command(0xc0);
			LCD_Message("DROWSY          ");
		}
		else if(EyeSensor == 0 && HeartSensor == 1 && AlcoholSensor == 1 && FlameSensor == 1){
			Buzzer=1;
			VehicleMotor1 = 0;
			VehicleMotor2 = 0;
			WaterMotor1 = 0;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("DRIVER IS       ");
			LCD_Command(0xc0);
			LCD_Message("DROWSY          ");
		}
		else if(EyeSensor == 1 && AlcoholSensor == 1 && HeartSensor == 1 && FlameSensor == 0){
			Buzzer=1;
			VehicleMotor1 = 0;
			VehicleMotor2 = 0;
			WaterMotor1 = 1;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("TURNING ON      ");
			LCD_Command(0xc0);
			LCD_Message("WATER VALVE     ");
		}
		else if(EyeSensor == 1 && AlcoholSensor == 0 && HeartSensor == 1 && FlameSensor == 1){
			Buzzer=1;
			VehicleMotor1 = 0;
			VehicleMotor2 = 0;
			WaterMotor1 = 0;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("DRIVER IS       ");
			LCD_Command(0xc0);
			LCD_Message("UNDER INFLUENCE ");
		}
		else{
			Buzzer = 1;
			VehicleMotor1 = 0;
			VehicleMotor2 = 0;
			WaterMotor1 = 0;
			WaterMotor2 = 0;
			LCD_Command(0x80);
			LCD_Message("LCD            ");
			LCD_Command(0xc0);
			LCD_Message("ERROR          ");
		}
	}
}

//Function Implementations

void Delay(unsigned char x){

	int i,j;
	for(i=0;i<x;i++)
	for(j=0;j<=1000;j++);
	
}

void LCD_Command(unsigned char x){

	rs=0;
	P2 = x;
	en=1;
	Delay(10);
	en=0;
	
}

void LCD_Data (unsigned char x){

	rs=1;
	P2 = x;
	en=1;
	Delay(10);
	en=0;
	
}

void LCD_Message (unsigned char *p){

	while(*p)
		LCD_Data(*p++);
	
}
