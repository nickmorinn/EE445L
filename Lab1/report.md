# EE 445L Lab 1 Report

Nick morin (npm436)

## Objectives

* I created protypes and functions for ST7735_XYplotInit() and ST7735_XYplot(). I tested the code in the simulator. 
* We were learning about the design tools (Keil), fixed-point notation and graphics.
* We did this lab to familiarize ourselves with the software, fixed-point notation and graphics. We now have a useful data plot module that can be reused for the LCD display in other labs. 

## Hardware Design

No hardware design for this lab

## Software Design

### Lab1.h 
- contains protypes for functions ST7735_XYplotInit() and ST7735_XYplot().
### Lab1.c 
- contains function definitions for ST7735_XYplotInit() and ST7735_XYplot() as well as the main function. 

```
uint32_t minX_global; 
uint32_t maxX_global; 
uint32_t minY_global; 
uint32_t maxY_global; 
uint32_t rangeX; 
uint32_t rangeY; 


void ST7735_XYplotInit(char *title, int32_t minX, int32_t maxX, int32_t minY, int32_t maxY, uint16_t bcolor){
	
	Output_Clear();
	ST7735_PlotClear(minY, maxY); // unsure about this function 
	ST7735_DrawString(0,1,title,ST7735_YELLOW); 
	
	minX_global = minX; 
	maxX_global = maxX; 
	minY_global = minY; 
	maxY_global = maxY; 
	rangeX = maxX - minX; 
	rangeY = maxY - minY; 
	
};	



void ST7735_XYplot(uint32_t num, int32_t bufX[], int32_t bufY[], uint16_t color){
	
	ST7735_SetTextColor(color);

	for(uint32_t i=0; i<num; i++) {
		ST7735_FillRect(127*(bufX[i] - minX_global)/rangeX, 32 + (127 * (maxY_global - bufY[i]))/rangeY, 2,2,color); 
	}

};
```

## Measurement Data

No measurement data for this lab

## Analysis and Discussion

* When should you use fixed-point over floating point? When should you use floating-point over fixed-point?*

	Fixed point can offer greater resolution at the expense of range when compared to floating-point. 

* Give an example application (not mentioned in the book) for fixed-point. Describe the problem, and choose an appropriate fixed-point format. (no software implementation required).*

	Fixed point notation is useful in deep neural networks. [This link](http://proceedings.mlr.press/v48/linb16.pdf) discusses increased accuracy and decreased model size with the use of fixed point versus floating point. 

* Can we use floating point on the ARM Cortex M4? If so, what is the cost?*

	Yes, however at the cost of power. The floating point processor must be turned on. 

* OPTIONAL: When should you use binary fixed-point over decimal fixed-point? When should you use decimal fixed-point over binary fixed-point?*

	When needing to multiply or divide by two, binary fixed-point has an advantage over decimal fixed-point by being able to preform the operation with just a bit shift. 
